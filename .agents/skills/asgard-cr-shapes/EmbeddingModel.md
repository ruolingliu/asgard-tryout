# EmbeddingModel

`asgard-ai.com/v1alpha1`, kind `EmbeddingModel`, plural `embeddingmodels`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.aoai` | object | - |  |  |  |
| `spec.aoai.apiKey` | object | **required** |  |  |  |
| `spec.aoai.apiKey.value` | string | - |  |  |  |
| `spec.aoai.apiKey.valueFrom` | object | - |  |  |  |
| `spec.aoai.apiKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.aoai.apiKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.aoai.apiKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.aoai.apiKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.aoai.apiKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.aoai.apiKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.aoai.apiKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.aoai.apiKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.aoai.apiVersion` | string | **required** |  |  |  |
| `spec.aoai.deploymentId` | string | **required** |  |  |  |
| `spec.aoai.resourceName` | string | **required** |  |  |  |
| `spec.builtin` | object | - |  |  | BuiltinEmbeddingModelSpec declares an Asgard-managed embedding model. Like its completion counterpart it holds no API key or concrete model name — only a tier alias; the model router supplies the managed key and concrete model. |
| `spec.builtin.alias` | string | **required** |  | one of `balanced` | EmbeddingModelBuiltinAlias is the tier of an Asgard-managed builtin embedding model. The model router maps it (via env) to a concrete model: balanced → text-embedding-3-small (OpenAI). |
| `spec.embeddingModelClass` | string | **required** |  | one of `aoai`, `openai`, `gemini`, `voyageai`, `mistral`, `builtin` |  |
| `spec.gemini` | object | - |  |  |  |
| `spec.gemini.apiKey` | object | **required** |  |  |  |
| `spec.gemini.apiKey.value` | string | - |  |  |  |
| `spec.gemini.apiKey.valueFrom` | object | - |  |  |  |
| `spec.gemini.apiKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.gemini.apiKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.gemini.apiKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.gemini.apiKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.gemini.apiKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.gemini.apiKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.gemini.apiKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.gemini.apiKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.gemini.model` | string | **required** |  |  |  |
| `spec.mistral` | object | - |  |  |  |
| `spec.mistral.apiKey` | object | **required** |  |  |  |
| `spec.mistral.apiKey.value` | string | - |  |  |  |
| `spec.mistral.apiKey.valueFrom` | object | - |  |  |  |
| `spec.mistral.apiKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.mistral.apiKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.mistral.apiKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.mistral.apiKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.mistral.apiKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.mistral.apiKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.mistral.apiKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.mistral.apiKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.mistral.model` | string | **required** |  |  |  |
| `spec.openai` | object | - |  |  |  |
| `spec.openai.apiKey` | object | **required** |  |  |  |
| `spec.openai.apiKey.value` | string | - |  |  |  |
| `spec.openai.apiKey.valueFrom` | object | - |  |  |  |
| `spec.openai.apiKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.openai.apiKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.openai.apiKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.openai.apiKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.openai.apiKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.openai.apiKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.openai.apiKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.openai.apiKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.openai.endpoint` | string | - |  |  |  |
| `spec.openai.model` | string | **required** |  |  |  |
| `spec.voyageai` | object | - |  |  |  |
| `spec.voyageai.apiKey` | object | **required** |  |  |  |
| `spec.voyageai.apiKey.value` | string | - |  |  |  |
| `spec.voyageai.apiKey.valueFrom` | object | - |  |  |  |
| `spec.voyageai.apiKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.voyageai.apiKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.voyageai.apiKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.voyageai.apiKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.voyageai.apiKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.voyageai.apiKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.voyageai.apiKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.voyageai.apiKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.voyageai.model` | string | **required** |  |  |  |
