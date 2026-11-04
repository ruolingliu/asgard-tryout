# Toolset

`asgard-ai.com/v1alpha1`, kind `Toolset`, plural `toolsets`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  | Which of tools/mcpServerConfig applies is decided by toolsetClass, not by a blanket exactly-one rule: a workflow-tooling toolset legitimately carries ZERO tools between "MCP server created" (name + description only) and its first added tool, so tools is optional and may be empty. mcpServerConfig belongs to the mcp-server class alone, where it is required and tools must stay empty. The mcp-server rule tolerates an explicitly empty list because CEL's has() reports a present-but-empty array as set. |
| `spec.apiKey` | object | **required** |  |  |  |
| `spec.apiKey.value` | string | - |  |  |  |
| `spec.apiKey.valueFrom` | object | - |  |  |  |
| `spec.apiKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.apiKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.apiKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.apiKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.apiKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.apiKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.apiKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.apiKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.mcpServerConfig` | object | - |  |  |  |
| `spec.mcpServerConfig.value` | string | - |  |  |  |
| `spec.mcpServerConfig.valueFrom` | object | - |  |  |  |
| `spec.mcpServerConfig.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.mcpServerConfig.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.mcpServerConfig.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.mcpServerConfig.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.mcpServerConfig.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.mcpServerConfig.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.mcpServerConfig.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.mcpServerConfig.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.mcpServerVolumeMounts` | array | - |  |  |  |
| `spec.mcpServerVolumeMounts[].mountPath` | string | **required** |  |  |  |
| `spec.mcpServerVolumeMounts[].sourceSetName` | string | **required** |  |  |  |
| `spec.mcpServerVolumeMounts[].subPath` | string | - |  |  |  |
| `spec.tools` | array | - |  |  | Tools is empty for a freshly created workflow-tooling toolset, and again once its last tool is removed. Consumers must read an absent or empty list as "no tools yet", not as an error. |
| `spec.tools[].entrypoint` | object | **required** |  |  |  |
| `spec.tools[].entrypoint.entry` | string | **required** |  |  |  |
| `spec.tools[].entrypoint.workflow` | string | **required** |  |  |  |
| `spec.tools[].requestConsent` | boolean | **required** |  |  | RequestConsent: when true, invocations of this tool require per-call user consent via the tool-call-consent flow. false means no consent gate. |
| `spec.toolsetClass` | string | **required** |  | one of `workflow-tooling`, `mcp-server` |  |
