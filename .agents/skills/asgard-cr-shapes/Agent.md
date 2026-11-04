# Agent

`asgard-ai.com/v1alpha1`, kind `Agent`, plural `agents`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.agentClass` | string | **required** |  | one of `managed` |  |
| `spec.managed` | object | - |  |  | ManagedAgentSpec is the config for a managed Agent. The Agent CR is a capability group (referenced by Plugin.Agents / SandboxBlueprint.Agents / SandboxTemplate.Agents): what one area of work needs — toolsets, skill sets, semantic layers, mounts, a browser — plus the guidance for working in it. It produces no deployment of its own and is not a separate assistant: the agent of every turn that resolves it holds its capabilities directly. |
| `spec.managed.aliasName` | string | **required** |  | matches `^[a-z0-9][a-z0-9\-]*$` | AliasName is the handle a user writes as @<aliasName> to point at this capability, and the key two references to the same agent are deduped on. |
| `spec.managed.browser` | object | - |  |  | Browser, when enabled, forces the sandbox browser sidecar ON when this agent is among a SandboxBlueprint's resolved agents (OR-aggregated: a blueprint "browser off" is not authoritative once a resolved agent requests it). |
| `spec.managed.browser.enabled` | boolean | **required** |  |  |  |
| `spec.managed.description` | string | **required** |  |  | Description is what this capability covers. It is shown to the agent that holds the capability (and in UIs), so describe the area of work rather than writing an instruction to hand work to someone. It need not name the tools: the platform lists, next to it, the tools, skills and semantic models this capability brings, by the names the agent calls them. |
| `spec.managed.prompt` | object | **required** |  |  | AgentPrompt is a capability's guidance — shown to the agent that holds it, alongside the Description. Every part may be empty: an Agent that only brings tools or data needs none of them. |
| `spec.managed.prompt.context` | string | **required** |  |  |  |
| `spec.managed.prompt.format` | string | **required** |  |  |  |
| `spec.managed.prompt.persona` | string | **required** |  |  |  |
| `spec.managed.prompt.task` | string | **required** |  |  |  |
| `spec.managed.sampleQuestions` | array | - |  |  | SampleQuestions are typical requests this capability handles. |
| `spec.managed.semanticLayers` | array | - |  |  | SemanticLayers this capability brings. They merge into the holding agent's run-total set (OR-merged by name with every other source) — there is no per-agent narrowing — and are listed by name as this capability's own. |
| `spec.managed.semanticLayers[].allowQuery` | boolean | - |  |  |  |
| `spec.managed.semanticLayers[].allowWrite` | boolean | - |  |  |  |
| `spec.managed.semanticLayers[].allowedCubes` | array | - |  |  |  |
| `spec.managed.semanticLayers[].name` | string | **required** |  |  |  |
| `spec.managed.skillSetNames` | array | - |  |  | SkillSetNames this capability brings; merged into the sandbox of the agent that holds it (deduped with other agents/plugins/blueprint). The skills found in them are listed by name as this capability's own. |
| `spec.managed.sourceSetMounts` | array | - |  |  | SourceSetMounts this capability needs mounted into the shared sandbox pod. Mirrors Plugin.spec.sourceSetMounts; merged into the holding agent's sandbox (deduped by mountPath with other agents/plugins/blueprint — first wins, Plugin ≻ Agent ≻ Blueprint). |
| `spec.managed.sourceSetMounts[].mountPath` | string | **required** |  | matches `^/.+` |  |
| `spec.managed.sourceSetMounts[].readOnly` | boolean | **required** |  |  |  |
| `spec.managed.sourceSetMounts[].sourceSetName` | string | **required** |  | matches `^[a-z0-9][a-z0-9\-]*$` |  |
| `spec.managed.sourceSetMounts[].subPath` | string | - |  |  |  |
| `spec.managed.toolsetNames` | array | - |  |  | ToolsetNames this capability brings; merged into the holding agent's tools, and their tools are listed by name as this capability's own. |
