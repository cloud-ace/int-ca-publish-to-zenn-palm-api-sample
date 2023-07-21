# int-ca-publish-to-zenn-palm-api-sample
## 公開先ブログタイトル
- [Firebase Extensions + PaLM API で 要約アプリを作ってみた](https://zenn.dev/cloud_ace/articles/55963031745413)

## 免責事項
このリポジトリに含まれる設定やソースコードはあくまでサンプルであり、動作保証やサポートは一切提供されません。
このリポジトリの使用によって生じるいかなる損害や問題についても、作者は一切の責任を負いません。使用者は自己の責任において利用してください。
実際のプロジェクトで使用する際には、適切にテストし、必要な変更を加えることを強くお勧めします。


## Repository 概要
### 技術構成

<img width="750" src="/images/architecture_1.png">

- Flutter（フロントエンド）
  - クライアントアプリとして UI を提供
  - UI に入力された内容を Firebase Firestore の text_documents コレクションにドキュメントを追加するリクエストを送る
  - Firebase Firestore から 要約結果を受け取る
- Firebase（バックエンド）
  - Extensions により Summarize Text with PaLM API をインストール
    - API インストールにより、自動的に Firestore をトリガーとした Cloud Functions 関数がデプロイされる
  - フロントエンドからのドキュメント追加リクエストにより Firestore へのドキュメント追加を行う
    - ドキュメント追加により、PaLM API 経由で要約を行う Cloud Functions 関数が実行される
  - クライアントに要約結果を送る

### フロントエンド（Flutter）アーキテクチャー

4 層のレイヤードアーキテクチャーを採用しています。

<img width="500" src="/images/architecture_2.png">