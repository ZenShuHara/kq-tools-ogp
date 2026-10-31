# kq-tools-ogp

コアサーバーに置いているサイト（https://knowledgequest.jp/ の各ページなど）の **OGP 画像（リンクのプレビュー用）** を GitHub Pages で配信するリポジトリです。どのサイト・どのプロジェクトのページでも使います。

- 配信 URL：`https://zenshuhara.github.io/kq-tools-ogp/<ファイル名>.png`
- 各ページの `og:image` / `twitter:image` はこの URL を指します（`?v=日付` で版を付ける）

## なぜ別に置くのか

コアサーバーでは、Discord がリンクのプレビューを作るときに、画像を取れないことがあります（ページのタイトル・説明は出るが画像だけ出ない。ときにはページごと取れない）。2026-10-12・10-25・11-01 に確認しました。サーバーのボット対策 Imunify360 が原因と推定しています。

- Discordbot と名乗って手元から取ると、ふつうに 200 が返ります。名乗りや直リンクで弾いているのではないので、`.htaccess` で Discordbot を許可しても直りません。
- ネット上の「`.htaccess` で Discordbot だけを許可する」例（`Deny from all` ＋ `Allow from env=discord_bot`）は、ほかの人を全員締め出すので、使わないでください。

## 画像を足す・変えるとき

1. **画像を作る**: 1200×630 の PNG。ファイル名は `<ページの名前>.png`（英数字。例：`listfilter.png`）。正本はそのサイトのリポジトリに置き、ここにはコピーを置きます。
2. **遅れを確かめる**: このリポジトリは共用です。`git fetch` して `git rev-list --left-right --count main...origin/main` で遅れを確かめます。
   - 遅れていたら、ZEN さんに確かめてから `git merge --ff-only origin/main` で取り込みます。
   - `git pull` は使いません。
3. **置いて push する**: 画像を置き、下の「ファイル」の表に1行足して、コミットして push します。約20秒で GitHub Pages に出ます。
   - `curl -sI https://zenshuhara.github.io/kq-tools-ogp/<ファイル名>.png` で 200 と `image/png` を確かめます。
   - ほかの人のファイルは変えません。
4. **ページから指す**: ページの `og:image` / `twitter:image` を、`https://zenshuhara.github.io/kq-tools-ogp/<ファイル名>.png?v=YYYYMMDD` にします。
5. **画像を作り直したら**: 同じ名前で置き直し、ページ側の `?v=` を新しくします。Discord は URL ごとにプレビューを覚えるためです。
6. **Discord で確かめる**: 確かめるときは、ページの URL に `?v=3` など、まだ使っていない番号を付けて貼ります。

## ページごと取れないとき（共有用ページ）

タイトルや説明まで出ない（ページそのものが取れない）ときは、ここに共有用のページを作り、そちらの URL を貼ります。例：`zenresearch/`。

- `<名前>/index.html` に og: / twitter: のタグだけを書きます。
- すぐに本物のページへ移動させます（meta refresh 0 ＋ `location.replace`。移動しないとき用のリンクも置く）。
- 本物のページの og: を変えたら、共有用ページも合わせます。

## ファイル

| ファイル | 使うページ |
|---|---|
| `home.png` | Knowledge Quest Tools のトップ（/tools/）・ログイン（login.php） |
| `news.png` | 更新情報（/tools/news/） |
| `<ツールのディレクトリ名>.png` | /tools/ の各ツール（am2mf, ys2mf, ya2mf, me2mf, ra2mf, E2O, refund_analyzer, AmazonOrderRecord, KeepaSyncPro, AmazonAppealCases）。正本は `MF-Conversion` の `tools/sozai/ogp/`（トップは `tools/sozai/ogp-image.png`） |
| `listfilter.png` | プレリサーチ（/listfilter/）。正本は `C:\dev\リストフィルタ\web\ogp.png` |
| `zenresearch.png` | ZenResearch（/zenresearch/ 全ページ）。正本は knowledgequest.jp の zenresearch/ogp.png |

| 共有用ページ | 移動先 |
|---|---|
| `zenresearch/` | https://knowledgequest.jp/zenresearch/ （2026-10-25 に作成。サーバーのログに Discord の取得の記録が無かったため） |
