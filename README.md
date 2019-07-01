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
