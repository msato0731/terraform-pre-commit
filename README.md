# terraform用のpre-commitを複数リポジトリで利用する方法

## グローバル設定

各リポジトリでpre-commitを自動有効化するコマンド。

このコマンドを実行することで、各リポジトリで`pre-commit install`が不要になる。

以下をテンプレートリポジトリ(本リポジトリを指す)が存在するディレクトリで実行。

```bash
git config --global init.templateDir ~/.git-template
pre-commit init-templatedir ~/.git-template
```

https://pre-commit.com/#automatically-enabling-pre-commit-on-repositories

## Terraformリポジトリ側作業

pre-commit設定を一元管理するため、Terraformリポジトリ側にテンプレートリポジトリのシンボリックリンクを作成する。

```bash
cd <Terraformリポジトリのディレクトリ>
ln -s <テンプレートリポジトリのディレクトリ>/terraform-pre-commit/.pre-commit-config.yaml ./.pre-commit-config.yaml
```

Terraformリポジトリ側では、.gitignoreで`.pre-commit-config.yaml`シンボリックリンクを追跡対象外とする。(各ユーザー毎に異なるため、差分が発生する)

```bash
# gitignore
pre-commit-config.yaml
```
