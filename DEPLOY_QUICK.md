# 🚀 Railwayクイックデプロイガイド

## ⚡ 3分でデプロイ完了！

### ステップ1: APIキーの準備（2分）

1. **Discord Bot Token**
   - https://discord.com/developers/applications
   - 「New Application」→ アプリ名入力
   - 「Bot」→ 「Reset Token」→ トークンコピー

2. **OpenAI API Key**
   - https://platform.openai.com/api-keys
   - 「Create new secret key」→ キーコピー

### ステップ2: 無制限設定（30秒）

`settings.json`を編集：
```json
{
  "owner_user_id": "あなたのDiscordユーザーID"
}
```

> DiscordユーザーID取得：設定→詳細設定→開発者モードON→自分を右クリック→IDコピー

### ステップ3: Railwayデプロイ（30秒）

1. **https://railway.app/** にアクセス
2. 「Start a New Project」
3. 「Deploy from GitHub repo」
4. このリポジトリを選択

### ステップ4: 環境変数設定（30秒）

Railwayで「Variables」タブ：
```
DISCORD_BOT_TOKEN = 先ほどコピーしたDiscordトークン
OPENAI_API_KEY = 先ほどコピーしたOpenAIキー
```

### ✅ 完了！

「Logs」タブで以下が表示されれば成功：
```
Successfully logged in as [あなたのBot名]
```

---

## 🎯 Bot使用方法

1. **サーバーにBotを招待**
   - Discord Developer Portal → OAuth2 → URL Generator
   - Scopes: `bot`, `applications.commands`
   - Bot Permissions: 必要な権限を選択
   - 生成されたURLでサーバーに招待

2. **チャンネル有効化**
   ```
   /activate
   ```

3. **使用開始**
   - メッセージに👍🎤❓❤️✏️📝のリアクションを付ける
   - 無制限で利用可能！

---

## 🔧 トラブルシューティング

| エラー | 解決方法 |
|--------|----------|
| Bot offline | 環境変数が正しく設定されているか確認 |
| FFmpeg error | 自動インストール済み、しばらく待つ |
| API error | OpenAIキーが有効か確認 |

**完全無料**: Railway月$5クレジット内で24時間稼働可能