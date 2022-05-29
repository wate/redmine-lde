Redmineローカル開発(デバッグ)環境
======================

必要なもの
-------------------

このローカル開発環境を利用するには、以下のアプリケーションが必要になります。

* [Vagrant](https://www.vagrantup.com/)
* [VirtualBox](https://www.virtualbox.org/)
* [Visual Studio Code](https://code.visualstudio.com/)
  * [Ruby](https://marketplace.visualstudio.com/items?itemName=rebornix.Ruby)


利用方法
-------------------

以下に記載されているコマンドの`${LDE_ROOT}`と`${REDMINE_ROOT}`は

* `${LDE_ROOT}`：本リポジトリをcloneした直下のディレクトリを指しています。
* `${REDMINE_ROOT}`： cloneしたRedmineのルートディレクトリを指しています。

### 1. 本リポジトリのコード一式を取得します

以下のコマンドを実行し、本リポジトリのコード一式を取得します

```
git clone https://github.com/wate/redmine-lde.git
```

### 2. Redmineのソースコードを取得します

以下のコマンドを実行しRedmineのソースコードを取得します。

```
cd ${LDE_ROOT}
git clone https://github.com/redmine/redmine.git
```

#### Redmineバージョンの切り替方法

以下のコマンドを実行し対応するバージョンのブランチに切り替えます。  
※以下のコマンドでは`4.2`に切り替えを行っています。

```
cd ${REDMINE_ROOT}
git checkout 4.2-stable
```

### 3. 仮想マシンの作成/起動します

以下のコマンドを実行し、ローカル開発(デバッグ)環境用の仮想マシンを作成します。

```
cd ${LDE_ROOT}
vagrant up
```

※初回のみマシンイメージのダウンロードに行うため、仮想マシンの作成に時間がかかります。  
(ダウンロードに必要な時間はご利用のネットワーク環境に依存します)

### 4. デバッガーを開始します。

Visual Studio Codeのデバッガを起動します。  

※デバッガに`Listen for rdebug-ide`が選択されていることを確認してください。

### 5. ステップ実行する

任意の止めたい場所にブレイクポイントを設定し、
以下のURLにアクセスし該当箇所が通るように操作します。

http://localhost:3000/

ブレイクポイントで処理が止まり、変数の確認やコードの実行、ステップ実行が可能になります。

デバッガの利用方法は以下のURLなどを参考にしてください。

[VSCodeで始めるデバッガ](https://www.bravesoft.co.jp/blog/archives/14082)

パッチファイルの作成方法
-------------------

### 変更内容のパッチファイルの作成する

変更した内容をパッチファイルとして出力したい場合は、以下のコマンドを実行します。

```
cd ${REDMINE_ROOT}
git diff > change_files.patch
```

ローカル開発環境の情報
-----------------------

### 仮想マシン上のRedmine設置先

仮想マシン内のRedmineの設置先は以下のディレクトリです。

```
/vagrant/redmine
```

### データベース情報

データベースへの接続情報は以下のとおりです。

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