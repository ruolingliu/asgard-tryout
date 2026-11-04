# Plugin

`asgard-ai.com/v1alpha1`, kind `Plugin`, plural `plugins`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.agents` | array | - |  |  | Agents referenced by this plugin; their skillSets/toolsets/semanticLayers merge into the agent of the sandbox, as with SandboxBlueprint.Agents. |
| `spec.agents[].name` | string | **required** |  | matches `^[a-z0-9][a-z0-9\-]*$` |  |
| `spec.hooks` | array | - |  |  | Lifecycle hooks executed inside the Sandbox container. |
| `spec.hooks[].commandHandler` | object | - |  |  |  |
| `spec.hooks[].commandHandler.command` | string | **required** |  |  |  |
| `spec.hooks[].event` | string | **required** |  | one of `session-start`, `session-end`, `user-prompt-submit`, `pre-tool-call`, `post-tool-call` | SandboxHookEvent names WHEN a hook fires. The event is the interface; WHICH component executes the hook (sandbox entrypoint, processor driver, or a future CLI delegation) is an asgard-core routing decision that stays out of this API, so an event can change executor without a CRD change. Names borrow the Claude CLI hook vocabulary (kebab-cased) where the concepts match. Deprecated values: "pre-tool-call" and "post-tool-call" are accepted by the schema and DO NOTHING. Nothing executes them - they were planned as driver scripts, the runners were never built, and asgard-core has no executor for them. A hook declaring either applies cleanly and never fires. They remain valid only so existing CRs stay readable; do not write new ones. **The deprecation is stated here, on the type, and not only on the constants below.** A CRD schema carries `enum: [...]` with no per-value description, so a doc comment on a constant reaches nothing - controller-gen copies THIS comment into the description of every field typed SandboxHookEvent, and that description is the only place a reader (or an agent reading the extracted CR shapes) can be told. `make lint` enforces it. |
| `spec.hooks[].handlerType` | string | **required** |  | one of `command` |  |
| `spec.skillSets` | array | - |  |  | SkillSets exposed by this plugin (referenced by name). |
| `spec.skillSets[].name` | string | **required** |  | matches `^[a-z0-9][a-z0-9\-]*$` |  |
| `spec.sourceSetMounts` | array | - |  |  | SourceSet volume mounts to inject into the Sandbox pod. |
| `spec.sourceSetMounts[].mountPath` | string | **required** |  | matches `^/.+` |  |
| `spec.sourceSetMounts[].readOnly` | boolean | **required** |  |  |  |
| `spec.sourceSetMounts[].sourceSetName` | string | **required** |  | matches `^[a-z0-9][a-z0-9\-]*$` |  |
| `spec.sourceSetMounts[].subPath` | string | - |  |  |  |
| `spec.toolsets` | array | - |  |  | Toolsets exposed by this plugin (referenced by name). |
| `spec.toolsets[].name` | string | **required** |  | matches `^[a-z0-9][a-z0-9\-]*$` |  |
