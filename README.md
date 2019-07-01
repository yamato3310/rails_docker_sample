# railsでdockerを使うときのテンプレート
## mysqlを使うときの手順
- docker-compose run web rails new . --force --database=mysql --skip-bundle
- database.ymlを以下のように変更
```
default: &default
  adapter: mysql2
  encoding: utf8
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password: password # docker-compose.ymlのMYSQL_ROOT_PASSWORD
  host: db # docker-compose.ymlのservice名
```
- docker-compose build
- docker-compose up -d
- docker-compose run web rails db:create

## 参考にしたサイト(ほとんど同じ)
- https://qiita.com/azul915/items/5b7063cbc80192343fc0

## vscode remote containersを使う場合
- クローンしたフォルダーを開きなおす
- 左下の青いボタンをクリック
- Remote-Containers Open Folder in Containerをクリック
- git cloneしたdocker-compose.ymlがあるフォルダーを指定
- From docker-composeをクリック
- webを選択
- buildが終わったらいったんローカルのファイルに戻る
- .devcontainer.jsonができているので"workspaceFolder": "/"を"/app_name"に変更する
