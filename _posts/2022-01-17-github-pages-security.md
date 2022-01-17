---
layout: post
title:  "github pagesのセキュリティチェックとブログの体裁を整える"
date:   2022-01-17 +0900
categories: github pages 
---

github pagesにブログを作ったはいいけど、ブログとしてのセキュリティは問題ないのかとか、悪意のある人が自分のリポジトリに変なものを勝手にpr（プルリクエスト）してマージされたらどうしよう思ったので、セキュリティについて調べてみた。

## HTTPS で GitHub Pages サイトを保護する
[公式ドキュメント](https://docs.github.com/ja/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)に以下のような記載がありました。
```
HTTPS は、他者によるあなたのサイトへのトラフィックの詮索や改ざんを防ぐ暗号化のレイヤーを追加します。 透過的に HTTP リクエストを HTTPS にリダイレクトするために、あなたの GitHub Pages サイトに HTTPS を強制できます。
```

ネットワークに詳しくないのですが、HTTPSを設定することでサイトを暗号化してくれるようです。
方法も公式ドキュメントに記載してありますが、簡単にまとめると、
github > setting > pages > Enforce HTTPS(一番下までスクロール)
の`Enforce HTTPS`部分にチェックを入れることで設定できます。（私のサイトでははじめから設定されていました。）

## 承認がないとpr（プルリクエスト）をマージできなくする
だれかが勝手にprをマージできないように設定できるようです。
[（参照）](https://zakkuri.life/github%E3%81%A7%E5%8B%9D%E6%89%8B%E3%81%AB%E3%83%9E%E3%83%BC%E3%82%B8%E3%81%95%E3%82%8C%E3%81%AA%E3%81%84%E3%82%88%E3%81%86%E3%81%AB%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E3%82%92%E4%BF%9D%E8%AD%B7/)

コードオーナーの承認がないとマージできなくなる仕組みもあるようですが、こちらは複数人での作業時に使うものみたいなので、今回は割愛します。
やり方は簡単で、github のマイページから setting > branch > add rules
から好きなruleを追加します。
私は`Require a pull request before merging(マージ前にprを要求する)`と`Require approvals(承認要求)1`を追加しました。
こうすることでマージするためにprを作成しなければならないようになり、承認も一人以上が承認しないとマージできなくなりました。
これで誤ったソースがmainにマージされることが防げるのではないでしょうか。それでは！