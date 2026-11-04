# OAuthCredential

`asgard-ai.com/v1alpha1`, kind `OAuthCredential`, plural `oauthcredentials`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.providerRef` | string | **required** |  |  | Reference to the OAuthProvider resource name |
| `spec.refreshToken` | object | - |  |  |  |
| `spec.refreshToken.aheadSeconds` | integer | **required** |  | format `int32` | Number of seconds ahead to refresh the token before expiry |
| `spec.refreshToken.autoRefresh` | boolean | **required** |  |  | Whether to automatically refresh the token when it's about to expire |
