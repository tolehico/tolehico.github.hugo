+++
tags = ["vccw","vagrant","wordpress"]
slug = ""
draft = false
date = "2017-02-02T19:48:31+09:00"
eyecatch = ""
categories = [""]
title = "Vagrantのバージョンアップの方法"

+++


## vccwを導入しようとしたら、vagrantのエラーが出た
WordPressの開発をVVVでしようとしていたが、テーマ作成がメインになるので、VVVを辞めてvccwでの開発に変更してみた。

いつものようにboxファイルを落としてきて、``vagrant up``をしようとしたら、エラーになってしまった。

```terminal
tolehico-pc:vccw tolehico$ vagrant up
This Vagrant environment has specified that it requires the Vagrant
version to satisfy the following version requirements:

  >= 1.8.6

You are running Vagrant 1.8.5, which does not satisfy
these requirements. Please change your Vagrant version or update
the Vagrantfile to allow this Vagrant version. However, be warned
that if the Vagrantfile has specified another version, it probably has
good reason to do so, and changing that may cause the environment to
not function properly.
```

1.8.6にあげてね、というメッセージだ。

どうやらvagrantのバージョンが古かったらしい。dockerに浮気したりしていて久しぶりにVagrantを使ってみたがこんなに更新されていたとは…。

```terminal
tolehico-pc:vccw tolehico$ vagrant -v
Vagrant 1.8.5
```

自分の環境を確認すると、たしかに1.8.5だった。



## Vagrantのバージョンアップは、公式ホームページから最新版のファイルをダウンロード
僕はMacなので、[ここ](https://www.vagrantup.com/downloads.html)から単純に.dmgファイルをダウンロードして、インストール。

僕の環境はまさかの1.8.5だったが、最新版は1.9.1に上がっていた。
ダウンロードして再度確認すると、しっかりと1.9.1に。

```terminal
tolehico-pc:vccw tolehico$ vagrant -v
Vagrant 1.9.1
```


これで一件落着。



