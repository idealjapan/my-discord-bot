# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

AI Keisuke Bot is a Discord bot that provides AI-powered features through emoji reactions (👍🎤❓❤️✏️📝). Users interact by adding reactions to messages after activating channels with slash commands.

## Development Commands

### Running the Bot
```bash
# macOS/Linux
./run.sh

# Windows
ai-keisuke.bat

# Manual run
python main.py
```

### Testing
```bash
# Run all successful tests only
python run_all_tests.py

# Run specific test file
python -m pytest tests/test_slash_commands_fixed.py -v
```

### Dependencies
```bash
# Install dependencies
pip install -r requirements.txt

# Key dependencies:
# - discord.py 2.5.0+
# - openai
# - Pillow
# - pydub (requires FFmpeg)
```

## Architecture Overview

### Core Bot Structure
The bot uses a reaction-based architecture where users interact via emoji reactions on messages. Key components:

1. **Premium System**: Triple-layered authentication
   - Owner user ID check (settings.json)
   - Discord role check in community server
   - Server owner auto-detection (fallback)

2. **Content Processing Pipeline**:
   - `extract_embed_content()`: Processes Discord embeds
   - `read_text_attachment()`: Async file reading with encoding detection (UTF-8/Shift-JIS)
   - Each reaction handler processes: original message → attachments → embeds

3. **File Generation**: All file uploads include descriptive messages for mobile compatibility
   - Transcription: "📄 文字起こし結果のテキストファイルです！"
   - Praise images: "🎉 褒め画像をお作りしました！"
   - Memo files: "📝 メモファイルを作成しました！"

### OpenAI Integration
- Free users: `gpt-4o-mini` model
- Premium users: `gpt-4o` model
- Whisper API for audio transcription
- Custom prompts loaded from `prompt/` directory

### Data Management
- Server settings: `data/server_data/{server_id}.json`
- User data: `data/user_data/{user_id}.json` (includes usage tracking, custom prompts)
- Activity logs: `data/activity_logs/` (DAU/MAU statistics)
- Temporary files: `attachments/` (auto-cleaned after use)

## Critical Implementation Notes

1. **File Upload Messages**: Always include descriptive text with file uploads for mobile Discord compatibility

2. **Japanese Filename Handling**: Discord strips Japanese characters from filenames. Solution: use English filenames with Japanese content inside files

3. **Premium Authentication**: Check premium status in this order:
   - Is user the configured owner? (owner_user_id in settings.json)
   - Does user have premium role in community server?
   - Is user the server owner? (fallback)

4. **Rate Limiting**: 
   - Free users: 5 uses/day (`free_user_daily_limit` in settings.json)
   - Premium users: unlimited
   - Usage tracked in user data JSON with daily reset

5. **Encoding**: Handle both UTF-8 and Shift-JIS for text file reading

6. **Error Handling**: 
   - Connection errors: Check DISCORD_TOKEN in .env
   - OpenAI errors: Verify OPENAI_API_KEY in .env
   - FFmpeg errors: Ensure FFmpeg is installed for audio processing

## Key Functions and Classes

- `StatsManager`: Handles DAU/MAU statistics
- `CustomPromptModal`: UI for custom prompt configuration
- `make_praise_image()`: Generates praise images with PIL
- `shorten_url()`: URL shortening via is.gd API
- Slash commands: `/activate`, `/deactivate`, `/status`, `/stats`, `/set_custom_prompt_*`

## Environment Setup

Required environment variables (.env file):
```
DISCORD_TOKEN=your_discord_bot_token
OPENAI_API_KEY=your_openai_api_key
```

## Testing Approach

The project includes test files in `tests/` directory. Run `python run_all_tests.py` to execute only passing tests, avoiding known failures in the test suite.