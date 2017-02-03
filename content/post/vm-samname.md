+++
draft = false
slug = ""
eyecatch = ""
tags = ["vagrant","vccw","vituralbox"]
categories = [""]
title = "同じ名前のVMがあって起動できなくなったら"
date = "2017-02-03T11:45:54+09:00"

+++

## 同名VMによるエラー発生

vccwをいじっていたら、box周りでエラー発生。

```terminal
A VirtualBox machine with the name 'hogehoge' already exists.
Please use another name or delete the machine with the existing
name, and try again.
```

``$vagrant up`` でも起動しなくなった。
どうやら同名のvmがあったらしい。

``$ vagrant global-status``
を実行すると、

```terminal
id       name        provider   state    directory                                                
--------------------------------------------------------------------------------------------------
888332a  default     virtualbox saved    /Users/xxxx/MyVagrant/mycentos                       
019a2d6  wocker      virtualbox poweroff /Users/xxxx/Works/hogehoge_dev/wocker                 
e794b53  hogehoge.dev virtualbox poweroff /Users/xxxx/Works/hogehoge_dev/hogehoge-wordpress/vccw 
 
The above shows information about all known Vagrant environments
on this machine. This data is cached and may not be completely
up-to-date. To interact with any of the machines, you can go to
that directory and run Vagrant, or you can use the ID directly
with Vagrant commands from any directory. For example:
"vagrant destroy 1a2b3c4d"
```


一旦、

``$ vagrant destroy e794b53``
をしてみたものの、

再び``$vagrant up``をすると同じエラーが発生。

下記コマンドでVirtualBoxでどうなっているかを確認してみたところ、
``$ vboxmanage list vms`


```terminal
"Windows 10 x64" {64e2251c-b862-46ea-8be7-69b60230c0c5}
"default" {467bfeae-ae8b-4834-b45e-0da25c6d588e}
"wocker_wocker_1471583108367_38178" {e159b097-aa23-4774-976e-62f570555177}
"hogehoge.dev" {59bc58cd-6cea-42d3-a1f5-f38c679b1ce6}
```

"hogehoge.dev"がまだ残っている...??

普通にMacのGUIアプリのVirtualBoxを起動したところ、まだ存在していたので、
電源OFFをしてから除去。

最後に改めて、
``$vagrant up``

したところ、無事起動。

すこしハマったので、備忘録として記録。

