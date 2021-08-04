# RESTful API
- フロントエンドとバックエンドを分けて開発
- laravelを使ってAPIサーバーを作成


## ルーティング
|  method |  URI  |  役割  |
| ---- | ---- | ---- |
|  GET  |  api/todos  |　タスク一覧の表示　|
|  POST  | api/todos  |　タスクの追加|
|  DELETE  | api/todos/{todo}  |　タスクの削除|
|  PATCH  | api/todos/{todo}  |　チェックボックスの切り替え|

## 実行方法
```

// プロジェクトへ移動
$ cd restapi

// Composer依存関係のインストール
$ docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v $(pwd):/opt \
    -w /opt \
    laravelsail/php80-composer:latest \
    composer install --ignore-platform-reqs
 
// .envの作成
$ cp .env.example .env

// 環境変数の上書き
$ php artisan sail:install

// エイリアスの設定
$ alias sail='bash vendor/bin/sail'

// アプリケーションキーの設定
$ php artisan key:generate

// sailを立ち上げる
$ sail up -d

// migrateの実行
$ sail artisan migrate

// 停止する場合
$ sail down

```

# 以下自分用

## Modelとマイグレーションファイルの作成
~~~
php artisan make:model Todo --migration
~~~

## Controllerの作成
~~~
# 今回はapiを作成するので--apiをつける
php artisan make:controller TodoController --api
~~~

## ルーティングの設定
routes/api.php
~~~
# 使わないものはexceptで指定
Route::resource('todos', TodoController::class, ['except' => ['show', 'edit']]);
~~~