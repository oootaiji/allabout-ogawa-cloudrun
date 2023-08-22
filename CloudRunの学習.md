# CloudRunを学習
## 概要
知識は人に説明できる状態で初めて価値が出るので、CloudRunについて説明できる状態にする
更に、GCPにはGKE,CloudRuns,CloudFunctionsという３つの違いを学習し、
技術選定でどのサービスを使えばよいのかを適切に判断できる状態を目指す。


## GKEとは
### 説明
- GCPのマネージドなKubernetesサービスで
- Google Kubernetes Engine
- k8sと呼ばれる理由は、kとsの間に8文字あるためで、英語でそういった略する表現方法があるらしい
- 特徴
    - Kubernetesベースのコンテナ環境


## Cloud Runとは
### 説明
- 一言
    - 
- 特徴 (比較して)


## Cloud Functionsとは
### 説明
- 一言
    - 
- 特徴 (比較して)

### デメリット
- 直接、独自ドメインが設定できないので、独自ドメインを必要としない領域の用途がよさそう (バックエンドのAPIとして, 簡易的なAPIとしてなど)



## GAPとは
- Google App Engineの略
- サーバーレスの一つで、マネージド
- KGEのようにサービス単位でアプリを管理できて、サービス単位でスケールできる



## 参考文献
- GAE
    - [スタートアップがGAE/Goを選択する上で知っておきたいこと](https://logmi.jp/tech/articles/304030)
- 事業の成長と技術選定
    - [事業成長とともに歩む Cloud Run→GAE→GKE Autopilot の旅路](https://www.youtube.com/watch?v=lzN2jSUHS84)
- コンテナのステートフルとステートレスとは
    - [ステートフルとステートレス](https://www.redhat.com/ja/topics/cloud-native-apps/stateful-vs-stateless)
- IaaSとPaaSとSaaS
    - [PaaS、IaaS、SaaS、CaaS の違い](https://cloud.google.com/learn/paas-vs-iaas-vs-saas?hl=ja)
- GAEはインスタンスのRAMに保存するからメモリを使う
    - [GAEはファイル保存はRAMへ](https://cloud.google.com/appengine/docs/standard/php-gen2/using-temp-files?hl=ja)
    - [cloud runはインメモリファイルシステム](https://cloud.google.com/run/docs/container-contract?hl=ja#filesystem)


## おまけ
### phpのメモリ
- 関数の変数で使っているメモリはすぐ開放される
- [リファレンスカウントが0になると開放される](https://zenn.dev/minonoblog/articles/35d51fff3baf1b)
- [get_memory_usageでメモリを使っている部分をデバッグする](https://qiita.com/hinako_n/items/8a7b366a3fe09f43dce8)

### GKEのストレージ
- [k8sは、ephemeral volume(一時データ)とpersistant volume(永続的なデータ)の２種類ある](https://qiita.com/toshihirock/items/0c91bbedf0e144acf6fc)
- [データ永続化の参考](https://www.netone.co.jp/knowledge-center/netone-blog/20191206-1/)
- さらにephemeral volumeには、複数の保存先がある
    - emptyDir: podの一時データ
    - hostPath: ノードの一時データ
- [保存先の考え方として、pod, ノード, 外部の３種類がある](https://www.netone.co.jp/knowledge-center/netone-blog/20191206-1/)