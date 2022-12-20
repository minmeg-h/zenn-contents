---
title: "Zennとgithubを連携してみる"
emoji: "😎"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: false #trueにすることでzennに公開される
---

GitHubリポジトリでZennのコンテンツを管理する
https://zenn.dev/zenn/articles/connect-to-github

その次はこちら
Zenn CLIをインストールする
https://zenn.dev/zenn/articles/install-zenn-cli

node.jsがないので入れてみます
https://nodejs.org/ja/
とりあえず推奨版で。

画面をとりあえずぽちぽちする

```
% node -v
v18.12.1
% npm -v
8.19.2
```
PATH通さなくても行けた

```

% npm init --yes
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
zenn-docs % npm install zenn-cli

added 1 package, and audited 2 packages in 3s

found 0 vulnerabilities
npm notice 
npm notice New major version of npm available! 8.19.2 -> 9.2.0
npm notice Changelog: https://github.com/npm/cli/releases/tag/v9.2.0
npm notice Run npm install -g npm@9.2.0 to update!
npm notice 
```

```
zenn-docs % npx zenn init

  🎉  Done!
  早速コンテンツを作成しましょう

  👇  新しい記事を作成する
  $ zenn new:article

  👇  新しい本を作成する
  $ zenn new:book

  👇  投稿をプレビューする
  $ zenn preview
```

```
npx zenn new:article --slug my-awesome-article
```

nodeを終了する方法(コマンド)４選
https://qiita.com/anoonoll/items/ec1cc54d2e442699fabd

```

minmeg@minmegnoMacBook-Pro zenn-docs % npx zenn new:article --slug zenn-github-alignment
created: articles/zenn-github-alignment.md
minmeg@minmegnoMacBook-Pro zenn-docs % git init    
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint:   git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint:   git branch -m <name>
Initialized empty Git repository in /Users/minmeg/workspace/zenn-docs/.git/
minmeg@minmegnoMacBook-Pro zenn-docs % git add .
minmeg@minmegnoMacBook-Pro zenn-docs % git remote add origin git@github.com:minmeg-h/zenn-docs.git
minmeg@minmegnoMacBook-Pro zenn-docs % git push
fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin master

minmeg@minmegnoMacBook-Pro zenn-docs % git branch -M main
minmeg@minmegnoMacBook-Pro zenn-docs % git push                 
fatal: The current branch main has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin main

minmeg@minmegnoMacBook-Pro zenn-docs % git push --set-upstream origin main
Enumerating objects: 8, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 4 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (8/8), 1.04 KiB | 530.00 KiB/s, done.
Total 8 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:minmeg-h/zenn-docs.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.

```
