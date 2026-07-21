```mermaid
flowchart TD
    %% 前半：自動投稿
    subgraph AutoPost [【前半】自動要約・投稿フロー]
        A[📄 定例会Docs作成] -->|指定フォルダに保存| B(📁 Google ドライブ)
        B -->|ファイル追加を検知| C[🤖 Workspace Studio]
        
        M1[(📚 用語集マスター)] -.->|用語リストのみ参照| D
        
        subgraph AI_Standardize [AI要約・表記統一]
            C -->|テキスト抽出| D[✨ Gemini]
            D -->|表記統一・要約生成| C
        end

        C -->|要約・用語リスト書き込み| E[(📊 ログスプレッドシート)]
        E -->|onChangeトリガー| F[⚙️ GAS]
        F -->|JSON送信 (Block Kit)| G[🔗 Slack Incoming Webhook]
        G -->|ボタン付き通知投稿| H[💬 Slack チャンネル]
    end

    %% 後半：インタラクティブ
    subgraph Interactive [【後半】ボタンクリック連動フロー]
        H -.->|ユーザーがボタンをクリック| I[🖥️ Slack Platform]
        I -->|POSTリクエスト (Payload)| J[⚙️ GAS (Web App)]
        
        J -->|該当用語の解説を取得| M1
        J -->|chat.update呼び出し| I
        I -->|メッセージを更新（解説追加）| H
    end

    %% スタイル設定
    classDef main fill:#f9f,stroke:#333,stroke-width:2px;
    classDef sheets fill:#e1f5fe,stroke:#0277bd,stroke-width:2px;
    classDef ai fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,stroke-dasharray: 5 5;
    classDef slack fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px;

    class A,C,F,J main;
    class B,E,M1 sheets;
    class D ai;
    class G,H,I slack;
```
