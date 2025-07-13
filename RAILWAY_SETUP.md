# Railway でのホスティング手順

## 1. 前準備

### 必要なアカウント
- [Railway](https://railway.app/) アカウント
- Discord Bot Token
- OpenAI API Key

### 自分用の無制限設定
`settings.json` を編集して、`owner_user_id` を自分のDiscordユーザーIDに変更：
```json
{
  "owner_user_id": "あなたのDiscordユーザーID"
}
```

DiscordユーザーIDの確認方法：
1. Discord開発者モードを有効化（設定 → 詳細設定 → 開発者モード）
2. 自分のプロフィールを右クリック → 「ユーザーIDをコピー」

## 2. Railwayでのセットアップ

### ステップ1: プロジェクト作成
1. [Railway](https://railway.app/) にログイン
2. 「New Project」をクリック
3. 「Deploy from GitHub repo」を選択
4. このリポジトリを選択（フォークした場合はフォーク先を選択）

### ステップ2: 環境変数の設定
Railwayのプロジェクトで「Variables」タブから以下を設定：

```
DISCORD_BOT_TOKEN=あなたのDiscord BotのToken
OPENAI_API_KEY=あなたのOpenAI APIキー
```

### ステップ3: デプロイ
1. 設定が完了すると自動的にデプロイが開始
2. 「Logs」タブでBotが正常に起動したか確認
3. 「Successfully logged in as [Bot名]」と表示されれば成功

## 3. トラブルシューティング

### FFmpegエラーが出る場合
すでに`nixpacks.toml`でFFmpegのインストールを設定済みですが、もし問題が発生した場合：
- RailwayのBuildpacksでFFmpegサポートを確認

### メモリ不足エラー
- Railwayの無料プランには制限があるため、必要に応じて有料プランへアップグレード

### Botがオフラインのまま
1. 環境変数が正しく設定されているか確認
2. Discord Bot TokenとOpenAI APIキーが有効か確認
3. RailwayのLogsでエラーメッセージを確認

## 4. 無料枠について

Railwayの無料プランの制限：
- 月$5相当のクレジット
- 実行時間制限あり

継続的に使用する場合は有料プラン（$5/月〜）への移行を検討してください。

## 5. 代替ホスティングサービス

他の選択肢：
- **Heroku**: Procfileがすでに用意されているので対応可能
- **VPS**: DigitalOcean, Vultr, Linode など（月$5〜）
- **自宅サーバー**: Raspberry Piなどでも動作可能