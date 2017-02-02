+++
date = "2015-05-07T19:56:31+09:00"
title = "test1"
draft = true
+++

# hugoでブログをやってみる

ブログをやってみようと思った時に、ここはRuby書いてる人っぽくjekyllでやってみるか！って思って調べてたら、もっと良さそうなものを見つけた。gitでリポジトリをプッシュするだけで簡単にブログ記事をあげられる＆記事の生成がめっちゃ早いということで評判が良かったので、[hugo](http://gohugo.io/)を使ってみることにしました。そして、ドハマりしたのでメモ。

## hugoの魅力

### 1. とにかく記事作成が楽

最終的にですが、ターミナルから以下の手順だけでGithub pagesにてブログが更新できます。

```terminal
$cd ~/blog
#hugoによって生成されたディレクトリまで移動
$hugo new post/hugahoge.md
#新規マークダウンファイルの作成
$ ./deploy.sh
#色々なコマンドの入ったシェルスクリプトの実行(コピペで手に入る)
$ git push origin master
#hugoによって生成されたディレクトリのリポジトリをgithub pagesのリモートにプッシュ(これはホントはやらなくて良い手順のハズ・・・・)
```

### 2. &ndash;watchコマンドでオートリロード!!</h3>

hugoでは、以下のコマンドで``localhost:1313``からプレビューができます。この時、``--watch``コマンドを利用することでmdファイルを更新する度にブラウザ側のプレビューも自動で更新されます。

```terminal
#hugoのルート・ディレクトリから・・・
$hugo server --watch -t hugo-zen
#--watchコマンド！
```

これがかなり便利です。いちいちcommand + r する手間が省けるのが素晴らしい。デュアルディスプレイとか[window magnet](https://itunes.apple.com/jp/app/window-magnet/id441258766?mt=12)とかで捗ります。

### 3.Markdown記法で気軽に書いて更新できる

これはjekyllなどでもそうですが、mdで書けるのは非常に楽です。普段からmdを書いているのもありますが、もう正直色をつけたり文字の大きさをいちいち変えたり「できる」というだけでまどろっこしいので。

### 4.記事の生成が早い

これは多くの人が言及しているので割愛。jekyllにはすごくお世話になっているのですが正直生成でストレスを感じたことはありません。上記のオートリロードが無いくらいですかね。

## インストール ~ テーマの適用

### インストール

とっても簡単。homebrewユーザーなら、以下のコマンドで。

```terminal
$cd 
#ホームディレクトリに移動
$brew install hugo
#hugaじゃないよ
```

続いて、以下のコマンドで新たなhugoプロジェクトを作成。

```terminal
$hugo new site &lt;your_site_name&gt;
#&lt;&gt;の部分は任意の名前を入れてね！
$cd &lt;your_site_name&gt;
#プロジェクトのルート・ディレクトリに移動しておきましょう
```

### テーマの適用

このままビルドしても記事を作成することはできるのですが、最初からある程度デザインができている方が楽です。というわけで、テーマを適用しましょう。まずは以下のコマンドでテーマを利用できるようにします。

```terminal
$git clone --recursive https://github.com/spf13/hugoThemes.git themes
#全てのテーマをダウンロード
```

今は全てのテーマをダウンロードしましたが、あとで利用するもの以外は削除してしまって構いません。

ところで、hugoはrailsなどと同じようにローカルでサーバーを立ち上げてプレビューすることができます。テーマは、その際にオプションで選択できます。

### 記事の作成

次に、試しに記事を作ってみます。

```terminal
hugo new post/hoge.md
#content/post/hoge.md が作成されます
```

生成されたmdファイルを適当に編集して、プレビューしてみましょう。以下のコマンドを打ちます。

```terminal
$hugo server -t 使用したいテーマ名 --watch
#テーマを適用しつつ、プレビューを起動。例えば以下のように・・・
$hugo server -t simple-a --watch
```

使用したいテーマ名の部分には、themesというディレクトリに入っているテーマの名前を入れます。うまく動かないものもありますが、とりあえず良さそうなものがないか試してみましょう。

以下のように表示されれば成功です。(と思ったら画像がうまく表示できない・・・)

<img src="images/001.jpg" alt="purehugo" />


## github pagesで公開

ここが一番詰まりました。「サーバー立ち上げたらテーマが適用されるのね。ほう、publicディレクトリができてそこに静的ファイルが生成されるとな？」とまでは良かったのですが、そもそもgithub pagesを使ったことがなかったのでその仕組みを知るのに一苦労。そして、いい感じのurlで表示できるようになるまでにまた一苦労。

基本的には、以下のhugoの公式docを読めばなんとかなるっぽいですが。

[Github Pagesへのセットアップ](http://gohugo.io/tutorials/github-pages-blog/)

よくわからなかったので、いろんな記事を参考に自分なりにやりました。これから紹介する方法は不完全ですので、完全版を教えていただけますと大変助かります(汗

### リポジトリを2つ作成

まずはgithub上で、リモートリポジトリを2つ作ります。1つは名前はなんでも大丈夫です。もう一つは公開用なのでgithub pagesの規約どおりに作ります。ここでは前者から

hogehuga

username.github.io

とします。

2つのリモートリポジトリが作れたら、次はhugoプロジェクトのルートディレクトリでローカルリポジトリを作り、先ほど作ったhogehugaの方にaddします。すでにプレビューをしているなら、ルートディレクトリ下に``public``フォルダができていますが、こちらは*消しておく必要があります。*

```terminal
$cd ~/blog
#プロジェクトのルート・ディレクトリに移動
$rm -rf public
#publicフォルダを削除
$git init
#gitコマンドでローカルリポジトリを作成
$git remote add origin https://github.com/&lt;gitのuser名&gt;/hogehuga.git
$git add .
#カレントディレクトリ以下を全てadd
$git commit -m &quot;first commit&quot;
#コミット
$git push origin master
#プッシュ
```

続いてGithub Pagesの表示で利用するリポジトリのpublicフォルダをhogehugaのサブモジュールとして追加します。なので、もう一度publicフォルダを作り直します。そのために、ビルドのコマンドを打ちます。ここでは、``hugo -t テンプレート名``とすると再びpublicフォルダを作成できます。

```terminal
$hugo -t &lt;テンプレート名&gt;
#publicフォルダに静的ファイルを生成
$git submodule add git@github.com:&lt;githubのユーザー名&gt;/&lt;githubのユーザー名&gt;.github.io.git public
#サブモジュールとしてpublicフォルダを追加


gitのサブモジュールっていうのはあくまで本体の一部のディレクトリを別のリポジトリで管理するものだと思ってましたが、hugoのページを読んでいるとどうも本家の方を更新することで本家のサブモジュールであるpublicも更新されて結果が反映される、みたいなノリなんですよね。よくわからない。。

ここまで来たら、プロジェクトのルート・ディレクトリに以下の内容のシェルスクリプト``deploy.sh``を作成します。途中記事をビルドする``hugo``の後に、 ``-t``オプションでテーマを指定することを忘れないでください。

```terminal
#deploy.shの中身
#!/bin/bash

echo -e &quot;\033[0;32mDeploying updates to GitHub...\033[0m&quot;

# Build the project. 
hugo # if using a theme, replace by `hugo -t &lt;yourtheme&gt;`

#↑ここを変更しましょう！！

# Go To Public folder
cd public
# Add changes to git.
git add -A

# Commit changes.
msg=&quot;rebuilding site `date`&quot;
if [ $# -eq 1 ]
  then msg=&quot;$1&quot;
fi
git commit -m &quot;$msg&quot;

# Push source and build repos.
git push origin master

# Come Back
cd ..
```

あとは冒頭で示した通り、``deploy.sh``を実行し、本体をプッシュすることでhugoのプロジェクトが更新されます。

```terminal
#hugoプロジェクトのルートディレクトリから・・・
$./deploy.sh
#deploy.shの実行
$git push origin master
#本体もプッシュする
```

いよいよ、Github Pagesにアクセスしてみましょう。先ほど作成したリポジトリの名前がそのままurlになっていますので、``gitのusername.github.io``というurlでいけるはずです。

無事、hugoのブログが表示されたでしょうか。

## 感想

本当ならddploy.shを実行するだけでいけるはず？また、画像の表示がうまくいかない、カテゴリーやタグ付けのやり方がわからないなど、まだやることはいっぱいですが、とりあえず楽にmdで書けるブログが手に入ったのは非常に良かったです。ちょいちょいカスタマイズしていきます。

## 謝辞

本ブログのテーマはrakuishi様の[hugo-zen](https://github.com/rakuishi/hugo-zen)をほんの少しカスタマイズして利用しています。どうもありがとうございます！！

