# Sandbox

`asgard-ai.com/v1alpha1`, kind `Sandbox`, plural `sandboxes`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.dataSubPath` | string | **required** |  | matches `^[^/].*[^/]$\|^[^/]$` | DataSubPath is the relative sub-path appended to the reconciler-managed "namespace/<ns>/" prefix when mounting the agent-sandbox PVC. The reconciler treats it as opaque and only validates that it is non-empty and has no leading or trailing "/", and does not contain "..". Callers (e.g. bpcontroller) typically encode their own domain identifiers here, e.g. "bot-provider/<bp>/channel/<id>". |
| `spec.sandboxTemplate` | object | **required** |  |  | SandboxTemplate is the fully-resolved capability set. |
| `spec.sandboxTemplate.agents` | array | - |  |  | Agents whose capabilities were merged into this sandbox (observability — the sandbox reconciler does not read it). Names only (aliasName); their description and prompt reach the agent via the task static config. |
| `spec.sandboxTemplate.agents[].name` | string | **required** |  | matches `^[a-z0-9][a-z0-9\-]*$` |  |
| `spec.sandboxTemplate.browser` | object | - |  |  | SandboxTemplateBrowser is the resolved browser-sidecar (Neko) settings. Only Enabled is supported for now; further config will be added later. |
| `spec.sandboxTemplate.browser.enabled` | boolean | **required** |  |  |  |
| `spec.sandboxTemplate.credentialMounts` | array | - |  |  |  |
| `spec.sandboxTemplate.credentialMounts[].mountPath` | string | **required** |  | matches `^/.+` | MountPath is the DIRECTORY the credential is projected into; the token lands in it as the file "access_token". A directory rather than a full file path, deliberately: mounting a single file requires a subPath mount, and kubelet never refreshes those — the token would be a one-time copy taken at pod start, defeating the propagation this type exists to guarantee. |
| `spec.sandboxTemplate.credentialMounts[].oAuthCredentialName` | string | **required** |  | matches `^[a-z0-9][a-z0-9\-]*$` | OAuthCredentialName is the OAuthCredential in the Sandbox's namespace whose access token to project. |
| `spec.sandboxTemplate.editorServer` | object | **required** |  |  |  |
| `spec.sandboxTemplate.editorServer.enabled` | boolean | **required** |  |  |  |
| `spec.sandboxTemplate.editorServer.initCommand` | string | - |  |  | InitCommand is the evaluated shell script content. Empty/unset means no init. |
| `spec.sandboxTemplate.editorServer.workingDirectory` | string | - |  |  | Path relative to /work (no leading slash); directory where the editor server opens. |
| `spec.sandboxTemplate.extraDirectories` | array | - |  |  | ExtraDirectories are the resolved absolute paths that accompany WorkingDirectory (see SandboxBlueprintSpec.ExtraDirectories). Unlike WorkingDirectory this is optional and routinely empty, so consumers must handle its absence rather than relying on a value being present. The cap is deliberate rather than nominal: every entry costs one file read at the start of every turn plus one more directory grant on the CLI command line, so an unbounded list would degrade turn startup in a way that is hard to attribute back to a blueprint edit. |
| `spec.sandboxTemplate.hooks` | array | - |  |  |  |
| `spec.sandboxTemplate.hooks[].commandHandler` | object | - |  |  |  |
| `spec.sandboxTemplate.hooks[].commandHandler.command` | string | **required** |  |  |  |
| `spec.sandboxTemplate.hooks[].event` | string | **required** |  | one of `session-start`, `session-end`, `user-prompt-submit`, `pre-tool-call`, `post-tool-call` | SandboxHookEvent names WHEN a hook fires. The event is the interface; WHICH component executes the hook (sandbox entrypoint, processor driver, or a future CLI delegation) is an asgard-core routing decision that stays out of this API, so an event can change executor without a CRD change. Names borrow the Claude CLI hook vocabulary (kebab-cased) where the concepts match. Deprecated values: "pre-tool-call" and "post-tool-call" are accepted by the schema and DO NOTHING. Nothing executes them - they were planned as driver scripts, the runners were never built, and asgard-core has no executor for them. A hook declaring either applies cleanly and never fires. They remain valid only so existing CRs stay readable; do not write new ones. **The deprecation is stated here, on the type, and not only on the constants below.** A CRD schema carries `enum: [...]` with no per-value description, so a doc comment on a constant reaches nothing - controller-gen copies THIS comment into the description of every field typed SandboxHookEvent, and that description is the only place a reader (or an agent reading the extracted CR shapes) can be told. `make lint` enforces it. |
| `spec.sandboxTemplate.hooks[].handlerType` | string | **required** |  | one of `command` |  |
| `spec.sandboxTemplate.skillSets` | array | - |  |  |  |
| `spec.sandboxTemplate.skillSets[].name` | string | **required** |  | matches `^[a-z0-9][a-z0-9\-]*$` |  |
| `spec.sandboxTemplate.sourceSetMounts` | array | - |  |  |  |
| `spec.sandboxTemplate.sourceSetMounts[].mountPath` | string | **required** |  | matches `^/.+` |  |
| `spec.sandboxTemplate.sourceSetMounts[].readOnly` | boolean | **required** |  |  |  |
| `spec.sandboxTemplate.sourceSetMounts[].sourceSetName` | string | **required** |  | matches `^[a-z0-9][a-z0-9\-]*$` |  |
| `spec.sandboxTemplate.sourceSetMounts[].subPath` | string | - |  |  |  |
| `spec.sandboxTemplate.toolsets` | array | - |  |  |  |
| `spec.sandboxTemplate.toolsets[].name` | string | **required** |  | matches `^[a-z0-9][a-z0-9\-]*$` |  |
| `spec.sandboxTemplate.workingDirectory` | string | **required** |  | matches `^/.+` | WorkingDirectory is the resolved CLI working directory (absolute path). bpcontroller always resolves this at evaluation time (defaults to /work), so it is always present and non-empty — a required field, consumers can rely on it. |
