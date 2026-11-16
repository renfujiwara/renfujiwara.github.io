# renfujiwara.github.io

個人ホームページのソースです。GitHub Pages が push のたびに Jekyll で自動的にビルドするので、
更新は `_data/` の YAML ファイルを書き換えて push するだけです（HTML を触る必要はありません）。

## ページ構成

| URL | 内容 | 日本語版 |
|---|---|---|
| `/` | 自己紹介、お知らせ、代表論文、進行中のプロジェクト、出張予定 | `/ja/` |
| `/publications/` | 全論文 | `/ja/publications/` |
| `/projects/` | 外部資金などのプロジェクト（1件以上登録するとメニューに現れる） | `/ja/projects/` |
| `/cv/` | 略歴、受賞・フェローシップ | `/ja/cv/` |

## 更新のしかた

| やりたいこと | 編集するファイル | 書き方 |
|---|---|---|
| 論文を追加する | `_data/publications.yml` | 同じ種別（`type`）の一番上に1件追加。番号（`[C9]` など）は自動 |
| 論文を代表論文にする | `_data/publications.yml` | その論文に `selected: true` を付ける |
| 論文のリンクを追加する | `_data/publications.yml` | `paper:` / `slides:` / `code:` / `bib:` に URL を書く（書いたものだけ表示） |
| お知らせを追加する | `_data/news.yml` | 一番上に1件追加。最新5件より古いものは自動で折りたたまれる |
| 出張予定を追加する | `_data/travels.yml` | 日程の早い順に追加。`end`（最終日）を過ぎると自動で「過去の予定」へ |
| プロジェクトを追加する | `_data/projects.yml` | ファイル内の見本をコピーして記入。`ongoing: true` ならトップページにも表示 |
| 略歴・受賞を追加する | `_data/cv.yml` | `history` または `awards` に1件追加 |
| 自己紹介・リンクを変える | `_data/profile.yml` | |
| 見出し・メニューの文言を変える | `_data/ui.yml` | `en` と `ja` の両方を直す |
| 論文の種別を増やす | `_data/pubtypes.yml` | `key`・番号の頭文字・見出しを追加 |

各ファイルの先頭に、項目の意味と見本をコメントで書いてあります。

### YAML で気をつけること

- 値に「`: `」（コロン＋空白）や `#` を含むときは、全体を `"..."` で囲む（論文タイトルに多い）。
- 字下げは半角スペースで、上下の項目とそろえる（タブは使えません）。
- 論文・プロジェクトの `title_ja` などは、日本語ページで別の表記にしたいときだけ書く（省略すると英語側と同じ表記になる）。
- お知らせ・出張予定は `ja` を省略すると `en` の文が日本語ページにも出る。略歴・受賞は、書いていない言語のページには出ない。

## 仕組み

- `_layouts/default.html` … 全ページ共通のヘッダー・メニュー・フッター
- `_layouts/home.html` ほか … 各ページの中身（`_data/` の内容を並べる）
- `_includes/pub-items.html` … 論文1件分の表示
- `index.html`、`ja/index.html` など … 「どのレイアウトを・どの言語で・どの URL に出すか」だけを書いた数行のファイル
- `assets/css/main.css` … スタイル、`assets/img/profile.webp` … プロフィール写真（表示サイズに合わせた 288×384px）

## 手元でプレビューする（任意）

Ruby が入っていれば、次のコマンドで http://localhost:4000 に表示できます。

```sh
bundle install
bundle exec jekyll serve
```

手元で確認しない場合、この手順と `Gemfile` は不要です。
push 後のビルドに失敗したときは GitHub からメールが届き、公開中のサイトは直前の状態のまま残ります。
