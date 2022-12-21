---
title: "Zennとgithubを連携してみる"
emoji: "😎"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["git", "github", "zenn"]
published: true #trueにすることでzennに公開される
---

公式の記事を見ながらやってみたので、自分への備忘録もかねて、共有したいと思います。
## 1.GitHubリポジトリをZennのコンテンツを連携する

参考記事:【公式】GitHubリポジトリでZennのコンテンツを管理する
https://zenn.dev/zenn/articles/connect-to-github

公式の記事を読みながらサクッとやってみる
GithubをリポジトリをZennで指定するだけでいいのか、とっても便利！

色々と調べているうちに興味深い記事がありました
https://zenn.dev/j5c8k6m8/articles/zenn-github-repository-name

リポジトリ名ってとりあえずすごく悩みますよね…
自分は公式の記事に沿ってzenn-docsにしました

## 2.Zenn CLIをインストールする

参考記事:【公式】Zenn CLIをインストールする
https://zenn.dev/zenn/articles/install-zenn-cli

Zenn CLIがあるとさらに便利に使えるらしい、ということで入れてみます。

まずはnode.jsがないのでインストールします
https://nodejs.org/ja/

推奨版のインストーラーをダウンロード、ダウンロード先のディレクトリ等を変更する必要はありませんでした。
インストールができたか確認します。

```
% node -v
v18.12.1
% npm -v
8.19.2
```
いけましたね！

後は参考記事にしたがってセットアップしていきます

```
% npm init --yes　　# プロジェクトをデフォルト設定で初期化
Wrote to /Users/minmeg/workspace/zenn-docs/package.json:

{
  "name": "zenn-docs",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

```
% npm install zenn-cli　# zenn-cliを導入

added 1 package, and audited 2 packages in 3s

found 0 vulnerabilities
npm notice 
npm notice New major version of npm available! 8.19.2 -> 9.2.0
npm notice Changelog: https://github.com/npm/cli/releases/tag/v9.2.0
npm notice Run npm install -g npm@9.2.0 to update!
npm notice 
```

```
% npx zenn init　# セットアップを行う

  🎉  Done!
  早速コンテンツを作成しましょう

  👇  新しい記事を作成する
  $ zenn new:article

  👇  新しい本を作成する
  $ zenn new:book

  👇  投稿をプレビューする
  $ zenn preview
```

🎉が出た！やったね🎉🎉

この時点で最初のコミットしてしまいます

```
% git init
% git add .
% git commit
% git remote add origin git@github.com:~~~
% git branch -M main
% git push --set-upstream origin main
```

## 3.記事を書いてみる

参考記事:【公式】Zenn CLIで記事・本を管理する方法
https://zenn.dev/zenn/articles/zenn-cli-guide

さっそく記事を書いてみましょう！（これです）
オプションでslugが任意のものを付けられるようです

```
% npx zenn new:article --slug zenn-github-alignment
created: articles/zenn-github-alignment.md
```

プレビューもできるようです！

```
% npx zenn preview
👀 Preview: http://localhost:8000
```

保存したらプレビューにも反映されています。
プレビューを終了するには control + C です
macのcontrolボタンが分からず少し途方に暮れました😇

そしてマークダウン上部の`published: false`をtrueにすると…
投稿されました！👏

自分の手元に履歴も残るし、編集しやすくてとってもいいですね
どんどん書いていきたいです


#### 参考になりそうな記事
https://zenn.dev/zenn/articles/markdown-guide

