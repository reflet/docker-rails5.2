## Ruby on Rails5.2環境
ローカル環境の構築について記載します。

　
 
### ■ 前提条件
ローカル環境に下記ソフトウェアをインストールしていること
* [Docker Toolbox](hhttp://docs.docker.jp/mac/step_one.html)

※ ちなみに、Dockerが使える環境であれば上記ツールに限定されません。

　
 
### ■ ファイルの配置
gitコマンドにてファイルを配置します。

```
$ mkdir -p ~/rails5.2 && cd ~/rails5.2
$ git clone git@github.com:reflet/docker-rails5.2.git .
```

　

### ■ コンテナ起動
下記コマンドでdockerコンテナを起動します。

```
$ docker-compose up -d --build
```

　
### マイグレーション
データベースにマイグレーションを実行したい場合は、下記のコマンドで実行できます。

```
$ docker-compose exec rails rake db:migrate
```

　

### 動作確認
ブラウザでアクセスしてみる。

```ｓｈ
192.168.99.100
```

　

### ruby on railsの各種操作
railsコマンドで操作できる各種コマンドを実行したい場合は、下記のように実行できます。

```
# Gemfileを変更した時のりライブラリ更新
$ docker-compose exec rails bundle update

# データベース作成
$ docker-compose exec rails rake db:create

# マイグレーション実行
$ docker-compose exec rails rake db:migrate

# アセットのプリコンパイルを行う
$ docker-compose exec rails rake assets:precompile
```

　

### MySQL情報
SequelProのような好きなツールでアクセスできます。

```
HOST: 192.168.99.100
PORT: 33306
USER: app
PASSWORD: development
```

　

### コンテナの停止
```
$ docker-compose stop
```

　

### コンテナの破棄
```
$ docker-compose down -v
```
