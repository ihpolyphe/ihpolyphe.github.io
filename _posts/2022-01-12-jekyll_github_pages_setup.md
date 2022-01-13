---
layout: post
title:  "github pagesでjekyllを使ったwebページ作成"
date:   2022-01-12 +0900
categories: jekyll 
---

## github pagesでjekyllを使ってwebページを作成するまでの手順
無料でブログを作成したい方にとってgithub pagesはとても魅力的です。xfreeなどの無料サーバーでwordpressを使いつつ運営することも可能ですが、個人的にgithub pagesを使ってみたいという気持ちがあったので使用しました。

github pagesを使ってwebページを作成するまでの流れは以下です。
1. gitインストール
2. Rubyインストール
3. jekyllインストール
4. githubアカウント作成
5. github pages用リポジトリの作成
6. jekyllプロジェクト作成
7. 記事を作成

かなりやることは多いです。特にgitの知識がないと苦労するかもしれません。（私がそうでした、、）ただgitの勉強にもなるので初心者の方はがんばってみてください。
ページ作成までの手順を網羅しておりますが、その分各項目の説明は薄いです。自分が環境構築時に参考にさせていただいたサイト様を記載していますので、そちらを参考にしてください。
なお開発環境はwindowsです。


### 1 gitのインストール
windowsの場合gitは公式ホームページからexeファイルをダウンロードします。
[https://git-for-windows.github.io/](https://git-for-windows.github.io/)
ダウンロードしたら.exeファイルを開き、インストールまで進みます。基本`next`でokです。

gitのインストールが完了したら、git bashと呼ばれるターミナルが開かれますので、他のソフトはここからインストールしました。（もちろんコマンドプロンプトでも問題ないと思います）
詳しいgitのインストール方法は[こちら](https://prog-8.com/docs/git-env-win)を参考にしました。


### 2 Rubyのインストール
Jekyll（ジキル）は静的サイトの生成を行うための、Rubyのパッケージです。よってRubyをインストールしないとjekyllも使うことができないということですね。（numpyを使うためにはpythonを入れないといけないみたいな）

Rubyのインストールも、windowsの場合gitと同様、exeファイルを公式ホームページからダウンロードします。
[https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/)

私は[ Ruby+Devkit 3.0.3-1 (x64) ](https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-3.0.3-1/rubyinstaller-devkit-3.0.3-1-x64.exe)をダウンロードして動作環境に問題がないことを確認しています。

exeファイルがダウンロード完了したら開き、インストールまで進みます。（詳しいインストール方法は[こちら](https://prog-8.com/docs/ruby-env-win)）
完了したら、git bashで以下のコマンドで、Rubyのバージョンが記載されるようになったらインストール完了です。

    ruby -v

### 3 jekyllのインストール
さて、ここまで来たら、jekyllをインストールします。
インストールは簡単で、git bashから以下のコマンドでインストールします。

    gem install jekyll bundler
インストールが成功すると以下のコマンドでバージョンチェックができます。

    jekyll -v

### 4 githubアカウントを作成する。
次にgithub pagesを利用するためにgithubアカウントを作成します。
[https://github.co.jp/](https://github.co.jp/)ここからサインアップをしてアカウントを作成しましょう。すでにアカウントを所持している方はサインインです。

### 5 github pages用リポジトリの作成
アカウントが作成できたら、github pages用のリポジトリを作成します。
以下の画像のようにリポジトリ作成画面から`<アカウント名>.github.io`のリポジトリを作成します。
リポジトリはよほどのことがない限りpublicで良いでしょう。

リポジトリを作成したらローカル環境にクローンする。ページのURLをコピーして、git bashにて以下のコマンドでクローンする。
    
    git clone <コピーしたリポジトリのURL>

これでローカル環境にリポジトリを落とすことができました。次のjekyllプロジェクトの作成でwebページを作成していきます。

### 6 jekyllプロジェクト作成
ようやくwebページの作成を行うことができるようになりました。
まずはjekyllプロジェクトを以下のコマンドで作成します。
    
    jekyll new test_project

こうすることでwebページを作成するための様々なファイルが生成されます。
次にプロジェクトをスタートさせます。
    
    bundle exec jekyll serve

成功したら、以下のコマンドでローカル環境でサイトの中身を確認することができます。
    
    jekyll s

私の場合このコマンドを打った際に``require': cannot load such file -- webrick (LoadError)`エラーで動きませんでした。
その場合以下のコマンドを入力します。

    bundle add webrick

こうすることで`jekyll s`でローカル環境でサイトが確認できるので、[ http://127.0.0.1:4000/]( http://127.0.0.1:4000/)から見てみます。サイトが立ち上がっていることがわかります。

こうなればあとはgithubにpushするだけです。
`test`で作成したプロジェクトを先ほどcloneした`<アカウント名>.github.io`へ移しましょう。
    
    cd test/
    git mv -r * ../<アカウント名>.github.io
    cd ../ && cd <アカウント名>.github.io
    git add .
    git commit -m "add jekyll project"
    git push

以上のコマンドが上手くいった場合、先ほど作成したgithubのアカウントのページでプロジェクトが反映されていることがわかります。

### 7 記事を作成
最後に自分で記事を作成する方法を説明します。
まずはjekyllプロジェクトの`/_post`にmarkdownファイルを作成します。
    
    cd <githubアカウント>.github.io/_post
    vim yyyy/mm/dd-how-to-make-article-of-jekyll.markdown

上記はコマンドで記載するためvimを使っていますが、基本は[visual studio code](https://azure.microsoft.com/ja-jp/products/visual-studio-code/)などのエディタで作成するのが良いです。

中身は以下のようにマークダウン方式で記載していきます。書き方がわからない方は[こちら](https://qiita.com/tbpgr/items/989c6badefff69377da7)のページを参照ください。

```
---
layout: post
title:  "github pagesでjekyllを使ったwebページ作成"
date:   2022-01-12 +0900
categories: jekyll 
---

# markdown方式で記事を作成
```
この方法でページ作成が完了したら、後は先ほどと同様githubにpushします。

    cd <アカウント名>.github.io
    git add <ファイル名>
    git commit -m "add new article"
    git push

この作業が完了したら、先ほど作成したmarkdownファイルがgithubにアップロードされていることを確認し、５分ほど待つと、以下のURLに作成した記事が追加されています。

- https://<githubアカウント名>.github.io

## 終わりに
今回はgithub pagesでjekyllを使ったページの作成方法についてまとめました。
今後はマークダウンのtipsであったり、編集方法、プラグインなどについても勉強し、こちらのサイトにページを作っていこうと思います。
ありがとうございました。