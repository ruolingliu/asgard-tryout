# SourceSetEditorServer

`asgard-ai.com/v1alpha1`, kind `SourceSetEditorServer`, plural `sourceseteditorservers`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.sourceSetName` | string | **required** |  | matches `^[a-z0-9][a-z0-9\-]*$` | Name of the SourceSet whose volume will be mounted into the editor. |
| `spec.workingDirectoryPath` | string | - |  | matches `^[^/].*/$` | Optional relative subdirectory inside the SourceSet volume to mount as the editor workspace. Must not start with '/' and must end with '/'. Path traversal ('..') and absolute paths are rejected by Kubernetes SubPath validation at Deployment creation time. Leave unset to use the volume root. |
