# Astro を Cloudflare Pages にデプロイするテンプレート

## 用意するもの

CloudFlare のアカウント id と API トークン

## デプロイするまで

1. `npm i` でパッケージをインストール
2. Pages プロジェクトの作成

```shell
npx wrangler pages project create <YOUR_PROJECT_NAME> --production-branch <PRODUCTION_BRANCH>
```

`<YOUR_PROJECT_NAME>` にはCloudflare Pages上に作成するプロジェクト名
`<PRODUCTION_BRANCH>` には本番用のバージョンとしてデプロイするブランチ名を指定します。(指定したbranch以外の指定でデプロイをすると開発用のバージョンとしてデプロイされます)


## CICD のセットアップ

### メインブランチへのマージタイミングで Pages にデプロイする。

1. workflow ファイルを有効にする

deploy.yaml.disable の名前変更。disable をなくす。

`mv .github/workflows/deploy.yaml.disable .github/workflows/deploy.yaml`

2. githubのsecretsにPagesのデプロイに必要な情報を書き込む

    1. setting > Security > Secrets and variables > Actions に遷移(https://github.com/{userId}/{repositoryId}/settings/secrets/actions に遷移するはず)し、「New repository secrets」クリック
    2. Nameに `CLOUDFLARE_API_TOKEN` を入れる。Secretに取得したAPIトークンを入れる。Add secretボタンをクリック
    3. 再度「New repository secrets」クリック
    3. `CLOUDFLARE_ACCOUNT_ID` を入れる。Secretに取得したアカウントidを入れる

3. githubにPUSHする。
