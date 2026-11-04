# Before customer-meeting

before any conversation with the customer, at any stage

The intuitive answers here are wrong in both directions, and the two
mistakes cost different things. Underselling - "it cannot tell who they are",
"we would have to build an approval step", "only the systems you connect to
it" - gives away scope, and the customer cannot tell caution from a wrong
answer. Overselling - a ticket number treated as authentication, a notification
the platform cannot send - is a promise that cannot be built. Read every entry
before the meeting, not only the ones that match your topic, because you cannot
predict which direction you will get wrong.

This stage's output is what you say. Other stages produce files, which can be
edited and re-rendered; a wrong sentence in a meeting ends up in the
customer's notes.

## how we reach a system inside their network

**Said:** "a VPN, an allowlist or a jump host - whichever suits you"

**True:** One shape only: they add our outbound addresses to their allowlist. Asgard is hosted and the agent runs in a sandbox in that cloud, so there is nothing of ours to place on their network. If you offer options, the customer picks one that does not apply. Ask who will make the firewall change, for the follow-up list, and do not hand out the addresses in the meeting

Read `../wiki/operations.md`.

## whether an anonymous channel knows who is asking

**Said:** "it cannot tell who they are, so identity has to wait"

**True:** An anonymous channel can answer "where is MY order". The caller supplies identity server-side every turn; only the model supplies nothing. LINE's webhook carries a userId, which `../guide/requirements.md` covers rather than this pointer. Deferring identity gives away something you already have

Read `../guide/read-path.md`.

## how many agents

**Said:** "one agent, then"

**True:** A flow-agent shape renders zero `Agent` CRs - the prompt is on a Workflow processor and the capabilities on the blueprint. A quote that assumes one Agent is priced for work that does not exist

Read `asgard-cli size flow-agent-single`.

## how an anonymous caller is identified

**Said:** "they can give us their ticket number and we look it up"

**True:** A ticket number is not authentication. Ticket numbers are usually sequential, so a lookup keyed on one alone lets anybody enumerate other people's cases. Any self-service query on a public channel has to say what identifies the person, and a number they type does not count

Read `../guide/requirements.md`.

## how a write is tested

**Said:** "during the test, shall we really create the ticket or just draft it?"

**True:** Ask whether they have a test environment first. The question under Said assumes they only have production, and it gives away the strongest version of the first delivery: writing into a test system proves the fields, the validation rules and the status codes, and a mock proves none of them. A mock is the fallback when there is no test environment - or when they will not let us write to production, which is their call

Read `../usecase/write-path.md`.

## whether it can do things, not only answer

**Said:** "we would have to build an approval step for that"

**True:** The approval gate is built into the platform. A write stops, names the tool, and nothing runs until a person allows it. It is not custom work. What is approved is the tool rather than the exact content

Read `../usecase/write-path.md`.

## whether it can email or message people

**Said:** "sure, we can have it send you a summary"

**True:** The platform sends nothing: no SMTP, no mail toolset, nothing in the core. It can call an endpoint of theirs that sends mail, if they have one. Ask whether they have one before promising a notification

Read `../wiki/integration.md`.

## what the agent can reach

**Said:** "only the systems you connect to it"

**True:** That is incorrect. Every sandbox carries the coding CLI's own tools - web search and fetch among them - and no Toolset or blueprint setting removes them. The only control is an instruction in the prompt

Read `../wiki/tools.md`.

## whether they can use their own model or their own key

**Said:** "yes, we can point it at your account"

**True:** Only on Odin. Sindri and Mimir use the platform's designated models and the LLM cannot be swapped there. So the answer depends on which product the capability lands in - which is question 2b, decided before anyone thinks about billing. A customer with a model contract or a rule about where inference happens needs this while the shape is still open

Read `../wiki/fehu.md`.

## whether they can have a specific model

**Said:** "of course, we will configure that one"

**True:** They can, and they should know the cost: a builtin tier is a logical model backed by several providers with automatic failover, and a custom `CompletionModel` is one provider, one key, one point of failure. A concrete reason - compliance, an existing contract, a model they tested against - justifies it. A preference usually does not

Read `../wiki/settings.md`.

## what the limits are

**Said:** "30 steps and 3 minutes per request is the limit"

**True:** The time is a default, raised by contacting sales or service@asgard-ai.com. The steps are not a quota at all: a step is one hand-off between processors, however many tools one of them calls, and the ceiling is the chart's own `maxUnsupervisedSteps`, 30 unless the chart says otherwise - so say what a step is and that it is set per deployment

Read `../wiki/integration.md`.

A slide is not an agenda and not a tracking list. "Who is
responsible for this?" is fine to ask in the room and should not be printed:
asking it shows you will follow up, while printing it reads as managing their
organisation. To decide, ask whether the answer is something we chase after
the meeting (keep it off the slide) or something we build (it can go on). Six
of one deck's twenty corrections were this, more than any other kind, and three
of those were copied out of this tool's own material.

Ask what they have already read before describing anything. The
product site tells them Odin is for non-technical staff, gives them a vocabulary
- Basic Function, Template - that maps to nothing here, and says Mimir simulates
the future. `../wiki/what-they-read.md` has the three, and it costs
one sentence to find out which of them you are correcting.

Anything on
`../wiki/platform-unknowns.md` that this engagement touches is ours to
resolve before the meeting. Do not raise it with the customer as something we
do not know about our own product.

Never on their screen: implementation nouns, another customer, coordinates -
theirs *or* our own outbound addresses - and this repository's own bookkeeping,
question numbers included. The `proposal-deck` skill has the rest.

**Checked:** every entry above is here because it actually happened, and each
names the document that carries the right version.

**Unchecked:** whether the list is complete, which only the next thing somebody gets wrong can show, so an activity with few entries is not a safe one.
