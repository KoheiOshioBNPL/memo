```mermaid
graph TD
    subgraph GW ["Google Workspace 領域"]
        node1["📄 1. 入力: Googleドキュメントの対象タブに追記"]
        node2["🤖 2. 処理・要約: ドキュメント読み取り、差分抽出、Gemini要約"]
        logDB[("📝 3. 記録: ログ用スプレッドシート")]
        node4["⚙️ 4. 読み取り: スプシ更新を検知、Webhookリクエスト処理"]
    end

    node5["💬 5. 出力: Slackへ要約・タブ直リンクを自動投稿"]

    node1 -->|追記テキスト| node2
    node2 -->|要約データ + タブURL| logDB
    logDB -->|記載データを取得| node4
    node4 -->|Incoming Webhook| node5
