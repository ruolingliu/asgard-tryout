# SkillSet

`asgard-ai.com/v1alpha1`, kind `SkillSet`, plural `skillsets`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.searchPaths` | array | - |  |  | List of paths within the SourceSet to look for SKILL.md files recursively. If omitted or empty, the entire SourceSet volume is searched. |
| `spec.sourceSetName` | string | **required** |  | matches `^[a-z0-9][a-z0-9\-]*$` | Name of the SourceSet where skills files live. Must match an existing SourceSet. |
