# SemanticLayer

`asgard-ai.com/v1alpha1`, kind `SemanticLayer`, plural `semanticlayers`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.completionModelName` | string | **required** |  |  | CompletionModelName is the name of the CompletionModel CR (in the same namespace) this semantic layer uses for its chat/parameterize workflows. Typically one of the namespace's builtin models (e.g. preset-balanced). |
| `spec.cubes` | array | **required** |  |  | Cubes may be empty. An empty layer is the starting point of the interactive modeling flow: the platform creates the SemanticLayer up front (name + data connector + completion model) and a modeling agent fills in the cubes afterwards. A cube-less layer simply answers nothing; each cube that IS present must still be fully valid. |
| `spec.cubes[].description` | string | **required** |  |  |  |
| `spec.cubes[].dimensions` | array | **required** |  |  |  |
| `spec.cubes[].dimensions[].description` | string | **required** |  |  |  |
| `spec.cubes[].dimensions[].format` | string | - |  | one of `link`, `currency`, `percent` |  |
| `spec.cubes[].dimensions[].name` | string | **required** |  |  |  |
| `spec.cubes[].dimensions[].sql` | string | **required** |  |  |  |
| `spec.cubes[].dimensions[].subQuery` | string | - |  |  |  |
| `spec.cubes[].dimensions[].title` | string | **required** |  |  |  |
| `spec.cubes[].dimensions[].type` | string | **required** |  | one of `string`, `time`, `boolean`, `number` |  |
| `spec.cubes[].measures` | array | **required** |  |  |  |
| `spec.cubes[].measures[].description` | string | **required** |  |  |  |
| `spec.cubes[].measures[].drillMembers` | array | - |  |  |  |
| `spec.cubes[].measures[].filters` | array | - |  |  |  |
| `spec.cubes[].measures[].filters[].sql` | string | **required** |  |  |  |
| `spec.cubes[].measures[].format` | string | - |  | one of `currency`, `percent` |  |
| `spec.cubes[].measures[].name` | string | **required** |  |  |  |
| `spec.cubes[].measures[].sql` | string | - |  |  |  |
| `spec.cubes[].measures[].title` | string | **required** |  |  |  |
| `spec.cubes[].measures[].type` | string | **required** |  | one of `string`, `time`, `boolean`, `number`, `number_agg`, `count`, `count_distinct`, `count_distinct_approx`, `sum`, `avg`, `min`, `max` |  |
| `spec.cubes[].name` | string | **required** |  |  |  |
| `spec.cubes[].primaryKeyDimensions` | array | - |  |  |  |
| `spec.cubes[].sql` | string | - |  |  |  |
| `spec.cubes[].sqlTable` | string | - |  |  |  |
| `spec.cubes[].title` | string | - |  |  |  |
| `spec.dataConnectorName` | string | **required** |  |  |  |
| `spec.effort` | string | - |  | one of `low`, `medium`, `high`, `xhigh`, `max`, `auto`, `disabled` | Effort is the reasoning depth the semantic layer's LLM processors run at. Same value domain as the llm-completion / stream-llm-completion-message processors' `effort` config. Unset means the processors carry no effort config at all, so the model applies its own default. |
| `spec.instruction` | string | - |  |  |  |
| `spec.joins` | array | **required** |  |  |  |
| `spec.joins[].description` | string | **required** |  |  |  |
| `spec.joins[].from` | object | **required** |  |  |  |
| `spec.joins[].from.cube` | string | **required** |  |  |  |
| `spec.joins[].from.dimensions` | array | **required** |  |  |  |
| `spec.joins[].name` | string | **required** |  |  |  |
| `spec.joins[].relationship` | string | **required** |  | one of `one_to_one`, `one_to_many`, `many_to_one` |  |
| `spec.joins[].to` | object | **required** |  |  |  |
| `spec.joins[].to.cube` | string | **required** |  |  |  |
| `spec.joins[].to.dimensions` | array | **required** |  |  |  |
| `spec.locale` | string | **required** |  |  |  |
| `spec.pluginNames` | array | - |  |  | PluginNames lists Plugin CRs (in the same namespace) whose capabilities (skillSets, toolsets, sourceSetMounts, hooks) are injected into the semantic layer's chat workflow main agent via a reconciler-owned SandboxBlueprint. Mirrors Agent's spec.managed.pluginNames. |
| `spec.sampleQueries` | array | - |  |  |  |
| `spec.sampleQueries[].comment` | string | **required** |  |  |  |
| `spec.sampleQueries[].sql` | string | **required** |  |  |  |
| `spec.sampleQuestions` | array | - |  |  |  |
| `spec.summary` | string | - |  |  |  |
| `spec.timezone` | string | **required** |  |  |  |
| `spec.toolsetNames` | array | - |  |  |  |
