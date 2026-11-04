# SandboxBlueprint

`asgard-ai.com/v1alpha1`, kind `SandboxBlueprint`, plural `sandboxblueprints`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  | Each top-level field is a ValueExprTemplate (value \| expression \| template), allowing dynamic evaluation against the request context (vars, payload). Lists/JSON encoded fields (sourceSetMounts, hooks) carry a JSON string in 'value' that bpcontroller unmarshals after evaluation. |
| `spec.agents` | object | - |  |  | Agents evaluates to a JSON-string array of SandboxBlueprintAgent. Each entry contributes one capability group, in one of two mutually-exclusive modes: reference an existing Agent CR via baseAgentName (and optionally layer overrides), or define an inline agent from scratch via aliasName (no Agent CR — the override fields are its full definition). Resolved agents are not separate assistants: their (override-merged) skillSets/toolsets/ sourceSetMounts/semanticLayers merge into the sandbox's agent, which also receives their description and prompt. See SandboxBlueprintAgent. |
| `spec.agents.expression` | string | - |  |  |  |
| `spec.agents.template` | string | - |  |  |  |
| `spec.agents.value` | string | - |  |  |  |
| `spec.browser` | object | - |  |  | Browser holds the browser-sidecar (Neko) related settings. |
| `spec.browser.enabled` | object | - |  |  | Enabled evaluates to "true" or "false". Default false when omitted. When true the Sandbox pod gains a Neko browser sidecar (headed Chromium streamed over WebRTC, automatable over CDP). Additional config will be added later. NOTE: a "false"/absent value is NOT authoritative when Agents resolves to agents — if any resolved Agent enables Browser, the sandbox opens the browser regardless (OR-aggregation in bpcontroller's evaluateBlueprintTemplate). |
| `spec.browser.enabled.expression` | string | - |  |  |  |
| `spec.browser.enabled.template` | string | - |  |  |  |
| `spec.browser.enabled.value` | string | - |  |  |  |
| `spec.credentialMounts` | object | - |  |  | CredentialMounts evaluates to a JSON-string array of SandboxCredentialMount. |
| `spec.credentialMounts.expression` | string | - |  |  |  |
| `spec.credentialMounts.template` | string | - |  |  |  |
| `spec.credentialMounts.value` | string | - |  |  |  |
| `spec.editorServer` | object | - |  |  | EditorServer holds the editor-sidecar related settings. |
| `spec.editorServer.enabled` | object | - |  |  | Enabled evaluates to "true" or "false". Default false when omitted. |
| `spec.editorServer.enabled.expression` | string | - |  |  |  |
| `spec.editorServer.enabled.template` | string | - |  |  |  |
| `spec.editorServer.enabled.value` | string | - |  |  |  |
| `spec.editorServer.initCommand` | object | - |  |  | InitCommand evaluates to a shell script that runs before code-server starts. Mounted at /entrypoint.d/init.sh on the editor container with mode 0755. |
| `spec.editorServer.initCommand.expression` | string | - |  |  |  |
| `spec.editorServer.initCommand.template` | string | - |  |  |  |
| `spec.editorServer.initCommand.value` | string | - |  |  |  |
| `spec.editorServer.workingDirectory` | object | - |  |  | WorkingDirectory evaluates to an absolute path. |
| `spec.editorServer.workingDirectory.expression` | string | - |  |  |  |
| `spec.editorServer.workingDirectory.template` | string | - |  |  |  |
| `spec.editorServer.workingDirectory.value` | string | - |  |  |  |
| `spec.extraDirectories` | object | - |  |  | ExtraDirectories evaluates to a JSON-string array of absolute paths that belong to this agent's workspace alongside WorkingDirectory. Each one is handed to the CLI as an additional working directory AND scanned for the project instructions file, whose contents are folded into the system prompt — so a directory mounted here can carry durable instructions of its own, not just files to be read on request. That second half is the whole point. The CLI grants tool access to an additional directory but never loads instruction files from it, so naming a path in a prompt is the weakest form of guidance available; the platform reads the file itself, exactly as it already does for WorkingDirectory. Order carries meaning. The instruction blocks are emitted in this order and WorkingDirectory's own block comes last, so a per-user workspace overrides whatever an extra directory establishes — put the most general first. |
| `spec.extraDirectories.expression` | string | - |  |  |  |
| `spec.extraDirectories.template` | string | - |  |  |  |
| `spec.extraDirectories.value` | string | - |  |  |  |
| `spec.hooks` | object | - |  |  | Hooks evaluates to a JSON-string array of SandboxHook. |
| `spec.hooks.expression` | string | - |  |  |  |
| `spec.hooks.template` | string | - |  |  |  |
| `spec.hooks.value` | string | - |  |  |  |
| `spec.pluginNames` | object | - |  |  | PluginNames evaluates to a comma-separated list of Plugin names. |
| `spec.pluginNames.expression` | string | - |  |  |  |
| `spec.pluginNames.template` | string | - |  |  |  |
| `spec.pluginNames.value` | string | - |  |  |  |
| `spec.skillSetNames` | object | - |  |  | SkillSetNames evaluates to a comma-separated list of SkillSet names. |
| `spec.skillSetNames.expression` | string | - |  |  |  |
| `spec.skillSetNames.template` | string | - |  |  |  |
| `spec.skillSetNames.value` | string | - |  |  |  |
| `spec.sourceSetMounts` | object | - |  |  | SourceSetMounts evaluates to a JSON-string array of SandboxSourceSetMount. |
| `spec.sourceSetMounts.expression` | string | - |  |  |  |
| `spec.sourceSetMounts.template` | string | - |  |  |  |
| `spec.sourceSetMounts.value` | string | - |  |  |  |
| `spec.toolsetNames` | object | - |  |  | ToolsetNames evaluates to a comma-separated list of Toolset names. |
| `spec.toolsetNames.expression` | string | - |  |  |  |
| `spec.toolsetNames.template` | string | - |  |  |  |
| `spec.toolsetNames.value` | string | - |  |  |  |
| `spec.workingDirectory` | object | - |  |  | WorkingDirectory evaluates to the CLI working directory (absolute path). Distinct from EditorServer.WorkingDirectory (which is editor-relative). |
| `spec.workingDirectory.expression` | string | - |  |  |  |
| `spec.workingDirectory.template` | string | - |  |  |  |
| `spec.workingDirectory.value` | string | - |  |  |  |
