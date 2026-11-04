# KnowledgeBase

`asgard-ai.com/v1alpha1`, kind `KnowledgeBase`, plural `knowledgebases`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.asgardBaseline` | object | **required** |  |  |  |
| `spec.asgardBaseline.aliasName` | string | **required** |  | matches `^[a-z_][a-z_0-9$]*$` |  |
| `spec.asgardBaseline.apiKey` | object | **required** |  |  |  |
| `spec.asgardBaseline.apiKey.value` | string | - |  |  |  |
| `spec.asgardBaseline.apiKey.valueFrom` | object | - |  |  |  |
| `spec.asgardBaseline.apiKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.asgardBaseline.apiKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.asgardBaseline.apiKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.asgardBaseline.apiKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.asgardBaseline.apiKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.asgardBaseline.apiKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.asgardBaseline.apiKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.asgardBaseline.apiKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.asgardBaseline.authMode` | string | - |  | one of `none`, `api-key` |  |
| `spec.knowledgeBaseClass` | string | **required** |  | one of `asgard-baseline` |  |
