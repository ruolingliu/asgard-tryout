# CompletionModel

`asgard-ai.com/v1alpha1`, kind `CompletionModel`, plural `completionmodels`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.anthropic` | object | - |  |  |  |
| `spec.anthropic.apiKey` | object | **required** |  |  |  |
| `spec.anthropic.apiKey.value` | string | - |  |  |  |
| `spec.anthropic.apiKey.valueFrom` | object | - |  |  |  |
| `spec.anthropic.apiKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.anthropic.apiKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.anthropic.apiKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.anthropic.apiKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.anthropic.apiKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.anthropic.apiKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.anthropic.apiKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.anthropic.apiKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.anthropic.model` | string | **required** |  |  |  |
| `spec.aoaiChat` | object | - |  |  |  |
| `spec.aoaiChat.apiKey` | object | **required** |  |  |  |
| `spec.aoaiChat.apiKey.value` | string | - |  |  |  |
| `spec.aoaiChat.apiKey.valueFrom` | object | - |  |  |  |
| `spec.aoaiChat.apiKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.aoaiChat.apiKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.aoaiChat.apiKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.aoaiChat.apiKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.aoaiChat.apiKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.aoaiChat.apiKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.aoaiChat.apiKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.aoaiChat.apiKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.aoaiChat.apiVersion` | string | **required** |  |  |  |
| `spec.aoaiChat.deploymentId` | string | **required** |  |  |  |
| `spec.aoaiChat.resourceName` | string | **required** |  |  |  |
| `spec.asgardModelHub` | object | - |  |  | AsgardModelHubCompletionModelSpec calls a model through Asgard Model Hub (Tyr). Model Hub speaks both the OpenAI Chat Completions and the Anthropic Messages protocols, so a call keeps whichever protocol it arrived in; the model behind the name may come from any provider Model Hub routes to. |
| `spec.asgardModelHub.apiKey` | object | **required** |  |  | ApiKey is a Model Hub API key, created by the tenant in Model Hub. |
| `spec.asgardModelHub.apiKey.value` | string | - |  |  |  |
| `spec.asgardModelHub.apiKey.valueFrom` | object | - |  |  |  |
| `spec.asgardModelHub.apiKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.asgardModelHub.apiKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.asgardModelHub.apiKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.asgardModelHub.apiKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.asgardModelHub.apiKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.asgardModelHub.apiKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.asgardModelHub.apiKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.asgardModelHub.apiKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.asgardModelHub.model` | string | **required** |  |  | Model is the model name as Model Hub lists it for the API key, e.g. claude-sonnet-5-5. |
| `spec.builtin` | object | - |  |  | BuiltinCompletionModelSpec declares an Asgard-managed model. It deliberately holds no API key or concrete model name — only a tier alias. The model router maps the alias to a concrete Anthropic model and supplies the managed key from its own environment, so the key never lands in a CR or per-namespace Secret. |
| `spec.builtin.alias` | string | **required** |  | one of `complex`, `balanced`, `fast`, `vision` | CompletionModelBuiltinAlias is the tier of an Asgard-managed builtin model. Each alias maps (in the model router, via env) to a concrete model: complex → claude-opus-4-8, balanced → claude-sonnet-4-6, fast → claude-haiku-4-5 (Anthropic); vision → a Gemini model for document/image understanding. |
| `spec.completionModelClass` | string | **required** |  | one of `aoai-chat`, `openai-chat`, `gemini`, `anthropic`, `mistral`, `builtin`, `gcp-anthropic`, `asgard-model-hub` |  |
| `spec.gcpAnthropic` | object | - |  |  | GcpAnthropicCompletionModelSpec calls an Anthropic publisher model on GCP Agent Platform. The request and response are Anthropic Messages; only the endpoint and authentication differ from the anthropic class. |
| `spec.gcpAnthropic.credentials` | object | **required** |  |  | Credentials is a Google service account key JSON. The service account needs roles/aiplatform.user on ProjectId. |
| `spec.gcpAnthropic.credentials.value` | string | - |  |  |  |
| `spec.gcpAnthropic.credentials.valueFrom` | object | - |  |  |  |
| `spec.gcpAnthropic.credentials.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.gcpAnthropic.credentials.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.gcpAnthropic.credentials.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.gcpAnthropic.credentials.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.gcpAnthropic.credentials.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.gcpAnthropic.credentials.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.gcpAnthropic.credentials.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.gcpAnthropic.credentials.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.gcpAnthropic.location` | string | - | `"global"` | matches `^(global\|us\|eu\|[a-z]+-[a-z]+[0-9]+)$` | Location is the GCP Agent Platform endpoint: global, the us / eu multi-regions, or a single region such as us-east5. |
| `spec.gcpAnthropic.model` | string | **required** |  |  | Model is the GCP Agent Platform model ID, e.g. claude-sonnet-5-5. |
| `spec.gcpAnthropic.projectId` | string | **required** |  | matches `^([a-z0-9.-]+:)?[a-z][a-z0-9-]{4,28}[a-z0-9]$` | ProjectId is the GCP project the calls are made in (and billed to). |
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
| `spec.openaiChat` | object | - |  |  |  |
| `spec.openaiChat.apiKey` | object | **required** |  |  |  |
| `spec.openaiChat.apiKey.value` | string | - |  |  |  |
| `spec.openaiChat.apiKey.valueFrom` | object | - |  |  |  |
| `spec.openaiChat.apiKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.openaiChat.apiKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.openaiChat.apiKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.openaiChat.apiKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.openaiChat.apiKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.openaiChat.apiKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.openaiChat.apiKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.openaiChat.apiKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.openaiChat.endpoint` | string | - |  |  |  |
| `spec.openaiChat.model` | string | **required** |  |  |  |
