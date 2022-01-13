---
layout: post
title:  "jekyllのテーマをgithub pagesに反映させる"
date:   2022-01-13 +0900
categories: jekyll 
---

[前回の記事](https://ihpolyphe.github.io/jekyll/2022/01/12/jekyll_github_pages_setup.html)でgithub pagesに記事を作成する方法をまとめました。今回は作成したページにjekyllのテーマを導入し、github pagesに反映させるまでの方法になります。

### 今回やりたいこと
- テーマの導入
- ローカル環境で確認
- github pagesに反映

導入しているところで躓くことが結構あったので細かめにまとめようと思います。

## テーマの導入
jekyllでのテーマの導入方法は多くのページでまとめられていますので、ここでは簡単に説明していきます。
まずは[ここから](http://jekyllthemes.org/)好きなテーマを見つけて、`homepages`からgithubページに移動します。
私は[こちら](https://github.com/chrisbobbe/jekyll-theme-prologue)のテーマにすることにしました。（このテーマはすでに管理対象から外れているようなので、そのあたりが気になる方は使用しない方がよさそうです。）

次にURLをコピーし、ローカル環境にクローンします。
    
    git clone https://github.com/chrisbobbe/jekyll-theme-prologue
    cd jekyll-theme-prologue
    bundle install
これでエラーなく完了すればokです。

## ローカル環境で確認

その後以下のコマンドでローカル環境でテーマが起動できるか確認します。

    bundle exec jekyll serve

私はこのコマンドをたたいたところ、エラーが出たので、`Gemfiles`に以下のコードを追加します。
```
gem "kramdown-parser-gfm"
gem 'wdm', '>= 0.1.0'
gem "webrick"
```
[https://github.com/jekyll/jekyll/issues/8523](https://github.com/jekyll/jekyll/issues/8523)

これで[http://127.0.0.1:4000/]( http://127.0.0.1:4000/)からテーマが導入できていることがわかります。

## Github pagesに反映させる
Github pagesに反映されるためには、github actionsというCI/CDを行うシステムでビルドを通過し、デプロイされるまで反映されません。
現在の`_config.yaml`では`theme: jekyll-theme-prologue`となっており、このgithub actionsでビルドが失敗し、デプロイすることができません。そこで`theme: jekyll-theme-prologue`を`remote_theme: chrisbobbe/jekyll-theme-prologue`とする必要があります。

次にこれまで作成した記事(_post/以下にあるmarkdownファイル)を先ほどローカル環境で動作確認できたリポジトリへ移動させ、完成したリポジトリの中身を自分の<アカウント>.github.ioプロジェクトに全コピーします。（他にいいやり方ありそう）
    cd jekyll-theme-prologue
    cp -r * ../<アカウント名>.github.io
    git add . 
    git commit -m "add new theme"
    git push

これでgithubのgithub actionsのページで上手くビルドが通って、デプロイされた場合、作成したページのテーマが変更されていることがわかります。

## 終わりに
今回はテーマの変更方法についてまとめました。以外に大変でwordpressは簡単にテーマ変えられてすごいと思いました。（小並感）
次回はページの体裁を整える方法についてまとめたいと思います。それでは!