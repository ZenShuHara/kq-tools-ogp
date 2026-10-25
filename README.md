# kq-tools-ogp

Knowledge Quest Tools（https://knowledgequest.jp/tools/）の **OGP 画像（リンクのプレビュー用）** を GitHub Pages で配信するリポジトリです。

- 配信 URL：`https://zenshuhara.github.io/kq-tools-ogp/<ファイル名>.png`
- 各ページの `og:image` / `twitter:image` はこの URL を指します（`?v=日付` で版を付ける）

## なぜ別に置くのか

サイトのサーバー（コアサーバー）では、Discord がリンクのプレビュー用に画像を取りに来ると取得できないことがありました（ページのタイトル・説明は出るが画像だけ出ない。2026-10-12 確認。サーバーのボット対策 Imunify360 が原因と推定）。OGP 画像だけを GitHub Pages から配信して回避しています。

## ファイル

| ファイル | 使うページ |
|---|---|
| `home.png` | トップ（/tools/）・ログイン（login.php） |
| `news.png` | 更新情報（/tools/news/） |
| `<ツールのディレクトリ名>.png` | 各ツール（am2mf, ys2mf, ya2mf, me2mf, ra2mf, E2O, refund_analyzer, AmazonOrderRecord, KeepaSyncPro, AmazonAppealCases） |
| listfilter.png | プレリサーチ（/listfilter/） |
| `zenresearch.png` | ZenResearch（/zenresearch/ 全ページ。正本は knowledgequest.jp の zenresearch/ogp.png） |

## 共有用ページ（zenresearch/）

`https://zenshuhara.github.io/kq-tools-ogp/zenresearch/` は Discord などに貼るための共有用ページです。og:/twitter: タグだけを持ち、すぐに https://knowledgequest.jp/zenresearch/ へ移動します（meta refresh 0 ＋ location.replace、移動しないとき用のリンクあり）。サーバー側で Discord のページ取得が届かない（2026-10-25 確認、ログに取得の記録なし）ため。本ページの og: を変えたら、ここも合わせてください。

## 画像を足す・変えるとき

正本はサイトのリポジトリ（`MF-Conversion` の `tools/sozai/ogp/`、トップは `tools/sozai/ogp-image.png`）にあります。画像を作り直したら、ここにも同じ名前で置いて push し、ページ側の `?v=` を新しくしてください（Discord などは URL ごとにプレビューを覚えるため）。
