# create-pr-action

## 概要
`create-pr-action`は、変更したファイルをコミットし、自動的にプルリクエストを作成するGitHub Actionです。このアクションは、コミットメッセージをそのままプルリクエストのタイトルと本文に利用します。必要なパーミッションには「contents: write」と「pull-requests: write」が含まれます。

## 使い方
このアクションを使用するには、以下のようにGitHub Actionsワークフローに追加してください。

```yaml
name: Create Pull Request

on:
  push:
    branches:
      - main

jobs:
  create-pr:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      - name: Create Pull Request
        uses: ./.github/actions/create-pr-action
        with:
          message: "My commit message"
```
## 必須要件
- GitHub CLI (`gh`) がインストールされていること。
- リポジトリに書き込み権限を持つパーソナルアクセストークン (PAT) またはGITHUB_TOKENが必要です。

## 入出力インターフェイス

### 入力
- `message`: (必須) コミットメッセージ。

### 出力
- `branch`: プルリクエストが作成されたブランチの名前。

## 環境変数
このアクションで利用される環境変数は以下の通りです。

- `USERNAME`: GitHubのユーザー名。デフォルトは`github-actions[bot]`。
- `EMAIL`: GitHubのメールアドレス。デフォルトは`41898282+github-actions[bot]@users.noreply.github.com`。
- `MESSAGE`: コミットメッセージ。
- `BRANCH`: プルリクエストを作成するためのブランチ名。
- `GITHUB_TOKEN`: GitHubの認証トークン。

## GITHUB_TOKEN のパーミッション
このアクションを正しく機能させるためには、GITHUB_TOKENに以下のパーミッションが必要です。

- `contents: write`
- `pull-requests: write`

## よくある質問

### 1. `AccessDenied` エラーが発生します。
GITHUB_TOKENのパーミッションが不足している可能性があります。必要なパーミッション（`contents: write`と`pull-requests: write`）を付与してください。
