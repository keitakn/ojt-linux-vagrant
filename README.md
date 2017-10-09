# ojt-linux-vagrant
[web-developer-ojt](https://github.com/keita-nishimoto/web-developer-ojt) で利用するLinuxの練習用リポジトリ

## 注意

この手順はMacOSを利用している事が前提となります。

## 利用の為の事前準備

いくつか事前にインストールが必要な物があります。

インストール済の場合はスキップして下さい。

### [Homebrew](https://brew.sh/index_ja.html)

Mac用のパッケージ管理を行う為のツールです。

[公式サイト](https://brew.sh/index_ja.html) に載っている手順を参考にインストールして下さい。

### [VirtualBox](https://www.virtualbox.org/)

既存のOS上に異なるOSをインストール出来るツールです。

VirtualBoxがインストールされているOSをホストOS、VirtualBox内にインストールされるOSをゲストOSと呼びます。

[公式サイト](https://www.virtualbox.org/) からインストーラーをダウンロードしてインストールして下さい。

### [Vagrant](https://www.vagrantup.com)

開発環境の構築と共有を簡単に行うためのツールです。

Vagrant を利用すると VirtualBox上に簡単にゲストOSをインストールする事が出来ます。

[公式サイト](https://www.vagrantup.com) よりインストーラーをダウンロードしてインストールして下さい。

### Vagrant Pluginのインストール

Vagrantプラグインのインストールを行います。 今回必須なのは、`vagrant-vbguest` です。

以下のコマンドを実行しインストールを行います。

```bash
vagrant plugin install vagrant-vbguest
```

その他に入れておいたほうがいい物としては [sahara](https://github.com/jedi4ever/sahara) があります。

これは サンドボックスモードを有効にするプラグインで操作等を間違えた時にロールバックが簡単に出来ます。

以下のコマンドでインストールしておきましょう。

```bash
vagrant plugin install sahara
```

### [Ansible](https://www.ansible.com/)

構成管理ツールの1つで、サーバの設定内容をymlファイルで管理出来ます。

今すぐは使いませんが後のlessonで利用するので、インストールしておきましょう。

以下のコマンドでHomebrewを最新状態にします。

```bash
brew update
```

brewコマンドでansibleを指定してインストールします。

```bash
brew install ansible
```

## 利用方法

本リポジトリの直下に移動して以下のコマンドを実行して下さい。

```bash
vagrant up
```

これを実行するとAmazon Linuxの環境がVirtualBox上に構築されます。

環境構築完了後、以下のコマンドを打つとVirtualBoxが立ち上がっていることが確認出来ます。

```bash
vagrant status
```

```text
Current machine states:

default                   running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
```

## サーバにログインを行う

構築したサーバにログインする為にSSHという方法で接続を行います。

SSHとは安全にリモート上のコンピュータと通信する為の手段です。

※ この内容に関してはセキュリティのレッスンで詳しく解説します。

かなり詳しく解説してくれている記事を見つけたので載せておきます。

https://qiita.com/tag1216/items/5d06bad7468f731f590e

`vagrant ssh` を実行するとサーバ内にログインが出来ます。

下記のような画面が出ればログインに成功しています。

```text
Last login: Mon Oct  9 13:43:51 2017 from 10.0.2.2

       __|  __|_  )
       _|  (     /   Amazon Linux AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-ami/2017.03-release-notes/
Amazon Linux version 2017.09 is available.
[vagrant@localhost ~]$
```

ログアウトする際は `exit` とターミナルに打ち込むとログアウト出来ます。

ちなみに vagrant で構築したサーバは `vagrant` というユーザーが自動で作成されています。

`sudo su` を実行するとrootユーザーになれます。

## その他の操作方法

[公式ドキュメント](https://www.vagrantup.com/docs/cli/) を参照して下さい。

サーバを停止する為の `vagrant halt` や 現在の状態を確認する `vagrant status` は良く利用します。

個人的な方法ですが、作業を終える際は `vagrant suspend` でサーバを一時停止して `vagrant resume` で再開すると普通に halt → up するより早いのでオススメです。

