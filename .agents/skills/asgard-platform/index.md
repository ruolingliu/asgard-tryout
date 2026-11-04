# The Asgard platform: the map

Five kinds of document, and a pointer from one to another is a path you can
follow:

    wiki/       what the platform has, and which CR a UI name maps to
    usecase/    how ONE deployment shape is assembled, field by field
    needs/      what to get from the customer before a shape can be built
    brief/      what has actually been got wrong, before you do the thing
    guide/      which decision to make now, and what it costs to change later
    aliases.md  what a customer said -> what to search for

They answer different questions and it is worth knowing which you have.
"Can Asgard do X" is `wiki/`; "what goes in this field" is `usecase/`; "what do I
have to ask them for" is `needs/`; "where does this go wrong" is `brief/`; and
"which decision am I making" is `guide/`.

A pointer is a path, relative to the document it is written in:

    ../wiki/<name>.md     from a document inside one of the directories
    wiki/<name>.md        from `aliases.md` or this file, which are at the root

Written with `../` even between two documents in the same directory, so that a
pointer carries which kind it points at. Following one is opening a file, and
this lists everything a document points at:

    grep -o '\.\./[a-z]*/[a-z0-9-]*\.md' wiki/agents.md

Read `aliases.md` first if the question did not arrive in English. The corpus
is English, so a word taken from what somebody said may match nothing, which
looks the same as a subject the material lacks.

## `wiki/` - what the platform has, and which CR a UI name maps to

Listed, grouped by the question each answers, in [`wiki/index.md`](wiki/index.md).

## `usecase/` - how one deployment shape is assembled, field by field

Listed, grouped by the question each answers, in [`usecase/README.md`](usecase/README.md).

## `needs/` - what to get from the customer before a shape can be built

| document | covers |
|---|---|
| [`needs/browser-operation.md`](needs/browser-operation.md) | a back-office login, whether a non-production one exists, how many pages and operations actually matter |
| [`needs/chat-channel.md`](needs/chat-channel.md) | which channel, asked before anything else because the field is immutable; the credential pair each platform actually takes; the LINE step that gates the rest |
| [`needs/external-api.md`](needs/external-api.md) | the base URL and its credential, whether a test environment exists, the rate limit, and why mail is an HTTP API rather than SMTP |
| [`needs/knowledge-drive.md`](needs/knowledge-drive.md) | the documents or the place they live, who keeps them current, how often they change |
| [`needs/semantic-layer.md`](needs/semantic-layer.md) | the connection and the account, whether it is read-only, the outbound addresses that have to go on their allowlist, a description per cube |
| [`needs/skill-set.md`](needs/skill-set.md) | the git repository the skills live in, and a token for it if it is private |
| [`needs/write-path.md`](needs/write-path.md) | whether a test environment exists, and who is on the other end when the approval gate stops |

## `brief/` - what has actually been got wrong, before you do the thing

| document | covers |
|---|---|
| [`brief/customer-meeting.md`](brief/customer-meeting.md) | what gets oversold and undersold in the room - the one network shape, the approval gate, what the platform cannot send, and what must never reach a slide |
| [`brief/connect.md`](brief/connect.md) | the questions binding a checkout has to ask a person - workspace, account, repository, pipeline, platform project - which of them `origin` answers on its own, and why a list of one is not a default |
| [`brief/write-chart.md`](brief/write-chart.md) | the decisions that look obvious and were reversed - the public read surface, the anonymous entry point, `allowWrite` defaulting to true, and what a green render does not cover |
| [`brief/handover.md`](brief/handover.md) | a green deploy the customer cannot see - the per-resource permission step, the order to walk them through, and which screenshots have to be cropped |

## `guide/` - which decision to make now, and what it costs to change later

| document | covers |
|---|---|
| [`guide/projects.md`](guide/projects.md) | the split follows the audience, ask against watch, two releases of one chart per environment, the table the interview builds |
| [`guide/data-sources.md`](guide/data-sources.md) | the ladder for what to ask them for, filling .env without anybody typing a password, introspecting the real schema rather than guessing it |
| [`guide/read-path.md`](guide/read-path.md) | a semantic layer or fixed query tools, the layer nobody asks questions of, what zero-parameter does not mean |
| [`guide/entry-point.md`](guide/entry-point.md) | the agent hub or your own BotProvider, why a public widget cannot have the hub, the project that needs no entry point at all |
| [`guide/knowledge.md`](guide/knowledge.md) | a Drive with contextIndex rather than a KnowledgeBase, the immutable Syncer paths, what a person still has to do after the deploy |
| [`guide/verify.md`](guide/verify.md) | what each step of the gate is for, the step that only the platform can run, why a skipped step is not a pass |
| [`guide/deploy.md`](guide/deploy.md) | the release and the values that exist before the first tag, which tag reaches which release, the Console step between a green deploy and a working one |
| [`guide/enhance.md`](guide/enhance.md) | which project a new capability belongs to, when it needs a spec first, the closing step that gets skipped |
| [`guide/requirements.md`](guide/requirements.md) | the order to ask in, the answers that looked obvious and were reversed, the two filters before a question becomes a row |
| [`guide/idle.md`](guide/idle.md) | the one question left when no request and no task are open, and why that state is not being behind |

## What is not here

Everything the material points at is a path you can follow. There is one
exception, and it needs the `asgard-cli` binary:

| pointer | why it is not a file |
|---|---|
| `asgard-cli guide <name>` | half of it is here. A guide renders this repository's own state into its guidance - which projects exist, what is still open - and a file would freeze one moment of that. The decisions are in `guide/`; run the command for where this repository stands |

The commands that answer that half directly, when it is all you want:

    asgard-cli project     what each chart declares
    asgard-cli question    what nobody has answered yet
    asgard-cli request     what the customer asked for
    asgard-cli task        the open task specs

## Staleness

These files came from one binary. A newer one may carry different pages, and
nothing in here can tell you which:

    asgard-cli init

It reports what is here against what the running binary carries, and replaces
this directory outright when the version has moved. Read it as the authority
over these files rather than anything written inside them.
