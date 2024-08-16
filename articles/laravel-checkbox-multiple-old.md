---
title: "複数選択のcheckboxでoldを使ってcheckedさせたい"
emoji: "❄️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Laravel", "PHP", "初心者"]
published: true
---

追記（2024/8/16）
コメントで教えていただいたのですが、Laravelの9からbladeには@selectedが追加されており、この記事のようにややこしいことをする必要はなくなりました
めでたい！
https://laravel.com/docs/master/blade#additional-attributes



忘れた頃に実装することになり、毎度自分が困るので、記録に残したいと思います。
コードが短くなるように考えましたが、もっと良い書き方があれば教えていただけますと幸いです

## 完成形
```php
<input type="checkbox" name="actor[]" value="{{ $actor->id }}"
	{{ !empty(old("actor")) && in_array((string)$actor->id, old("actor"), true) ? 'checked' : ''}}
	{{ $actor->movies->contains('id', $movie->id) ? 'checked' : ''}}>
	<p>{{ $actor->name }}</p>
```

### 前提
* 実装時は、多対多のテーブルを紐付ける中間テーブルへの登録に対しての内容です
* 各モデルにはリレーションが設定されています
* Laravelのバージョンは8.1です
* シンプルにbladeで実装したいです
* 新規作成時も編集時もバリデーションがかかった時もこれ一つで対応したいという盛りだくさんなものです
* 完成形は例ですが「映画情報を編集する時、どの俳優が出ていたかを選択する画面」の想定です。

### 詳細
1行ずつやりたいことの詳細を記載します。

```php
<input type="checkbox" name="actor[]" value="{{ $actor->id }}"
```
ここはシンプルなinputタグの内容です。
nameが配列になっているのが忘れがちですがポイントです。

```php
{{ !empty(old("actor")) && in_array((string)$actor->id, old("actor"), true) ? 'checked' : ''}}
```
この三項演算子は、このような意図で記載しています。
`!empty(old("actor"))`でバリデーションにかかった値があるかをみています。

`in_array((string)$actor->id, old("actor"), true)`で、actorの中に自身のidがないかを探します。
これでバリデーションにかかった時にどれにチェックをしていたかを確認します。

in_arrayの第3引数のtrueを無くせば、`(string)$actor->id`のstringはなくても自動で判定します。

https://qiita.com/ritukiii/items/3a6add378ae089ab5d70

```php
{{ $actor->movies->contains('id', $movie->id) ? 'checked' : ''}}>
```
この三項演算子は、編集画面の表示用です。

今回の場合、actorとmovieは多対多でリレーションがあります。
$actor->moviesとすることで、リレーションでmovieを引っ張ってくることができます。
映画を編集する時、どの俳優が出ていたかを選択する画面なので、
すでにその俳優が選択されていたら、俳優の情報から該当の映画情報がついてくるはずなので、その映画情報が含まれるかを検証します

containsは戻り値がbool型なので、そのまま判定に使用します。
https://laravel.com/docs/8.x/collections#method-contains

以上です！

## 参考
https://qiita.com/Ioan/items/a851ef1099718d079c8c
https://zenn.dev/fuwakani/articles/c3e8aa9c443eda14836e



