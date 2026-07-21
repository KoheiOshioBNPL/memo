```mermaid
flowchart TD
    %% データベース定義（円柱記号）
    DB_MASTER[(マスターDB<br>用語集スプシ)]
    DB_LOG[(実行ログDB<br>スプレッドシート)]

    %% 自動配信処理フロー
    A[毎朝 GASトリガー起動] --> B{① 昨日の定例予定は<br>あったか？}
    
    B -- No（予定なし） --> C[スキップ処理] --> DB_LOG
    B -- Yes（予定あり） --> D[Googleドライブ内を自動検索]
    
    D --> E{② 該当 Docs が<br>存在するか？}
    
    E -- No（未検出） --> F[Slackに「議事録未検出」通知] --> DB_LOG
    E -- Yes（検出） --> G[WS内 AI要約処理を実行]
    
    G --> H{③ AI要約処理は<br>成功したか？}
    
    H -- No（エラー） --> I[管理者へエラー通知] --> DB_LOG
    H -- Yes（成功） --> J[Slack times チャンネルへ要約配信] --> DB_LOG
    
    %% インタラクティブ処理フロー
    J --> K{④ ユーザーが<br>用語解説ボタンを押下？}
    
    K -- No --> L[待機終了]
    K -- Yes --> M[用語データの参照]
    DB_MASTER --> M
    M --> N[Slack上に用語解説を動的展開]
    N --> O[閲覧ログの保存] --> DB_LOG
