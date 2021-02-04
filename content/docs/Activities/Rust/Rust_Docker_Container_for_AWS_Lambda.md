# AWS Lambda でのカスタムコンテナイメージで Rust を動かす
[AWS Lambda の新機能 – コンテナイメージのサポート](https://aws.amazon.com/jp/blogs/news/new-for-aws-lambda-container-image-support/) から、手順を確認。

選択肢は、2つ。
- Amazon Linux ベースのカスタムランタイム用のベースイメージがすでにあって、Lambda ランタイム APIを実装する
- Alpine や Debian Linux などの独自のベースイメージにした場合には Lamdbaランタイム API を実装する必要がある


関連するツールは下記。
- Runtime interface clients: lambda と関数の間のコミュニケーションを監理する
- Lambda Runtime Interface Emulator にて、ローカルテストが実施できる


手順は、下記
- AWS Lambda アプリケーションを実装
- AWS Lambda のためのコンテナイメージを作成
    - Dockerfile の作成
        - Lambda Runtime Interface Client を追加
        - Lambda Runtime Interface Emulator を追加(オプション)
        - Lambda Runtime Interface Client を起動する `entry.sh` を作成して、`ENTRYPOINT` とする
- Amazon ECR へプッシュ
- AWS Lambda 上へデプロイ

### Rust Runtime for AWS Lambda とは
- AWS Labs から提供されている Rust のための Runtime
- 詳しくは [Rust Runtime for AWS Lambda](https://aws.amazon.com/blogs/opensource/rust-runtime-for-aws-lambda/)
- Runtime API で実現すること
    - 初期化エラーの通知
    - Handler の呼び出しとレスポンス or エラーの通知




### 参考
- https://github.com/yoshihitoh/rust-lambda-example