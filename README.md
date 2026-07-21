```mermaid
flowchart TD
    A[📄 Google ドキュメント作成] -->|指定フォルダに保存| B(📁 Google ドライブ)
    B -->|ファイル追加を検知| C[🤖 Google Workspace Studio]
    
    subgraph AI解析・標準化処理
        C -->|テキスト抽出| D[✨ Gemini]
        M[(📚 社内用語マスター)] -->|用語統一・粒度ルール参照| D
        D -->|表記統一・要約生成| C
    end

    C -->|標準化データを書き込み| E[(📊 議事録ログスプレッドシート)]
    E -->|トリガー発火 onChange| F[⚙️ GAS]
    F -->|Webhook 送信| G[🔗 Slack Incoming Webhook]
    G -->|通知投稿| H[💬 Slack チャンネル]
```
