---
title: サードパーティアプリケーションと接続する
intro: '{% data variables.product.product_name %}のアイデンティティを、OAuth を使うサードパーティのアプリケーションに接続できます。 これらのアプリケーションを認可する際には、そのアプリケーションを信頼するか、誰が開発したのか、そのアプリケーションがどういった種類の情報にアクセスしたいのかを確認すべきです。'
redirect_from:
  - /articles/connecting-with-third-party-applications
versions:
  free-pro-team: '*'
  enterprise-server: '*'
  github-ae: '*'
---

サードパーティアプリケーションが {% data variables.product.product_name %} ログインであなたを識別したい場合、そのアプリケーションの開発者の連絡先情報と、リクエストされている情報のリストのページが表示されます。

### アプリケーション開発者に連絡する

アプリケーションは、{% data variables.product.product_name %} 以外のサードパーティにより開発されているため、アプリケーションがアクセスを要求しているデータをどう使うかについて、私たちは正確に把握していません。 アプリケーションについて、質問や懸念がある場合は、ページ上部の開発者情報を使って、アプリケーション管理者に連絡できます。

![{% data variables.product.prodname_oauth_app %}オーナー情報](/assets/images/help/platform/oauth_owner_bar.png)

開発者が情報を入力している場合は、ページの右側に、アプリケーションの詳細情報や関連ウェブサイトが表示されます。

![OAuth アプリケーションの情報とウェブサイト](/assets/images/help/platform/oauth_app_info.png)

### アプリケーションのアクセスとデータのタイプ

アプリケーションは、{% data variables.product.product_name %}のデータに対して*読み取り*または*書き込み*アクセスを持つことができます。

- **読み取りアクセス**は、アプリケーションに対してデータを*見る*ことのみを許可します。
- **書き込みアクセス**は、アプリケーションに対してデータを*変更*することを許可します。

#### OAuth のスコープについて

*スコープ*は、アプリケーションがパブリックおよび非パブリックのデータへのアクセスをリクエストできる権限について名前を付けたグループです。

{% data variables.product.product_name %} と統合するサードパーティアプリケーションを使用したい場合、そのアプリケーションは、データに対してどういった種類のアクセスが必要になるのかをあなたに通知します。 アプリケーションにアクセスを許可すれば、アプリケーションはあなたの代わりにデータの読み取りや変更といったアクションを行えるようになります。 たとえば `user:email` スコープをリクエストするアプリケーションを使用したい場合、そのアプリケーションはあなたのプライベートのメールアドレスに対してリードオンリーのアクセスを持つことになります。 詳しい情報については 、「[{% data variables.product.prodname_oauth_app %} のスコープについて](//apps/building-integrations/setting-up-and-registering-oauth-apps/about-scopes-for-oauth-apps)」を参照してください。

{% tip %}

**メモ:** 現時点では、ソースコードへのアクセスのスコープをリードオンリーにすることはできません。

{% endtip %}

#### リクエストされるデータの種類

アプリケーションがリクエストできるデータの種類はいくつかあります。

![OAuth アクセスの詳細](/assets/images/help/platform/oauth_access_types.png)

{% tip %}

**ヒント:** {% data reusables.user_settings.review_oauth_tokens_tip %}

{% endtip %}

| データの種類                | 説明                                                                                                                                                                                                  |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| コミットのステータス            | サードパーティアプリケーションに、コミットのステータスを報告するためのアクセスを許可できます。 コミットステータスのアクセスがあれば、アプリケーションはビルドが特定のコミットに対して成功したかどうかを判定できます。 アプリケーションは、コードにはアクセスできませんが、特定のコミットに対するステータス情報を読み書き<em>できます</em>。             |
| デプロイメント               | Deployment status access allows applications to determine if a deployment is successful against a specific commit for public and private repositories. Applications won't have access to your code. |
| Gist                  | [Gist](https://gist.github.com) アクセスがあれば、アプリケーションはあなたのパブリックおよびシークレット Gist の両方を読み書きできます。                                                                                                             |
| フック                   | [webhook](/webhooks) アクセスがあれば、アプリケーションはあなたが管理するリポジトリ上のフックの設定を読み書きできます。                                                                                                                              |
| 通知                    | Notification access allows applications to read your {% data variables.product.product_name %} notifications, such as comments on issues and pull requests. ただし、アプリケーションはリポジトリ内へはアクセスできません。         |
| Organization および Team | Organization および Team のアクセスがあれば、アプリケーションは Organization および Team のメンバー構成へのアクセスと管理ができます。                                                                                                              |
| 個人ユーザデータ              | ユーザデータには、名前、メールアドレス、所在地など、ユーザプロファイル内の情報が含まれます。                                                                                                                                                      |
| リポジトリ                 | リポジトリ情報には、コントリビュータの名前、あなたが作成したブランチ、リポジトリ内の実際のファイルなどが含まれます。 アプリケーションは、ユーザ単位でパブリックまたはプライベートリポジトリへのアクセスをリクエストできます。                                                                                     |
| リポジトリの削除              | アプリケーションはあなたが管理するリポジトリの削除をリクエストできますが、コードにアクセスすることはできません。                                                                                                                                            |

### 更新された権限のリクエスト

アプリケーションは新しいアクセス権限をリクエストできます。 権限の更新を要求する場合、アプリケーションはその違いについて通知します。

![サードパーティアプリケーションのアクセスを変更する](/assets/images/help/platform/oauth_existing_access_pane.png)