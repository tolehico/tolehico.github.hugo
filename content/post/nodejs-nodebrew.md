+++
date = "2016-05-19T10:47:33+09:00"
draft = true
categories = ["env"]
tags = ["nodejs","nodebrew"]
title = "node.jsをnodebrewで管理してみた"
+++

## html-css-js prettifyを導入しようとしたら、Node.jsのエラーが出た。
SublimeText3を導入するにあたって、整形プラグインのhtml-css-js prettifyを入れようとしました。
そしたら以下の様なメッセージが出てしまい。

```terminal
Node.js was not found in the default path. Please specify the location.
```

つまり、Node.jsが指定されたパスにないですよ！といった内容ですね。
そういえばNode.jsも入れてなかったかと気づきまして。

なのでNode.jsを入れてみました。

## Node.jsのバージョン管理nodebrewの導入
プロジェクトごとにバージョン変更したりしないといけないので、バージョン管理可能な環境にしておくことが望ましいです。
今回、Node.jsのバージョン管理にはnodebrewを仕様してみました。
お馴染みのHomebrewを使用してのインストールは、EICapitanを使用していると上手くいかないようなので、ターミナルにcurlコマンドを叩いて直にインストールしました。

```terminal
$ curl -L git.io/nodebrew | perl - setup
```

## HTML-CSS-JS PrettifyにNode.jsのパスを通す
パスの指定は以下のとおり。
Preferences > Package Settings > HTML/CSS/JS Prettify > set node path
の8行目を、

```terminal
"osx": "$HOME/.nodebrew/current/bin/node"
```

に変更。



