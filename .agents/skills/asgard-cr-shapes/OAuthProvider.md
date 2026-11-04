# OAuthProvider

`asgard-ai.com/v1alpha1`, kind `OAuthProvider`, plural `oauthproviders`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.additionalParameters` | object | - |  |  | Additional parameters to be passed to the OAuth provider |
| `spec.clientId` | object | **required** |  |  | The OAuth client id. It is not a secret, so `value` is the usual form; `valueFrom` reads it from a Secret or ConfigMap key like any other value. |
| `spec.clientId.value` | string | - |  |  |  |
| `spec.clientId.valueFrom` | object | - |  |  |  |
| `spec.clientId.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.clientId.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.clientId.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.clientId.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.clientId.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.clientId.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.clientId.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.clientId.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.clientSecret` | object | **required** |  |  | The OAuth client secret, normally `valueFrom.secretKeyRef` to a key of the release's app Secret. The key can have any name, so one release can hold the clients of several providers. |
| `spec.clientSecret.value` | string | - |  |  |  |
| `spec.clientSecret.valueFrom` | object | - |  |  |  |
| `spec.clientSecret.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.clientSecret.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.clientSecret.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.clientSecret.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.clientSecret.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.clientSecret.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.clientSecret.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.clientSecret.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.endpoints` | object | **required** |  |  |  |
| `spec.endpoints.authURL` | string | **required** |  | format `uri` | OAuth authorization URL |
| `spec.endpoints.revocationURL` | string | - |  | format `uri` | Token revocation URL (RFC 7009). Optional: without it, disconnecting an account deletes the platform's copy of the tokens and revokes nothing at the provider. |
| `spec.endpoints.tokenURL` | string | **required** |  | format `uri` | OAuth token exchange URL |
| `spec.endpoints.userInfoURL` | string | - |  | format `uri` | URL that returns the authorized account, such as an OpenID Connect userinfo endpoint. Optional: without it, the account that granted access is not shown. |
| `spec.scopes` | array | **required** |  |  | OAuth scopes requested for this provider |
