# syntax=docker/dockerfile:1

# グローバル変数として使うためここに定義
ARG LOG_DIR=/tmp/log/app

#############################################
## build
#############################################
FROM golang:1.19-bullseye as build

ARG LOG_DIR

WORKDIR /app

COPY ./src ./
RUN go mod download && \
    go build -v -o /app/bin ./cmd/server/main.go

RUN mkdir -p ${LOG_DIR}

#############################################
## Development
#############################################
FROM golang:1.19-bullseye as development

ARG LOG_DIR

# USER作成
ARG UID=1000
ARG GID=1000
RUN groupadd -g ${GID} nonroot && \
    useradd -l -g ${GID} -u ${UID} -m -s /bin/bash nonroot

WORKDIR /app

COPY --from=build --chown=nonroot:nonroot /app ./
COPY --from=build --chown=nonroot:nonroot ${LOG_DIR} ${LOG_DIR}
COPY --from=build /usr/local/bin /usr/local/bin
COPY --from=build /go /go

# カバレッジ出力先作成
RUN mkdir -p coverage

USER nonroot:nonroot

EXPOSE 8080

#############################################
## Production
#############################################
FROM gcr.io/distroless/base-debian11 as production

ARG LOG_DIR

WORKDIR /app

# USERはdistrolessで定義しているnonrootを使う
COPY --from=build --chown=nonroot:nonroot ${LOG_DIR} ${LOG_DIR}
COPY --from=build /usr/local/bin /usr/local/bin
COPY --from=build /go /go

USER nonroot:nonroot

EXPOSE 8080