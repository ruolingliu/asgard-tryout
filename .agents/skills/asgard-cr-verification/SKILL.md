---
name: asgard-cr-verification
description: Use before pushing any change under a chart or `.asgard-pipeline.yaml`. What the Asgard platform checks when it plans a run, what each rule code means and how to fix it, and the mistakes that pass every local check and every dry run and still fail — a dangling reference, a resource credential read from the platform's own Secret, a missing display annotation, an invented processor config key, a field the CRD silently prunes. Read it with the generated `asgard-cr-shapes` and `asgard-workflow-processors` references beside it.
alwaysApply: false
---

# Verifying an Asgard CR

There is no application to run in an IaC repository. Every artifact is a
declarative Kubernetes custom resource under `asgard-ai.com/v1alpha1`, so what
"it works" means is: the platform rendered your chart, the apiserver accepted
every object it produced, and the objects resolve to each other.

**Any red step stops the work.** Report the specific error and do not push past
it.

> **This document comes from the platform**, and it describes the platform your
> runs deploy to rather than whichever Asgard we happened to be running when
> your tooling was built. It is written; the two files beside it —
> `asgard-cr-shapes` and `asgard-workflow-processors` — are extracted from this
> server's cluster and this server's runtime. Those say what a field is called.
> This says what happens when you get it wrong.

## What the platform does with a push

A push of a tag or a branch matching a release's trigger produces a run, and a
run has six steps, in this order:

    checkout -> lint -> variables -> render_dry_run -> review -> apply

`review` is a person. Everything before it is the plan, and everything the plan
found is in its report.

**The plan is the authority, and nothing that ran before the push is.** Whatever
your tooling checked locally, it checked without a cluster — and the two most
valuable rules below, `crd/dry-run-rejected` and `crd/unknown-field`, need an
apiserver that **no client is ever issued credentials for**. A clean local run
means "worth pushing". It never means "this will deploy".

> **This document deliberately stops at the push.** What your CLI runs before
> it, and what each of those steps covers, is a fact about a binary whose
> version this server does not know — an on-prem customer's CLI can be several
> releases from ours in either direction. That half is documented by the CLI
> itself, where it moves when the CLI moves. Ask it what it runs; do not take
> a list of steps from a server that cannot see it.

## The rules the plan applies

Ten fail the run. Four are recorded and do not.

### Errors

| code | what it means |
|---|---|
| `config/schema` | `.asgard-pipeline.yaml` is missing, does not match the schema, or declares a `version` this platform does not support |
| `config/release-missing` | the release this run hit is declared in the yaml but was never created on the platform. **The yaml does not create releases** — declaring one and pushing a matching tag produces nothing until somebody creates it |
| `config/chart-missing` | the `chart` path does not exist, or has no `Chart.yaml` |
| `vars/required-missing` | a key the declaration marks required has no value. Usual on a release's first run; the values are set on the platform, not in the repository |
| `chart/kind-not-allowed` | the chart rendered something outside the `asgard-ai.com` group. A pipeline deploys Asgard resources and nothing else — no Deployment, no Secret, no ConfigMap of your own |
| `chart/hook-not-allowed` | a manifest carries a `helm.sh/hook` annotation. There is no hook phase to run in |
| `chart/namespace-not-allowed` | a rendered object sets `metadata.namespace`. A release deploys into one namespace — the one its Project owns — and the platform supplies it. Leave it off and the object lands in the right place; naming one is how an object ends up in a Project whose own release knows nothing about it |
| `chart/remote-dependency` | `Chart.yaml` names a dependency from somewhere other than `file://`. What deploys has to be in the repository the run checked out |
| `chart/render-error` | a template error, or the render exceeded the time or size limit |
| `crd/dry-run-rejected` | the apiserver refused the object. Pattern violations, CEL rules, `Required value` |
| `crd/unknown-field` | a rendered object sets a field the cluster's CRD does not declare. **See below — this is the one that looks like it works** |

### Warnings

| code | what it means |
|---|---|
| `config/release-orphan` | the platform has a release the yaml no longer declares. Nothing deploys it; it is a row nobody is going to notice |
| `vars/orphan` | a value is stored for a key the declaration does not name. **It is not injected**, so a chart reading it gets nothing |
| `chart/asgard-key-defined` | the chart's own `values.yaml` defines the reserved `asgard` key. The platform's values win, so whatever it says there is decoration |
| `run/pattern-mismatch` | a manual run's ref does not match the release's trigger pattern. It runs anyway — you asked for it — but a push of that same ref would not have |

## The mistakes that pass everything and still fail

These are the ones worth knowing, because nothing before deployment says a word
about them.

### A field the CRD does not declare

CRDs prune unknown fields by default, so a server-side dry run reports the
object as created **while the field is quietly discarded**. A deprecated
`Toolset.spec.instruction` passed 25 dry runs in a row and then failed the real
deploy, because a server-side apply builds a typed patch and refuses it:

    .spec.instruction: field not declared in schema

`crd/dry-run-rejected` answers "will it be accepted". `crd/unknown-field`
answers "will it be kept". They are different questions and the plan asks both.

Check a field against `asgard-cr-shapes/<Kind>.md` beside this file. That is
read from this cluster's own CRDs, so it is the same schema the plan uses — a
checkout of asgard-kube is a different answer, because a cluster runs whatever
chart was applied to it.

### An invented processor config key

`Workflow.processors[].configs[].name` is a free-form string in the CRD. A
misspelt key **lints clean, passes CRD validation and does nothing at runtime**.
Nothing in Kubernetes can catch it, because as far as the schema is concerned
you have written a valid string.

`asgard-workflow-processors/SKILL.md` beside this file lists, for every
processor type, the config keys this server accepts and which are required. It
is extracted from the runtime, so it is the only statement of that set that
cannot drift.

### A dangling reference

CRs address each other by name, and a name that resolves to nothing applies
perfectly. These are the pairs that matter:

- `Agent.managed.toolsetNames[]` → a real `Toolset`
- `Agent.managed.skillSetNames[]` → a real `SkillSet`
- `Agent.managed.semanticLayers[].name` → a real `SemanticLayer`
- `SemanticLayer.dataConnectorName` → a real `DataConnector`
- `SkillSet.sourceSetName`, `Syncer.sourceSetName` → a real `SourceSet` — or
  the Agent Hub Global Directory, which the platform creates in every namespace
  and a chart reaches only through `.Values.asgard.agentHubGlobalSourceSetName`
  (below)
- `Loader.knowledgeBaseName` → a real `KnowledgeBase`
- `Loader.database.dataConnectorName` → a real `DataConnector`
- `SandboxBlueprint.skillSetNames[]` → a real `SkillSet`
- `SandboxBlueprint.pluginNames[]` → a real `Plugin`

**Every entrypoint is a pair, and both halves have to resolve.**
`Toolset.tools[]`, `Workflow.exits[].handlingWorkflow` and
`BotProvider.entrypoint` each name a workflow *and an entry within it*. A wrong
entry name is as fatal as a wrong workflow name, and apply catches neither.

**The Flow Agent chain is three links and a typo silently drops it.** A
processor's `sandboxBlueprint` config names a real `SandboxBlueprint`, and
`SandboxBlueprint.spec.agents[].baseAgentName` names a real `Agent` — the second
one lives inside a JSON string the CRD stores, so nothing schema-shaped can look
at it. The symptom is an agent that "can't call any tools".

### A resource credential read from the platform's Secret

`SourceSet.apiKey`, `Toolset.apiKey` and `BotProvider.adminApiKey` are each the
`X-API-KEY` that edgeserver checks on that one resource's own endpoints, and the
platform's own callers read the value back from the CR. So the key is the
release's own: `asgard_resource_api_key` by convention, in the release's Secret,
declared under `appSecret:`.

    apiKey:
      valueFrom:
        secretKeyRef:
          name: {{ include "<chart>.appSecretName" . }}
          key: asgard_resource_api_key

**When no use case calls the resource from outside the platform, set a random
value and ask nobody** — there is nobody who issues it. Thirty-two random bytes
as hex, with no trailing newline, stored as the release's secret variable
`asgard_resource_api_key` is the whole answer. Generate it with whatever your
tooling provides for this rather than a shell recipe: one that pipes text
through a terminal can add a newline or re-encode it, and the value stored is
then not the value intended.

Set it before the first deploy. **A key missing from the Secret resolves to an
empty string, and an empty key matches a request that sends none** — the
resource is open, and nothing reports it. When a caller does need the value — a
front end calling a `generic` BotProvider with `authMode: api-key`, a script
managing a SourceSet's volume through edgeserver — generate it the same way and
hand it to that caller.

**Never reference `preset-agent-hub`.** The platform creates that Secret in
every namespace for Agent Hub, and never rotates it because Agent Hub depends on
the same value. A CR reading it resolves, applies and comes up Ready, and every
check here is green — while the chart is bound to a key it cannot rotate without
breaking Agent Hub, and a leak of it exposes every platform function in the
namespace rather than one chart.

### A file written into the Agent Hub Global Directory

The Global Directory is a SourceSet the platform creates in every namespace and
mounts, read-only, into every Agent Hub conversation; the `AGENTS.md` at its top
level is read on every turn. A chart puts that file there with a
`static-content` Syncer:

    apiVersion: asgard-ai.com/v1alpha1
    kind: Syncer
    metadata:
      name: agents-md
      annotations:
        asgard-ai.com/syncer-name: AGENTS.md
    spec:
      sourceSetName: {{ required "the platform injects .Values.asgard.agentHubGlobalSourceSetName" .Values.asgard.agentHubGlobalSourceSetName }}
      destinationPath: AGENTS.md
      syncerClass: static-content
      schedule: "0 * * * *"
      staticContent:
        text: |
          # Working rules
          ...

Each of these applies cleanly and is still wrong:

- **Writing the SourceSet's name down.** It is the platform's to choose. Read
  the reserved value; `required` makes a platform that predates it fail at
  `chart/render-error` instead of rendering an empty name. **Never declare a
  SourceSet of that name** — the platform owns it.
- **A `{{` inside `text`.** The text is part of the template, so helm evaluates
  it. An `AGENTS.md` that shows a template example gets the rendered value
  written into it instead, with nothing in the plan to say so. Escape it:
  `{{ "{{" }}`.
- **Treating `destinationPath` as a folder.** For `static-content` it is the one
  file the Syncer writes, and it does not end in `/` — every other class's
  `destinationPath` does. The CRD rejects either mix-up at
  `crd/dry-run-rejected`.
- **A file inside another Syncer's folder**, or two `static-content` Syncers on
  one file. Each run of one replaces or removes what the other wrote, for as
  long as both exist.
- **Expecting more of the file than the platform reads.** Only the top-level
  `AGENTS.md` is read, and only its first 64 KiB. A Syncer is one Kubernetes
  object, so text past about 1.5 MB cannot be stored at all.

What the Syncer does is narrow on purpose: a file that already matches is left
alone, missing folders are created, a path blocked by a file, a directory or a
symlink fails that run and writes nothing, and deleting the Syncer leaves the
file where it is. Edits made to the file by hand are replaced on its next run.

### A git Syncer narrowed with `includePaths`

`spec.git.includePaths` makes a git Syncer check out only the listed folders of
the repository; absent or `[]` is the whole repository. It is how a SkillSet
takes a few skills out of a large repository:

    git:
      repoUrl: https://github.com/anthropics/skills.git
      revision: main
      includePaths:
        - skills/pdf/

Each of these applies cleanly and is still wrong:

- **A SkillSet `searchPaths` entry outside the listed folders.** Nothing is
  written there, so it loads no skills, and the platform does not compare the
  two lists. A searchPath inside a listed folder, or at or above one, is fine.
- **Writing an entry relative to the volume.** An entry is relative to the
  repository root — `skills/pdf/`, not `git/skills/pdf/` — and the folder keeps
  its place, so the searchPath is still `git/skills/pdf/`. The CRD rejects an
  entry that is not a relative folder ending in `/` at `crd/dry-run-rejected`,
  but not one the repository does not have.
- **An entry the revision does not have, or one that is a file.** The plan and
  the apply pass; the Syncer's next run fails and leaves the destination as the
  last sync wrote it.
- **Narrowing without meaning to delete.** The list is edited in place, and the
  next run removes a dropped folder from the drive. Adding a folder downloads
  only that folder; clearing the list brings back the whole repository. None of
  it clones again.

Git's cone mode also writes the files directly in the repository root and in
each parent folder of an entry. Inside the checkout, `git log -p`, `git show`
and `git diff` fetch the missing contents from the repository, which fails for a
private one: its credentials are not in the volume.

### A missing display annotation

Every CR the platform's UI renders carries a `<kind>-name` annotation —
`asgard-ai.com/agent-name`, `asgard-ai.com/semantic-layer-name`,
`asgard-ai.com/data-connector-name`, `asgard-ai.com/syncer-name`. Without it the
CR **applies fine and then appears in the UI with no name.** `Agent` needs only
`agent-name`; its description comes from `spec.managed.description`.

## The reserved values

The platform injects an `asgard` block into every render. A chart reads from it
and never writes a namespace, a secret name or an environment id down:

    .Values.asgard.release              the helm release name
    .Values.asgard.releaseName          the release as the declaration spells it
    .Values.asgard.namespace            where it deploys
    .Values.asgard.projectId
    .Values.asgard.projectEnvironmentId
    .Values.asgard.appSecretName
    .Values.asgard.appConfigMapName
    .Values.asgard.ref                  the git ref this run deployed
    .Values.asgard.commitSha
    .Values.asgard.agentHubGlobalSourceSetName
                                        the Agent Hub Global Directory's SourceSet

A chart that hardcodes any of these deploys to one place and one place only, and
the failure shows up the first time somebody creates a second release.

## Reporting

Summarise pass/fail per step. Declare success only when the run reached `apply`
and finished. On a failure, name the step and the rule code and **quote the
error rather than paraphrasing it** — the rule codes above are stable and
searchable, and a paraphrase is not.

If a step could not be run, say so. That is not the same as passing.
