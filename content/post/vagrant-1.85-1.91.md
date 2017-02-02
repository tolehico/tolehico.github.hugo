+++
title = "vagrant環境のアップデート (1.8.6 -> 1.9.1)でエラーが発生"
date = "2017-02-02T20:02:35+09:00"
categories = [""]
tags = ["vagrant",""]
eyecatch = ""
slug = ""
draft = false
+++

## vagrantのアップデート後にエラー発生
(vagrantをアップデートして)[https://tolehico.github.io/post/vagrant-update/]起動したら、以下の際なエラーメッセージが出てしまった。


```terminal
tolehico-pc:vccw tolehico$ vagrant up
Vagrant failed to initialize at a very early stage:

The plugins failed to initialize correctly. This may be due to manual
modifications made within the Vagrant home directory. Vagrant can
attempt to automatically correct this issue by running:

  vagrant plugin repair

If Vagrant was recently updated, this error may be due to incompatible
versions of dependencies. To fix this problem please remove and re-install
all plugins. Vagrant can attempt to do this automatically by running:

  vagrant plugin expunge --reinstall

Error message given during initialization: Unable to resolve dependency: user requested 'vagrant-triggers (> 0)’
```

メッセージに従い、

``vagrant plugin repair``

を実行。すると、

```terminal
tolehico-pc:vccw tolehico$ vagrant plugin repair
Repairing currently installed plugins. This may take a few minutes...
Fetching: bundler-1.14.3.gem (100%)
Bundler and RubyGems.org are free for anyone to use, but maintaining them costs more than $25,000 USD every month. Help us cover those costs so that we can keep the gem ecosystem free for everyone: https://ruby.to/support-bundler
Fetching: vagrant-hostsupdater-1.0.2.gem (100%)
Fetching: vagrant-triggers-0.5.3.gem (100%)
Installed plugins successfully repaired!
```

これで修復できた様子。

最後に、

``vagrant up``

でゲストOSが起動できました。