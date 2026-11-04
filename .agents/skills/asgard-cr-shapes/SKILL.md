---
name: asgard-cr-shapes
description: The Asgard custom resource shapes this cluster enforces - every kind, every spec field, its type, whether it is required, its default, its enum and its pattern, read from the apiserver itself. Read the file for a kind before writing or editing a CR of that kind.
version: 13
alwaysApply: false
---

# Asgard CR shapes

24 kinds, 1419 spec fields, 532 of them required.

**Generated from the cluster this repository deploys to. Do not edit these
files** - the next `asgard-cli skill update` overwrites them.

**It is read from the apiserver, not from asgard-kube.** Those two are not the
same answer. A CRD is applied by whatever chart the cluster runs, so a checkout
of the Go types says what asgard-kube says today, while the apiserver says what
it will admit - and every check that decides whether a CR is accepted (required,
enum, pattern) is the apiserver's. This came from the cluster your runs deploy
to.

**What is here and what is not.** This is shape. It will tell you that
`spec.displayName` is required and must match a pattern; it will not tell you
that a wrong entry name is as fatal as a wrong workflow name and that apply
catches neither. That kind of thing is judgement, it cannot be extracted, and it
lives in the hand-written skills beside this.

`status` is not here at all. It is written by controllers, never by an author,
and it is about a third of each schema by field count.

## How to read a field

- **field** is the path as a chart writes it. `[]` is a list's items and `.*` is
  any key of a map: `spec.entries[].workflowName`, `spec.labels.*.value`.
- **required** is the parent object's `required` list, so it means required *when
  the object containing it is present*.
- **default** is JSON, so it keeps its type: `3` is a number, `"read"` is a
  string, and an empty cell means the schema declares no default - which is not
  the same as defaulting to empty.
- **constraints** carries the enum and the pattern. A pattern is worth reading
  before naming anything: the apiserver's rejection quotes the regex and does
  not say which field it came from.
- **deprecated** in that column is a convention rather than a schema fact.
  Kubernetes has no per-field deprecation marker, so the only signal is a Go
  `// Deprecated:` doc comment that controller-gen copied into the description.
  A field superseded without one looks identical to a current field here.

## The kinds

| kind | fields | required | file |
|---|---|---|---|
| `Agent` | 25 | 14 | [Agent.md](Agent.md) |
| `BotProvider` | 129 | 38 | [BotProvider.md](BotProvider.md) |
| `CompletionModel` | 100 | 34 | [CompletionModel.md](CompletionModel.md) |
| `DataConnector` | 238 | 77 | [DataConnector.md](DataConnector.md) |
| `EmbeddingModel` | 72 | 25 | [EmbeddingModel.md](EmbeddingModel.md) |
| `ImageGenerationModel` | 46 | 17 | [ImageGenerationModel.md](ImageGenerationModel.md) |
| `Indexer` | 67 | 31 | [Indexer.md](Indexer.md) |
| `KnowledgeBase` | 16 | 7 | [KnowledgeBase.md](KnowledgeBase.md) |
| `Loader` | 118 | 45 | [Loader.md](Loader.md) |
| `OAuthCredential` | 5 | 4 | [OAuthCredential.md](OAuthCredential.md) |
| `OAuthProvider` | 30 | 11 | [OAuthProvider.md](OAuthProvider.md) |
| `Plugin` | 17 | 10 | [Plugin.md](Plugin.md) |
| `Sandbox` | 30 | 18 | [Sandbox.md](Sandbox.md) |
| `SandboxBlueprint` | 55 | 1 | [SandboxBlueprint.md](SandboxBlueprint.md) |
| `SemanticLayer` | 49 | 32 | [SemanticLayer.md](SemanticLayer.md) |
| `SkillSet` | 3 | 2 | [SkillSet.md](SkillSet.md) |
| `Source` | 75 | 39 | [Source.md](Source.md) |
| `SourceSet` | 21 | 7 | [SourceSet.md](SourceSet.md) |
| `SourceSetEditorServer` | 3 | 2 | [SourceSetEditorServer.md](SourceSetEditorServer.md) |
| `Syncer` | 182 | 57 | [Syncer.md](Syncer.md) |
| `Toolset` | 33 | 13 | [Toolset.md](Toolset.md) |
| `TranscriptionModel` | 46 | 17 | [TranscriptionModel.md](TranscriptionModel.md) |
| `Trigger` | 9 | 8 | [Trigger.md](Trigger.md) |
| `Workflow` | 50 | 23 | [Workflow.md](Workflow.md) |

## Deprecated fields

2 field(s) say so in their description:

- `Syncer` `spec.destinationMemberKey` - Deprecated: use destinationPath instead. Kept only so pre-rename Syncer objects stay readable during the transition; new objects should set destinationPath.
- `Syncer` `spec.stateMemberKey` - Deprecated: use statePath instead. Kept only so pre-rename Syncer objects stay readable during the transition; new objects should set statePath.
