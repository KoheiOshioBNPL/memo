```mermaid
flowchart TD
    subgraph Flow1 ["① 【定例翌日】カレンダー自動検知 ＆ ドライブ自動検索 ＆ 要約配信"]
        A[Gカレの予定を自動検知] --> B[該当Docsをドライブから自動検索]
        B --> C[WS内AIによる要約生成]
        C --> D[Slack times チャンネルへ投稿<br>・要約<br>・Docs直リンク<br>・用語解説ボタン]
    end

    subgraph Flow2 ["② 【随時】Slackからの「用語解説」動的展開"]
        D -. 配信メッセージ .-> E[ユーザーがボタンを押す]
        E --> F[本物用語集を参照]
        F --> G[社内用語の意味がSlack上に一瞬で展開]
    end
