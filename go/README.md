# go

## 概要

[Connect](https://connect.build/docs/go/getting-started/)を使った gRPC サーバのサンプル実装

### 実行コマンドなど

```bash

# init
cd src
go mod init example

# install modules
go install github.com/bufbuild/buf/cmd/buf@latest
go install github.com/fullstorydev/grpcurl/cmd/grpcurl@latest
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
go install github.com/bufbuild/connect-go/cmd/protoc-gen-connect-go@latest

# generate proto with buf
buf lint
buf generate
```
