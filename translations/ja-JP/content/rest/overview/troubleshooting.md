---
title: トラブルシューティング
intro: REST API で発生する最も一般的な問題の解決方法を学びます。
redirect_from:
  - /v3/troubleshooting
versions:
  free-pro-team: '*'
  enterprise-server: '*'
  github-ae: '*'
---



API で不可解な問題が発生した場合、発生したと思われる問題の解決策をこちらの一覧から確認できます。

### `404` error for an existing repository

通常、クライアントが正しく認証されていない場合、`404` エラーが送信されます。 このような場合、`403 Forbidden` が表示されるはずであると考えるかもしれません。 しかし、プライベートリポジトリに関する_いずれの_情報も提供されないため、API は代わりに `404` エラーを返します。

トラブルシューティングを行うには、[正しく認証されていること](/guides/getting-started/)、[OAuth アクセストークンに必要なスコープがあること](/apps/building-oauth-apps/understanding-scopes-for-oauth-apps/)、そして[サードパーティアプリケーションの制限][oap-guide]によってアクセスがブロックされていないことを確認してください。

### Not all results returned

リソース（_例:_ ユーザ、Issue _など_）のリストにアクセスするほとんどの API 呼び出しは、ページネーションをサポートしています。 リクエストをして、すべての結果を受け取っていない場合は、おそらく最初のページしか表示されていません。 より多くの結果を受け取るには、残りのページをリクエストする必要があります。

ページネーション URL のフォーマットを推測*しない*ことが重要です。 すべての API 呼び出しで同じ構造が使用されるわけではありません。 代わりに、すべてのリクエストで送信される [Link Header](/rest#pagination) からページネーション情報を抽出します。

{% if currentVersion == "free-pro-team@latest" %}
### Basic authentication errors

On November 13, 2020 username and password authentication to the REST API and the OAuth Authorizations API were deprecated and no longer work.

#### Using `username`/`password` for basic authentication

If you're using `username` and `password` for API calls, then they are no longer able to authenticate. 例:

```bash
curl -u my_user:my_password https://api.github.com/user/repos
```

Instead, use a [personal access token](/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line) when testing endpoints or doing local development:

```bash
curl -H 'Authorization: token my_access_token' https://api.github.com/user/repos
```

For OAuth Apps, you should use the [web application flow](/apps/building-oauth-apps/authorizing-oauth-apps/#web-application-flow) to generate an OAuth token to use in the API call's header:

```bash
curl -H 'Authorization: token my-oauth-token' https://api.github.com/user/repos
```

#### Calls to OAuth Authorizations API

If you're making [OAuth Authorization API](/enterprise-server@2.22/rest/reference/oauth-authorizations) calls to manage your OAuth app's authorizations or to generate access tokens, similar to this example:

```bash
curl -u my_username:my_password -X POST "https://api.github.com/authorizations" -d '{"scopes":["public_repo"], "note":"my token", "client_id":"my_client_id", "client_secret":"my_client_secret"}'
```

Then you must switch to the [web application flow](/apps/building-oauth-apps/authorizing-oauth-apps/#web-application-flow) to generate access tokens.

{% endif %}

[oap-guide]: https://developer.github.com/changes/2015-01-19-an-integrators-guide-to-organization-application-policies/