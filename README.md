# Quoridorn monorepo

## What is this

Hilltopさん作のQuoridorn Mark2およびQuoridorn-serverをmonorepo化する試み。

- `npx lerna run build` でサーバー、クライアント両方をビルドし、 
- `npx lerna run test` でテストを実行する

が理想。

## Requirements

- git
- node.js(nvmやnvsで入れるのが好ましいと思う、ここではLTSの12系を使用)
- docker
- docker-compose

**※ このリポジトリのdocker-compose.ymlはあくまでローカル環境での利用のみを想定しております。そのままでの外部公開は絶対にしないでください。**

## Setup

1. Githubからsubmodule含めてチェックアウトする。 `git clone --recursive https://github.com/hirokinko/quoridorn-monorepo`
1. 各種設定の *.yaml.example、.env.exampleから *.yaml と .env を作成する。 `VUE_APP_BASE_URL` はブランクにする。
1. packages/client に移動し、 `npm run build` を実行。
1. プロジェクトホームに戻り、 `docker-compose up -d` で `minio` 、 `mongodb` 、 `nginx` を起動。 `nginx` にはビルドしたクライアントがデプロイされている。
1. ブラウザから `http://localhost:9000` にアクセスし、 `/quoridorn` バケットを作成する。
1. packages/server に移動し、 `npm run server` を実行。
1. ブラウザから `http://localhost:8080` にアクセスし、動作を確認する。

## Bugs and TODO

- 最初の1回目のアクセスは必ず失敗する。ウォームアップが必要？
- 所々画面レイアウトが崩れる。
- 画像の取得に失敗する。
- minioを立ち上げたら `quoridorn` バケットを作るようにしたい。
