---
title: "Ruby そういう動きするんだと思ったTips"
emoji: "🍑"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Ruby", "初心者", "AtCoder"]
published: true
---

初歩的なことだとは思いますが、恥ずかしながら知らず、「あ、そういうのできるんだ」と思ったこと集です

### 配列に対して -1 のindexを指定することで末尾を取ってこれる
```
array = ["aaa", "bbb", "ccc"]
array[-1] # => "ccc"
```

### 同じ型同士の配列を - すると内容の差分が取ってこれる
（公式から引用）
```
[1, 2, 1, 3, 1, 4] - [1, 4]    # => [2, 3]
```

https://docs.ruby-lang.org/ja/latest/class/Array.html#I_--2D

### 文字列はindex指定で内容を取ってくることができる
```
s = "ruby"
s[2] # => "b"
```