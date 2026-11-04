---
name: asgard-workflow-processors
description: The Workflow processor catalogue this Asgard server enforces - every processor type, its static config keys, their types, which are required, what they default to, and which relationships it can emit. Read it before writing or editing a Workflow CR's nodes or relationships.
version: 13
alwaysApply: false
---

# Workflow processors

13 processor types, 30 required config keys between them.

**Generated from the server this repository deploys to. Do not edit it** - the
next `asgard-cli skill update` overwrites it, and an edit here is a claim about
the server that the server did not make.

It is generated because it has to describe *your* server. Asgard runs as a
hosted platform and on-prem, and a document saying what `llm-completion` takes
is only true of the version it was taken from. This came from the one your runs
deploy against.

**What is here and what is not.** This is shape: names, types, requiredness,
defaults. It is not judgement - which mistakes apply cleanly and fail at
runtime, what a wrong name costs - and it will not tell you a design is wrong.
That is what the hand-written skills beside it are for.

## How to read it

- **config key** is what goes under a node's `staticConfigs`, spelled exactly.
- **required** means the runtime refuses the Workflow without it. A missing
  optional key takes the default in the next column.
- **default** is typed: `false` is a boolean, `20` is a number, `""` is an empty
  string, and `null` means there is no default at all - which is not the same
  as defaulting to empty.
- **dynamic config** says whether keys outside this table are accepted, and the
  type every one of them must take. Where the processor reads particular extra
  keys, a second table says which, in the form a Workflow writes them: `<n>`
  is a position and `<name>` a name you choose.
- **deprecated** marks a processor that still runs and that a new Workflow
  should not add. It says what replaces it, and the deprecated processors are
  listed last.
- **relationships** are the `relationName` values a relationship may use to leave
  a node of this type. A relationship naming anything else does not run.

## The processors

- [`execute-script`](#execute-script) - Execute a script and mutate context payload.
- [`generate-embedding`](#generate-embedding) - Generate text embedding.
- [`http-request`](#http-request) - Send an HTTP request.
- [`listen-message`](#listen-message) - Listen to the message from the channel.
- [`llm-completion`](#llm-completion) - Generate completion using the language model.
- [`llm-query-database`](#llm-query-database) - Query the database with natural language using the language model.
- [`push-message`](#push-message) - Push a message to the channel.
- [`query-database`](#query-database) - Query the database.
- [`retrieve-knowledge`](#retrieve-knowledge) - Retrieve knowledge from the knowledge base.
- [`router`](#router) - Route the message to the corresponding processor.
- [`stream-llm-completion-message`](#stream-llm-completion-message) - Stream completion message using the language model.
- [`update-context`](#update-context) - Update the context.
- [`validate-payload`](#validate-payload) - **deprecated** - Validate the payload using the JSON schema (Draft 2020-12).

## `execute-script`

Execute a script and mutate context payload.

| config key | type | required | default | what it is |
|---|---|---|---|---|
| `engine` | string | **required** | `null` | The script engine to use. (Value: ECMA5) |
| `script` | string | **required** | `null` | The script to execute. |

Dynamic config: **not accepted**. A key outside the table above is an error.
Relationships: `success`. No others.

## `generate-embedding`

Generate text embedding.

| config key | type | required | default | what it is |
|---|---|---|---|---|
| `embeddingModel` | string | **required** | `null` | The name of the embedding model. |
| `input` | string | **required** | `null` | The input text to generate the embedding. |
| `resultField` | string | **required** | `null` | The field name of the result. A float array which represents the embedding will be stored in this field. |

Dynamic config: **not accepted**. A key outside the table above is an error.
Relationships: `failure`, `success`. No others.

## `http-request`

Send an HTTP request.

| config key | type | required | default | what it is |
|---|---|---|---|---|
| `method` | string | **required** | `null` | The method of the request. |
| `parseJson` | boolean | **required** | `false` | Parse the response body as JSON. |
| `url` | string | **required** | `null` | The URL of the request. |
| `body` | any | - | `null` | The body of the request. |

Dynamic config: accepted, any type.

| dynamic key | type | what it is |
|---|---|---|
| `<name>` | string | One HTTP request header. The key is the header name. The value must be a string; any other type fails the step at run time. |

Relationships: `success`. No others.

## `listen-message`

Listen to the message from the channel.

No static config keys.

Dynamic config: **not accepted**. A key outside the table above is an error.
Relationships: none. Nothing leaves a node of this type. No others.

## `llm-completion`

Generate completion using the language model.

| config key | type | required | default | what it is |
|---|---|---|---|---|
| `completionModel` | string | **required** | `null` | The name of the completion model. |
| `outputSchema` | string | **required** | `null` | The json schema of the output. |
| `prompt` | string | **required** | `null` | The prompt for the model. Provide some background information and necessary context for data supplementation. (The output format should be config by the input schema of the success relation.) |
| `blobs` | string | - | `null` | The comma-separated blob IDs that the model can access. (Optional) |
| `effort` | string | - | `null` | Reasoning effort for the turn: one of low, medium, high, xhigh, max (or auto = model default). Controls thinking depth and overall token spend. Not every model supports every level, and one it does not support fails the turn — set `disabled` for a model that rejects the reasoning-effort parameter outright, which stops it being sent at all (every builtin preset accepts every level). Unset = model default. (Optional) |
| `executionMode` | string | - | `"agent"` | How this node runs: `agent` (default) or `direct`. `agent` runs an AI agent in the channel sandbox and can use tools, skills, semantic layers and a sandboxBlueprint. `direct` skips the sandbox and makes a single model call with only the prompt, the attached files and outputSchema — much faster to start, for tasks like classifying an image, transcribing audio or rewriting text. In `direct` mode toolsets, semanticLayers, semanticLayers.preQueries, semanticLayer and sandboxBlueprint must be empty, effort may only be unset, auto or disabled, and outputSchema must describe an object; attachments may be images (jpeg/png/gif/webp), PDF, text (txt/csv/md/json/xml/yaml/html) or audio (wav/mp3/m4a/aac/ogg/flac/aiff/webm), up to 20 MiB in total, and audio needs a model that accepts it (e.g. preset-vision). The workspace AGENTS.md is not read in `direct` mode. A result that does not match outputSchema is retried once. (Optional) |
| `maxTokens` | integer | - | `null` | Max output tokens per turn. Optional — maps to the CLI's CLAUDE_CODE_MAX_OUTPUT_TOKENS and is clamped to the model's upper limit; unset = model default. Small values truncate output. (Optional) |
| `openai.webSearch.enabled` | boolean | - | `false` | Whether to enable OpenAI web search. (Optional) |
| `openai.webSearch.searchContextSize` | string | - | `"medium"` | Controls how much context is retrieved from the web to help the tool formulate a response. Available options are: 'low', 'medium', 'high'. (Optional) |
| `sandboxBlueprint` | string | - | `""` | Name of the SandboxBlueprint to materialize a Sandbox for this LLM call. When set, bpcontroller ensures the Sandbox is Ready before sendTask, and the LLM gains sandbox-bound builtin tools (bash, str_replace_editor) plus discovered Skills in the system prompt. (Optional) |
| `semanticLayer` | string | - | `null` | The semantic layer name to attach to the model. (Deprecated: use semanticLayers instead. Optional) |
| `semanticLayer.allowQuery` | boolean | - | `false` | Whether to allow the model to query the semantic layer. (Deprecated: use semanticLayers instead. Optional) |
| `semanticLayer.allowWrite` | boolean | - | `true` | Whether to allow the model to write to the database of semantic layer. (Deprecated: use semanticLayers instead. Optional) |
| `semanticLayer.allowedCubes` | string | - | `""` | The comma-separated cube names that the model can access. (Deprecated: use semanticLayers instead. Optional) |
| `semanticLayers` | any | - | `null` | JSON array of semantic layers. Each element: {"name": "<CR name>", "allowQuery": bool, "allowWrite": bool, "allowedCubes": ["...", ...]}. Supports multiple databases per LLM call. (Optional) |
| `semanticLayers.preQueries` | any | - | `null` | JSON object mapping a DataConnector name to the pre-queries run before every semantic layer data-tool query sent to that connector, in order, on the same connection and transaction. Each pre-query: {"sql": "<one statement with the connector's placeholders>", "arguments": [{"type": "<config type>", "value": <value>}, ...]}. Bind values through arguments; never write them into sql. Supported for postgres, mysql, mssql, oracle and hana connectors. A database that scopes access by these settings must deny access when they are absent: table listings, table data previews, connection checks and Core versions without pre-query support query without them. (Optional) |
| `toolsets` | string | - | `null` | The comma-separated toolset names that the model can use. (Optional) |

Dynamic config: accepted, every value must be `string`.
Relationships: `failure`, `success`. No others.

## `llm-query-database`

Query the database with natural language using the language model.

| config key | type | required | default | what it is |
|---|---|---|---|---|
| `completionModel` | string | **required** | `null` | The name of the completion model to use for the query. |
| `maxTokens` | integer | **required** | `null` | The maximum number of tokens generated. |
| `query` | string | **required** | `null` | The natural language query to be converted to SQL. |
| `resultField` | string | **required** | `null` | The field name of the result. The result will be a JSON object containing the query results and the SQL query. |
| `semanticLayer` | string | **required** | `null` | The semantic layer to use for the query. |
| `temperature` | number | - | `null` | The temperature of the model. (Optional) |

Dynamic config: **not accepted**. A key outside the table above is an error.
Relationships: `failure`, `success`. No others.

## `push-message`

Push a message to the channel.

| config key | type | required | default | what it is |
|---|---|---|---|---|
| `flush` | boolean | **required** | `false` | Flush the reply buffer immediately. |
| `isDebug` | boolean | **required** | `false` | A flag to indicate whether the message is for debugging purposes. (Optional) |
| `message` | string | **required** | `""` | The message to push. |
| `payload` | any | - | `null` | Additional payload data (such as metadata) to push. (Optional) |
| `template` | any | - | `null` | Message template (Optional) |

Dynamic config: **not accepted**. A key outside the table above is an error.
Relationships: `success`. No others.

## `query-database`

Query the database.

| config key | type | required | default | what it is |
|---|---|---|---|---|
| `dataConnector` | string | **required** | `null` | The data connector to use. |
| `resultField` | string | **required** | `null` | The field name of the result. |
| `sql` | string | **required** | `null` | The SQL query to execute, written with placeholders. Bind request data through sql.args.<n>.type and sql.args.<n>.value; never write it into this text. |
| `allowWrite` | boolean | - | `true` | Whether to allow write operations (INSERT, UPDATE, DELETE, DDLs). (Optional, default: true) |
| `allowedTables` | string | - | `""` | The comma-separated table names that are allowed to be accessed. (Optional) |
| `preQueries` | any | - | `null` | JSON array of pre-queries run before the query, in order, on the same connection and transaction. Each pre-query: {"sql": "<one statement with the connector's placeholders>", "arguments": [{"type": "<config type>", "value": <value>}, ...]}. Bind values through arguments; never write them into sql. Supported for postgres, mysql, mssql, oracle and hana connectors. A database that scopes access by these settings must deny access when they are absent: table listings, table data previews, connection checks and Core versions without pre-query support query without them. (Optional) |

Dynamic config: accepted, any type.

| dynamic key | type | what it is |
|---|---|---|
| `sql.args.<n>.type` | string | The type the n-th bound argument is converted to: string, integer, number, boolean or any. Pairs with sql.args.<n>.value; numbered from 1 and read until the first gap. |
| `sql.args.<n>.value` | any | The n-th bound argument, usually an expression reading the payload. It is passed to the database as a prepared statement's argument and cannot change the statement, so request data belongs here and never in sql itself: an expression or a template that writes it into sql runs whatever the caller sends. In sql, the n-th argument is written, by the DataConnector's class: athena ?; hana ?; mssql @p1, @p2; mysql ?; netsuite :1, :2; oracle :p1, :p2; postgres $1, $2; salesforce $1, $2; trino ?. |

Relationships: `success`. No others.

## `retrieve-knowledge`

Retrieve knowledge from the knowledge base.

| config key | type | required | default | what it is |
|---|---|---|---|---|
| `knowledgeBases` | string | **required** | `null` | The comma-separated knowledge bases name to retrieve. |
| `resultField` | string | **required** | `null` | The field name of the result. |
| `sampleK` | integer | **required** | `20` | The number of samples to retrieve from the indexed data and their enhancement data. |
| `similarityThreshold` | number | **required** | `null` | The similarity threshold to filter the results. |
| `textQuery` | string | **required** | `null` | The text query to retrieve the knowledge. |
| `filterTags` | string | - | `null` | Common separated tags to filter the results. (Optional) |

Dynamic config: accepted, every value must be `string`.

| dynamic key | type | what it is |
|---|---|---|
| `path.<n>.exists` | string | A JSON path a chunk's metadata must contain to be returned. Numbered from 0 and read until the first gap. |
| `path.<n>.predicate` | string | A JSON path predicate a chunk's metadata must satisfy to be returned. Numbered from 0, counted separately from path.<n>.exists, and read until the first gap. |

Relationships: `success`. No others.

## `router`

Route the message to the corresponding processor.

No static config keys.

Dynamic config: accepted, every value must be `boolean`.

| dynamic key | type | what it is |
|---|---|---|
| `<name>` | boolean | One branch. The key is the relationName a relationship leaving this node uses, and the value is a boolean, or a string that parses as one, usually an expression. Branches are tried in the order they are declared and the first true one is taken; when none is, the else relationship is. |

Relationships: `else`, plus dynamic ones.

## `stream-llm-completion-message`

Stream completion message using the language model.

| config key | type | required | default | what it is |
|---|---|---|---|---|
| `completionModel` | string | **required** | `null` | The name of the completion model. |
| `isDebug` | boolean | **required** | `false` | A flag to indicate whether the message is for debugging purposes. (Optional) |
| `blobs` | string | - | `null` | The comma-separated blob IDs that the model can access. (Optional) |
| `effort` | string | - | `null` | Reasoning effort for the turn: one of low, medium, high, xhigh, max (or auto = model default). Controls thinking depth and overall token spend. Not every model supports every level, and one it does not support fails the turn — set `disabled` for a model that rejects the reasoning-effort parameter outright, which stops it being sent at all (every builtin preset accepts every level). Unset = model default. (Optional) |
| `input` | string | - | `null` | The user message for this turn. Optional — when omitted, the processor uses the channel's incoming message (context prevMessage). |
| `maxTokens` | integer | - | `null` | Max output tokens per turn. Optional — maps to the CLI's CLAUDE_CODE_MAX_OUTPUT_TOKENS and is clamped to the model's upper limit; unset = model default. Small values truncate output. (Optional) |
| `openai.webSearch.enabled` | boolean | - | `false` | Whether to enable OpenAI web search. (Optional) |
| `openai.webSearch.searchContextSize` | string | - | `"medium"` | Controls how much context is retrieved from the web to help the tool formulate a response. Available options are: 'low', 'medium', 'high'. (Optional) |
| `prompt` | string | - | `null` | The system prompt (persona) for the agent. Provides stable background, role, and output-requirement instructions — it must NOT contain the per-turn user message or conversation history (history is loaded natively by the CLI --resume). Appended to the Claude Code system preset. Optional: when absent, no persona is appended and the CLI runs with its default preset (unlike llm-completion, `prompt` here is NOT the turn's user message — that comes from `input`). |
| `sandboxBlueprint` | string | - | `""` | Name of the SandboxBlueprint to materialize a Sandbox for this LLM call. When set, bpcontroller ensures the Sandbox is Ready before sendTask, and the LLM gains sandbox-bound builtin tools (bash, str_replace_editor) plus discovered Skills in the system prompt. (Optional) |
| `semanticLayer` | string | - | `null` | The semantic layer name to attach to the model. (Deprecated: use semanticLayers instead. Optional) |
| `semanticLayer.allowQuery` | boolean | - | `false` | Whether to allow the model to query the semantic layer. (Deprecated: use semanticLayers instead. Optional) |
| `semanticLayer.allowWrite` | boolean | - | `true` | Whether to allow the model to write to the database of semantic layer. (Deprecated: use semanticLayers instead. Optional) |
| `semanticLayer.allowedCubes` | string | - | `""` | The comma-separated cube names that the model can access. (Deprecated: use semanticLayers instead. Optional) |
| `semanticLayers` | any | - | `null` | JSON array of semantic layers. Each element: {"name": "<CR name>", "allowQuery": bool, "allowWrite": bool, "allowedCubes": ["...", ...]}. Supports multiple databases per LLM call. (Optional) |
| `semanticLayers.dataVisualization` | boolean | - | `false` | Opt-in. When true and at least one semantic layer is configured, the LLM gains two extra tools (show_result_set_table, show_vega_visualization) to render the most recent query result as a UI table or Vega v5 chart. (Optional) |
| `semanticLayers.preQueries` | any | - | `null` | JSON object mapping a DataConnector name to the pre-queries run before every semantic layer data-tool query sent to that connector, in order, on the same connection and transaction. Each pre-query: {"sql": "<one statement with the connector's placeholders>", "arguments": [{"type": "<config type>", "value": <value>}, ...]}. Bind values through arguments; never write them into sql. Supported for postgres, mysql, mssql, oracle and hana connectors. A database that scopes access by these settings must deny access when they are absent: table listings, table data previews, connection checks and Core versions without pre-query support query without them. (Optional) |
| `toolsets` | string | - | `null` | The comma-separated toolset names that the model can use. (Optional) |

Dynamic config: **not accepted**. A key outside the table above is an error.
Relationships: `failure`, `success`. No others.

## `update-context`

Update the context.

No static config keys.

Dynamic config: accepted, any type.

| dynamic key | type | what it is |
|---|---|---|
| `<name>` | any | One context variable. The key is the variable's name and the value is what it is set to; later processors read it by that name. |

Relationships: `success`. No others.

## `validate-payload`

**Deprecated.** Use the Workflow entry's inputSchema instead: the platform validates the payload against it before any processor runs, and it is what a model is shown as a tool's parameters. The entry's files replaces file.<n>.type and file.<n>.alias. A Workflow that still has this processor keeps working.

Validate the payload using the JSON schema (Draft 2020-12).

| config key | type | required | default | what it is |
|---|---|---|---|---|
| `schema` | string | **required** | `null` | The JSON schema to validate the payload. |
| `path` | string | - | `"$"` | The json path to the payload to validate. (Optional, default to $ (root)) |

Dynamic config: accepted, every value must be `string`.

| dynamic key | type | what it is |
|---|---|---|
| `file.<n>.type` | string | The type the n-th uploaded file must have. Numbered from 0 and read until the first gap. |
| `file.<n>.alias` | string | The context name the n-th uploaded file is given. Numbered from 0, counted separately from file.<n>.type, and read until the first gap. |

Relationships: `failure`, `success`. No others.

