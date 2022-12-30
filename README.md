# GraphQL Codegen

## 概要

`GraphQL`から`TypeScript`のソースコードを自動生成するための最小構成と、ゼロからこのリポジトリの構成を再現するまでの処理を紹介する。

## ファイル構成

```sh
.
├── README.md
├── codegen.ts # コード生成設定ファイル
├── generated # 生成されたコードが格納されるファイル
├── graphql.schema.json
├── operations # GraphQLのクエリ操作ファイル
├── package-lock.json
├── package.json
└── schema.graphql # GraphQLスキーマファイル
```

## 手順

### `npm`の初期化

`npm`の初期化。特に設定が必要なものはないので、`-y`オプションで設定する。

```sh
npm init -y
```

### パッケージのインストール

必要なパッケージをインストールする。

```sh
npm install graphql
npm install -D typescript
npm install -D @graphql-codegen/cli
```

### スキーマファイル

`GraphQL`のスキーマファイル。通常は`GraphQL`サーバーから出力できる。
今回はプロジェクトのルートディレクトリに`schema.graphql`というファイル名で作成する。

### クエリ操作ファイル

アプリケーション内で実際に呼び出すときに利用するクエリを記述したファイル。
今回は`operations/query.graphql`に作成する。

### 出力用のディレクトリ

コード生成したファイルの出力先のディレクトリを用意する。
今回は`generated/`とする。

```sh
mkdir generated
```

### コード生成の設定ファイルを生成する

以下のコマンドを実行して各問に回答する。
今回はアプリケーションに`React`を使っているという想定。

```sh
npx graphql-code-generator init
? What type of application are you building? Application built with React
# Reactを選択
? Where is your schema?: (path or url) schema.graphql
# スキーマファイルを置いているPathを指定
? Where are your operations and fragments?: operations/*.graphql
# operations/query.graphqlをワイルドカードで指定
? Where to write the output: generated/
# 出力フォルダを指定
? Do you want to generate an introspection file? Yes
# よくわからんけどとりあえずYES
? How to name the config file? codegen.ts
# 設定ファイルの名前
? What script in package.json should run the codegen? codegen
# コマンド`npm run 〇〇`の〇〇をどうするか。
```

### コード生成

以下のコマンドでコードが生成されていることを確認する。

```tsx
npm run codegen
```
