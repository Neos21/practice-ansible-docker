# Practice Ansible Docker

Docker コンテナを対象に Ansible を実行する、Ansible のお試しキット。


## Information

`docker-compose` を使い、以下の3つの Docker コンテナを起動する。

- `ansible-server` : Ansible の実行環境となるコンテナ
- `target-1` : Ansible での操作対象となる CentOS コンテナ
- `target-2` : Ansible での捜査対象となる Debian コンテナ

`ansible-server` コンテナから `target-1` ・ `target-2` コンテナへの `ssh` 接続は、パスワードでの認証となる。パスワード文字列は `mypassword` (`Dockerfile` の `chpasswd` 部分に記載)。

Ansible で使用するファイルは以下のとおり。

- `./ansible/inventry-hosts.ini` : Ansible の操作対象となるホスト名を記した hosts ファイル
- `./ansible/playbook.yaml` : Ansible での処理内容を記載した Playbook ファイル。サンプルは `/tmp/ansible-docker-test.txt` ファイルを生成する処理とした


## How To Use

```sh
# Ansible コンテナと操作対象コンテナ2台をまとめて起動する
$ docker-compose up -d

# Ansible コンテナに接続する
$ docker exec -it ansible-server /bin/bash

# Ansible コンテナから Target 1 コンテナに SSH できるか確認する
$$ ssh target-1
# 初回のみ `yes` と回答する
# `root@target-1's password:` にパスワードを入力する

# Ansible コンテナから Target 2 コンテナに SSH できるか確認する
$$ ssh target-2
# 初回のみ `yes` と回答する
# `root@target-2's password:` にパスワードを入力する

# Ansible を実行する
$$ ansible-playbook -i ./ansible/inventry-hosts.ini ./ansible/playbook.yaml --ask-pass
# SSH パスワードを入力する

# 全てのコンテナを停止・破棄する
$ docker-compose rm --stop --force
```


## Author

[Neo](http://neo.s21.xrea.com/) ([@Neos21](https://twitter.com/Neos21))


## Links

- [Neo's World](http://neo.s21.xrea.com/)
- [Corredor](http://neos21.hatenablog.com/)
- [Murga](http://neos21.hatenablog.jp/)
- [El Mylar](http://neos21.hateblo.jp/)
- [Neo's GitHub Pages](https://neos21.github.io/)
- [GitHub - Neos21](https://github.com/Neos21/)
