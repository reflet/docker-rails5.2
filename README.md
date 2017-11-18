# Ruby2.3 + MySQL + Redis
docker-composeコマンドを使っての操作方法を記載します。

## コンテナ起動
下記のコマンドにてコンテナを起動します。

```
$ git clone git@github.com:reflet/server-ruby2.3-mysql-redis.git .
$ docker-compose build
$ docker-compose up -d
```

## bundleインストール
bundle installコマンドにて、railsをインストールする。

```
$ docker exec ruby bundle install
```

## railsアプリ作成
下記コマンドで、新規アプリを作成します。

```
$ docker exec ruby bundle exec rails new . --force --database=mysql
```

※ bundle installを実行したくないときは「--skip-bundle」オプションを追加する

一部Gemfileを修正する

```
$ docker exec -it ruby bash
$ vim Gemfile

　　修正前)
　　# gem 'therubyracer', platforms: :ruby

　　　　　　　　　　↓↓↓↓↓↓
　　修正後)
　　gem 'therubyracer', platforms: :ruby

$ exit
```

bundle updateを実行

```
$ docker exec ruby bundle update
```

## サーバ起動
下記のコマンドにてサーバを3000ポートで起動する。

```
$ docker exec ruby bundle exec rails s -d -p 3000 -b '0.0.0.0'
```

dockerで3000ポートを80ポートに接続しているので、ブラウザで下記URLにアクセスしてみる。

```
http://192.168.33.10/
```

※ ここ記事では、vagrantで192.168.33.10の仮想環境を使用しています。

※ 192.168.33.10のIPの部分は、各環境に合わせて変更ください。

