```mermaid
flowchart LR
    DB_MASTER[(社内用語集スプレッドシート)]

    A[毎朝 GASトリガー起動] --> B{① 昨日の定例予定は<br>あったか？}
    
    B -- No（予定なし） --> C[処理スキップ・終了]
    B -- Yes（予定あり） --> D[Googleドライブ内を自動検索]
    
    D --> E{② 該当 Docs が<br>存在するか？}
    
    E -- No（未検出） --> F[Slackに「議事録未検出」通知・終了]
    E -- Yes（検出） --> G[WS内 AI要約処理を実行]
    
    G --> H{③ AI要約処理は<br>成功したか？}
    
    H -- No（エラー） --> I[管理者へエラー通知・終了]
    H -- Yes（成功） --> J[Slack times チャンネルへ要約配信]
    
    J --> K{④ ユーザーが<br>用語解説ボタンを押下？}
    
    K -- No --> L[待機終了]
    K -- Yes --> M[用語データの参照]
    DB_MASTER --> M
    M --> N[Slack上に用語解説を動的展開・完了]
