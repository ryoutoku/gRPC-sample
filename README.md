# grpc-sample

## 概要

gRPC のサンプル実装を介して gRPC の理解を深める。

ついでに golang も。

## サンプル実行

```bash

# serverの起動
docker compose up

#############################
# ターミナルからgo/cmd/server/main.go の処理に対してリクエストを投げるコマンド
# localhostではなく127.0.0.1を指定する必要がある
curl \
--data '{"name": "Jane"}' \
http://127.0.0.1:8080/greet.v1.GreetService/Greet

```
