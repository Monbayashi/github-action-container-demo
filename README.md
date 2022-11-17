# GitHub Action Container Demo

Github Action ではDockerコンテナを利用できる。

## Job Container

containerキーワードを使って
Jobの実行環境を指定できる。

```yml
jobs:
  test:
    environment: testing
    runs-on: ubuntu-latest
    # job testに対しての実行環境
    container:
      image: node:16
```

## Service Container

Github上でDBなどのコンテナを作成できる。

利点: 使い捨てのDB(テスト用)などを作成。

```yml
jobs:
  test:
    environment: testing
    runs-on: ubuntu-latest
    # job testに対しての実行環境
    container:
      image: node:16
    env:
      MONGODB_CONNECTION_PROTOCOL: mongodb
      MONGODB_CLUSTER_ADDRESS: mongodb
      MONGODB_USERNAME: root
      MONGODB_PASSWORD: example
      PORT: 8080
    # Service Container
    services:
      mongodb:
        image: mongo
        env:
          MONGO_INITDB_ROOT_USERNAME: root
          MONGO_INITDB_ROOT_PASSWORD: example
```