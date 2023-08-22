# allabout-ogawa-cloudrun
## 概要
Cloud Runを触ったことがないので学習
以前に実装したallabout-ogawa-webhookのメール送信するだけのアプリを作成し、
以前はGKEだったが、今回はCloud Runへデプロイすることで比較学習する。


## 成果物
```
Github
https://github.com/oootaiji/allabout-ogawa-cloudrun

学習アウトプット
https://github.com/oootaiji/allabout-ogawa-cloudrun/blob/main/CloudRunを学習.md

アプリ
お金かかるため、デプロイしたらすぐ停止
```


## 目的・要件
### 目的
- 実践的な学習
    - 商用・業務で使うことを意識する
    - devopsを意識する
        - 本番環境はdockerコンテナが動いているが、ローカル開発環境もコンテナで動くようにする
        - devopsを意識して、開発環境と本番環境の連携を容易にする

### インフラ要件
- クラウド
    - Cloud Run
    - やらない
        - VPC (ネットワーク設計)
        - 運用設計・運用方針
- リポジトリ管理
    - Github
- CI/CD
    - Github Actions

### アプリ要件
- allabout-ogawa-webhookに同じ



## 手動デプロイ
### SendGridの準備
- SendGridのSender Authenticationを設定
    - チュートリアルどおりに設定する


### デプロイ (Cloud Console)
- cloudrun作成
    - 名前は `allabout-ogawa-cloudrun` にする
    - 未承認呼び出しを許可を選択 (内部的なAPIではなく、公開APIにする)
    - ランタイム環境変数にSendGridのAPIキーを設定
    - コードを作成
- デプロイ
- デプロイ確認
    - https://hoge.com/allabout-ogawa-cloudrun/関数名



## デプロイ自動化
### 1. サービスアカウント(権限)JSONの作成
- IAMでサービスアカウントを作成 (運用方針は定義してないのでこだわらない。すぐ削除する)
    - 以下の3つのロールを入れておく
        - Cloud Run (とりあえず管理者でOK)
        - Artifact Registry (とりあえず管理者でOK)
        - ストレージ (とりあえず管理者でOK)
- Workload Identityを有効にする
    - APIを有効化
    - Workload Identityを作成
    - Service Accountに紐付ける

### 2. Github Actionsのyamlを作成
- .github/workflows/workflow.yml作成
- Githubに環境変数を設定 (config.yamlで使う環境変数を登録)
    - アプリで使う環境変数
    - サービスアカウントJSON


### 3. デプロイ
1. 手動デプロイは済ませておく
    1. 「未承認呼び出しを許可」は後で設定を変えられないので注意
2. mainへpush
3. デプロイ確認
    1. Actionsのworkflowが動く
    2. Actionsのworkflowが正常終了
    3. ブラウザにてアプリ稼働確認


## 注意
- allow-authenticatedは、変更不可。はじめのデプロイで設定しておく必要がある
- GKEと同じで最初デプロイしている状態からCICDを始める
- actionsにcloud run deployのライブラリがある

## 参考
- [チュートリアル](https://cloud.google.com/run/docs/tutorials?hl=ja)
- [クイックスタート](https://cloud.google.com/run/docs/quickstarts?hl=ja)
- [cloud run deployのactionsのライブラリ](https://github.com/google-github-actions/deploy-cloudrun/tree/main)
