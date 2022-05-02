redmine-lde
======================

必要なもの
-------------------

* [Vagrant](https://www.vagrantup.com/)
* [VirtualBox](https://www.virtualbox.org/)
* [Visual Studio Code](https://code.visualstudio.com/)
  * [Ruby](https://marketplace.visualstudio.com/items?itemName=rebornix.Ruby)


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

### 2. 仮想マシンの作成/起動します

```
cd ${LDE_ROOT}
vagrant up
```

### 3. rdebug-ideを使ってRedmineを起動します

以下のコマンドを実行し、仮想マシンにログインします

```
vagrant ssh
```

仮想マシンにログインし以下のコマンドを実行します。

```
launch_rdebug-ide
```

または、以下のコマンドを実行します。

```
cd /vagrant/redmine
bundle exec rdebug-ide --host 0.0.0.0 --port 1234 -- bin/rails server -b 0.0.0.0 -p 3000 -e development 
```

### 4. デバッガーを開始します。

以下のURLを参考にVSCodeのデバッガを起動します。  

※デバッガに`Listen for rdebug-ide`が選択されていることを確認してください。

### 5. ステップ実行する

任意の止めたい場所にブレイクポイントを設定し、
以下のURLにアクセスし該当箇所が通るように操作を行います。

http://localhost:3000/

ブレイクポイントで処理が止まり、変数の確認やコードの実行、ステップ実行が可能になります。

デバッガの利用方法は以下のURL等を参考にしてください。

[VSCodeで始めるデバッガ](https://www.bravesoft.co.jp/blog/archives/14082)

パッチファイルの作成方法
-------------------

### 変更内容のパッチファイルの作成する

変更を行った内容をパッチファイルとして出力したい場合は、以下のコマンドを実行します。

```
cd ${REDMINE_ROOT}
git diff > change_files.patch
```

ローカル開発環境の情報
-----------------------

### データベース情報

データベースへの接続情報は以下の通りです

* ホスト名：:`localhost`
* データベース名：`redmine`
* ユーザー名：`redmine_user`
* パスワード：`redmine_password`
* ポート：`3306`

#### 補足事項

Vagrantの[ポートフォワーディング機能](https://www.vagrantup.com/docs/networking/forwarded_ports)を設定を行っているため、
ホストマシンから上記の接続情報を利用し仮想マシンのデータベースに接続できます。

### メール送信のテスト

メールの送信テストを可能にするために[MailHog][]をインストールしています。  
[MailHog][]の画面には以下のURLよりアクセスできます。

http://localhost:8025/

[MailHog]: https://github.com/mailhog/MailHog