# さつきあん ゲストガイド

沖縄・宮古島の民宿「さつきあん宮古島」の宿泊客専用デジタルガイド。単一の静的HTMLファイル(`index.html`)で、ビルド不要・依存パッケージなし。

## 構成

- `index.html` — アプリ本体(HTML/CSS/JSすべて1ファイルに内包)
- `content/satsukian_guide_content.xlsx` — 表示内容(4言語)のマスターデータ。内容を変更する際はこのExcelを直接編集してから `index.html` に反映する運用

## 内容の言語

日本語・英語・繁体中文(台湾からの旅行者向け)・韓国語をボタンで切り替え。`index.html` 内の `const T = {...}` オブジェクトに4言語分の文言がまとまっている。

## 重要な設計上の制約

- 宿泊客は運営者のClaudeアカウントの組織メンバーではない外部の一般利用者のため、Claude Artifactの `db` / `sample` などのランタイム機能は使用不可(組織内限定のため公開共有と両立しない)。そのため:
  - 表示内容はすべて `index.html` に静的に埋め込み(4言語分を事前翻訳済み)
  - オーナーへの連絡はメール(`mailto:`)リンクのみ
  - Wi-Fiパスワード等は実データをそのまま埋め込み(このファイルの取り扱いに注意)
- インタラクションは**すべて `addEventListener` によるイベント委譲**で実装している。`onclick="..."` のようなインライン属性ハンドラは、Claude Artifactの CSP でブロックされ動作しない実績があるため、今後も避けること。

## 実データ

- 住所: 沖縄県宮古島市下地川満879
- 電話(代表): 070-8350-6509 / 緊急連絡先: 090-5655-0299(倉橋)
- メール: satsukian.miyakojima@gmail.com
- お部屋: 102号室(最大8名・バリアフリー)/ 201号室(最大12名・屋上テラス)/ 202号室(最大10名・ファミリー向け)
- Wi-Fi SSID/パスワードは `content/satsukian_guide_content.xlsx` の「Wi-Fi_接続情報」シートが正。

## 公開について

現在は Claude Artifact としても公開中: https://claude.ai/code/artifact/a8cf1aa6-3aa7-4af3-a9d6-14c4c9c74436

VS Code側で `index.html` を編集しても、この Artifact URL には自動反映されない。Artifact側に反映したい場合は、更新した `index.html` を持って元のClaude会話(またはこのファイルを添付した新しい会話)に戻り、Artifactツールで再公開する必要がある。独立して公開したい場合は GitHub Pages 等へのデプロイを検討。
