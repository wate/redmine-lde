redmine-lde
======================

必要なもの
-------------------

* [Vagrant](https://www.vagrantup.com/)
* [VirtualBox](https://www.virtualbox.org/)
* [Visual Studio Code](https://code.visualstudio.com/)
  * [Ruby](https://marketplace.visualstudio.com/items?itemName=rebornix.Ruby)
  * [Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)


利用方法
-------------------

以下に記載されているコマンドの`${LDE_ROOT}`と`${REDMINE_ROOT}`は

* `${LDE_ROOT}`：本リポジトリをcloneした直下のディレクトリを表しています
* `${REDMINE_ROOT}`： cloneしたRedmineのルートディレクトリを表しています。


### 1. Redmineのソースコードを取得

```
cd ${LDE_ROOT}
git clone https://github.com/redmine/redmine.git
```

#### Redmineのバージョンを切り替える

以下のコマンドを実行し対応するバージョンのブランチに切り替えます。
※以下のコマンドでは`4.2`に切り替えを行っています

```
cd ${REDMINE_ROOT}
git checkout 4.2-stable
```

### 2. 仮想マシンの作成/起動

```
cd ${LDE_ROOT}
vagrant up
```

### 3. rdebug-ideを使ってRedmineを起動する

以下のコマンドを実行し、仮想マシンにログインします

```
vagrant ssh
```

仮想マシン内で以下のコマンドを実行しrdebug-ideを使ってRedmineを起動します

```
cd /vagrant/redmine
bundle exec rdebug-ide --host 0.0.0.0 --port 1234 -- bin/rails server -b 0.0.0.0 -p 3000 -e development 
```

### 4. デバッガーを開始します。


### 5. ステップ実行する

任意の止めたい場所にブレイクポイントを入れ、以下のURLにアクセスし、
該当箇所が通るようなコードを実行します。

http://localhost:3000/

ブレイクポイントで処理が止まり、変数の確認やコードの実行、ステップ実行が可能になります。

デバッガの利用方法は以下のURL等を参考にしてください。

[VSCodeで始めるデバッガ](https://www.bravesoft.co.jp/blog/archives/14082)

パッチファイルの作成方法
-------------------

### 変更内容のパッチファイルの作成する

```
cd ${REDMINE_ROOT}
git diff > change_files.patch
```

サーバー情報
-----------------------

### データベース情報

* データベース名：`redmine`
* ユーザー名：`redmine_user`
* パスワード：`redmine_password`

### データベース情報

http://localhost:8025/


参考URL
-----------------------

* [Ruby for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=rebornix.Ruby)
* [Debugger](https://github.com/rubyide/vscode-ruby/blob/main/docs/debugger.md)
