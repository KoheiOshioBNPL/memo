graph TD
    subgraph GW ["Google Workspace 領域 (ノーコード / 内蔵AI)"]
        node1["📄 1. 入力: Googleドキュメント<br/>対象タブに追記"]
        node2["🤖 2. 処理・要約: ドキュメント読み取り<br/>差分抽出・直リンクURL取得<br/>Geminiによる要約"]
        logDB["📝 3. 記録: ログ用スプレッドシート<br/>へ要約・URLを記載"]
    end

    subgraph GAS ["GAS 領域 (最小中継)"]
        node4["⚙️ 4. 読み取り: スプシの更新を検知<br/>Webhookリクエスト処理"]
    end

    subgraph Output ["通知先"]
        node5["💬 5. 出力: Slackへ要約・<br/>タブ直リンクを自動投稿"]
    end

    %% フロー接続
    node1 --> node2
    node2 --"要約データ + タブURL"--> logDB
    logDB --"記載データを取得"--> node4
    node4 --"Incoming Webhook"--> node5
