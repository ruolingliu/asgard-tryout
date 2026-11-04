# Workflow

`asgard-ai.com/v1alpha1`, kind `Workflow`, plural `workflows`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.entries` | array | **required** |  |  |  |
| `spec.entries[].files` | array | - |  |  | Files defines per-slot file type validation and context aliasing for uploaded blobs. Order matches the uploaded blob array. |
| `spec.entries[].files[].alias` | string | - |  |  | Alias, if set, stores the blob into the task context under this key. |
| `spec.entries[].files[].type` | string | **required** |  | one of `IMAGE`, `VIDEO`, `AUDIO`, `DOCUMENT`, `BINARY` | Type is the expected file type. |
| `spec.entries[].handlingProcessor` | string | - |  |  |  |
| `spec.entries[].inputSchema` | string | - |  |  | InputSchema is a JSON Schema string used to validate the entry's incoming payload. |
| `spec.entries[].labels` | object | - |  |  |  |
| `spec.entries[].name` | string | **required** |  |  |  |
| `spec.entries[].tooling` | object | - |  |  | Tooling holds the tool name and description when this entry is exposed as a tool via a Toolset. |
| `spec.entries[].tooling.allowUploadFile` | boolean | **required** |  |  |  |
| `spec.entries[].tooling.description` | string | **required** |  |  |  |
| `spec.entries[].tooling.name` | string | **required** |  | matches `^[a-z_\-0-9]+$` |  |
| `spec.exits` | array | **required** |  |  |  |
| `spec.exits[].handlingWorkflow` | object | - |  |  |  |
| `spec.exits[].handlingWorkflow.entry` | string | **required** |  |  |  |
| `spec.exits[].handlingWorkflow.name` | string | **required** |  |  |  |
| `spec.exits[].labels` | object | - |  |  |  |
| `spec.exits[].name` | string | **required** |  |  |  |
| `spec.processors` | array | **required** |  |  |  |
| `spec.processors[].configs` | array | **required** |  |  |  |
| `spec.processors[].configs[].expression` | string | - |  |  |  |
| `spec.processors[].configs[].labels` | object | - |  |  |  |
| `spec.processors[].configs[].name` | string | **required** |  |  |  |
| `spec.processors[].configs[].template` | string | - |  |  |  |
| `spec.processors[].configs[].value` | string | - |  |  |  |
| `spec.processors[].labels` | object | - |  |  |  |
| `spec.processors[].name` | string | **required** |  |  |  |
| `spec.processors[].type` | string | **required** |  | one of `push-message`, `listen-message`, `llm-completion`, `router`, `http-request`, `update-context`, `query-database`, `generate-embedding`, `execute-script`, `stream-llm-completion-message`, `retrieve-knowledge`, `validate-payload`, `llm-query-database` |  |
| `spec.relationships` | array | - |  |  |  |
| `spec.relationships[].from` | object | **required** |  |  |  |
| `spec.relationships[].from.processor` | string | **required** |  |  |  |
| `spec.relationships[].from.relationName` | string | **required** |  |  |  |
| `spec.relationships[].labels` | object | - |  |  |  |
| `spec.relationships[].to` | object | **required** |  |  |  |
| `spec.relationships[].to.exit` | string | - |  |  |  |
| `spec.relationships[].to.processor` | string | - |  |  |  |
| `spec.variables` | array | - |  |  |  |
| `spec.variables[].labels` | object | - |  |  |  |
| `spec.variables[].name` | string | **required** |  | matches `^[a-zA-Z_][a-zA-Z_0-9]*$` |  |
| `spec.variables[].value` | string | - |  |  |  |
| `spec.variables[].valueFrom` | object | - |  |  |  |
| `spec.variables[].valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.variables[].valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.variables[].valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.variables[].valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.variables[].valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.variables[].valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.variables[].valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.variables[].valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
