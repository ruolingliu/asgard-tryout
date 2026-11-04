# BotProvider

`asgard-ai.com/v1alpha1`, kind `BotProvider`, plural `botproviders`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.adminApiKey` | object | - |  |  |  |
| `spec.adminApiKey.value` | string | - |  |  |  |
| `spec.adminApiKey.valueFrom` | object | - |  |  |  |
| `spec.adminApiKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.adminApiKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.adminApiKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.adminApiKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.adminApiKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.adminApiKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.adminApiKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.adminApiKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.botProviderClass` | string | **required** |  | one of `generic`, `telegram`, `line`, `discord`, `slack`, `msteams` |  |
| `spec.channelMaxIdleMs` | integer | - |  | format `int64` |  |
| `spec.debugMode` | string | - |  | one of `never`, `on-demand`, `always` |  |
| `spec.disabled` | boolean | **required** |  |  |  |
| `spec.discord` | object | - |  |  |  |
| `spec.discord.botToken` | object | **required** |  |  |  |
| `spec.discord.botToken.value` | string | - |  |  |  |
| `spec.discord.botToken.valueFrom` | object | - |  |  |  |
| `spec.discord.botToken.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.discord.botToken.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.discord.botToken.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.discord.botToken.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.discord.botToken.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.discord.botToken.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.discord.botToken.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.discord.botToken.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.entrypoint` | object | **required** |  |  |  |
| `spec.entrypoint.entry` | string | **required** |  |  |  |
| `spec.entrypoint.workflow` | string | **required** |  |  |  |
| `spec.generic` | object | - |  |  |  |
| `spec.generic.apiKey` | object | - |  |  |  |
| `spec.generic.apiKey.value` | string | - |  |  |  |
| `spec.generic.apiKey.valueFrom` | object | - |  |  |  |
| `spec.generic.apiKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.generic.apiKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.generic.apiKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.generic.apiKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.generic.apiKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.generic.apiKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.generic.apiKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.generic.apiKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.generic.authMode` | string | - |  | one of `none`, `api-key` |  |
| `spec.line` | object | - |  |  |  |
| `spec.line.channelAccessToken` | object | **required** |  |  |  |
| `spec.line.channelAccessToken.value` | string | - |  |  |  |
| `spec.line.channelAccessToken.valueFrom` | object | - |  |  |  |
| `spec.line.channelAccessToken.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.line.channelAccessToken.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.line.channelAccessToken.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.line.channelAccessToken.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.line.channelAccessToken.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.line.channelAccessToken.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.line.channelAccessToken.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.line.channelAccessToken.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.line.channelSecret` | object | **required** |  |  |  |
| `spec.line.channelSecret.value` | string | - |  |  |  |
| `spec.line.channelSecret.valueFrom` | object | - |  |  |  |
| `spec.line.channelSecret.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.line.channelSecret.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.line.channelSecret.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.line.channelSecret.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.line.channelSecret.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.line.channelSecret.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.line.channelSecret.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.line.channelSecret.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.maxUnsupervisedSteps` | integer | **required** |  | format `int32` |  |
| `spec.msteams` | object | - |  |  |  |
| `spec.msteams.appId` | string | **required** |  | matches `^[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}$` | AppId is the Application (client) ID of the Entra app registration backing this bot. It is also the audience ('aud') of the inbound Bot Framework JWT, and the suffix of the Activity's recipient.id ("28:<appId>"). Always a GUID. An empty or malformed one makes every inbound JWT fail its audience check, which looks like "Teams is silent" rather than like a configuration error. |
| `spec.msteams.appPassword` | object | **required** |  |  | AppPassword is the client secret of that app registration. Entra caps the lifetime of a client secret at 24 months, so it has to be rotated. |
| `spec.msteams.appPassword.value` | string | - |  |  |  |
| `spec.msteams.appPassword.valueFrom` | object | - |  |  |  |
| `spec.msteams.appPassword.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.msteams.appPassword.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.msteams.appPassword.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.msteams.appPassword.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.msteams.appPassword.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.msteams.appPassword.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.msteams.appPassword.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.msteams.appPassword.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.msteams.botTenantId` | string | **required** |  |  | BotTenantId is the Entra tenant the BOT'S OWN identity belongs to — the one used to obtain a Bot Connector token from login.microsoftonline.com/{botTenantId}/oauth2/v2.0/token. When the Azure resources live in the Asgard tenant and serve several customers, every BotProvider carries the same value here: Asgard's own tenant. This is NOT the customer's tenant. See customerTenantId — the two happen to be equal only when the Azure resources were created inside the customer's own tenant, and confusing them is the classic way this integration breaks. Deliberately NOT constrained to a GUID, unlike appId and customerTenantId: the {tenant} segment of that URL also accepts a verified domain name such as contoso.onmicrosoft.com, and common / organizations / consumers. A GUID pattern here would reject input Microsoft accepts. |
| `spec.msteams.customerTenantId` | string | **required** |  | matches `^[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}$` | CustomerTenantId is the tenant of the CUSTOMER this provider serves — the Teams tenant whose users talk to the bot. It is NOT botTenantId: that one is the bot's own identity tenant, used to fetch a token. The two are equal only when the Azure resources were created inside the customer's own tenant. It is the ROUTING KEY. All customers share one Azure Bot and one messaging endpoint, so the URL carries nothing that tells them apart; the edge server matches the inbound Activity's channelData.tenant.id (falling back to conversation.tenantId) against this field to find the BotProvider to run. That lookup is also the allow list — an unregistered tenant is dropped, not served by some default provider — and it is trusted only after the Bot Framework JWT has been validated, since an unverified payload can claim any tenant. Required, because a BotProvider without it can never be routed to: it would be created happily and then silently receive nothing. It is a GUID — channelData.tenant.id always is, so the pattern below costs nothing — and it is compared case-insensitively: hand-entered values tend to be upper case while Teams sends lower case. |
| `spec.slack` | object | - |  |  |  |
| `spec.slack.appToken` | object | **required** |  |  |  |
| `spec.slack.appToken.value` | string | - |  |  |  |
| `spec.slack.appToken.valueFrom` | object | - |  |  |  |
| `spec.slack.appToken.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.slack.appToken.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.slack.appToken.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.slack.appToken.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.slack.appToken.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.slack.appToken.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.slack.appToken.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.slack.appToken.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.slack.botToken` | object | **required** |  |  |  |
| `spec.slack.botToken.value` | string | - |  |  |  |
| `spec.slack.botToken.valueFrom` | object | - |  |  |  |
| `spec.slack.botToken.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.slack.botToken.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.slack.botToken.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.slack.botToken.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.slack.botToken.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.slack.botToken.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.slack.botToken.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.slack.botToken.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.telegram` | object | - |  |  |  |
| `spec.telegram.botToken` | object | **required** |  |  |  |
| `spec.telegram.botToken.value` | string | - |  |  |  |
| `spec.telegram.botToken.valueFrom` | object | - |  |  |  |
| `spec.telegram.botToken.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.telegram.botToken.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.telegram.botToken.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.telegram.botToken.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.telegram.botToken.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.telegram.botToken.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.telegram.botToken.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.telegram.botToken.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.telegram.webhookSecretToken` | object | **required** |  |  |  |
| `spec.telegram.webhookSecretToken.value` | string | - |  |  |  |
| `spec.telegram.webhookSecretToken.valueFrom` | object | - |  |  |  |
| `spec.telegram.webhookSecretToken.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.telegram.webhookSecretToken.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.telegram.webhookSecretToken.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.telegram.webhookSecretToken.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.telegram.webhookSecretToken.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.telegram.webhookSecretToken.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.telegram.webhookSecretToken.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.telegram.webhookSecretToken.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
