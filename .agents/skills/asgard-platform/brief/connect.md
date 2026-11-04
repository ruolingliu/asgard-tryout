# Before connect

before binding a fresh checkout to the platform, and before adding a second account or pipeline to one

Every item below is a question for a person, and for each one the tool
will appear to have an answer already. The risk here is a question that was
never asked.

A list with one entry reads as a default whatever the text next to it says. An
agent bound the only pipeline in a workspace because its name resembled the
directory, when the person wanted a new pipeline against a different
repository. Read this as a checklist and get an answer for each line.

One item is not a question when the checkout has already answered it, and the
item says so: the remote called origin decides the provider account and the
repository, and both commands that need them derive them from it. Do not ask a
question whose answer is already on disk. An FDE was once given three options
that their own origin remote had already settled, and that extra question
displaced the one that needed asking.

## which workspace

**Said:** the one whose name looks like the customer's

**True:** Always ask. Nothing in the checkout says which workspace it deploys into - it is one of the two facts a repository cannot supply about itself, which is why `.asgard-cli.yaml` records it. An account can reach fifteen, and several will be plausible

Read `asgard-cli workspace list`.

## which provider account

**Said:** the one the workspace already has a connection to

**True:** The account whose repositories this engagement is about, which is often not the one connected months ago for something else. A workspace holds one connection per account and may hold several; `pipeline connect --account` names the one you mean, and defaults to the owner of this checkout's origin remote when there is one

Read `asgard-cli pipeline connections`.

## the app is not installed on that account yet

**Said:** pick an account from the list you already reach

**True:** Install the app; a person does that on GitHub. `pipeline connect --account <account>` prints the install URL for it - the app's slug is per-platform and a wrong slug is indistinguishable from a private app, so it comes from the platform rather than being guessed. On an organisation it may need one of its admins. That is a wait, not a failure: say so and stop

Read `asgard-cli pipeline connect --help`.

## which repository

**Said:** the one this directory is named after

**True:** Look at `origin` before asking anything. When it is set, do not ask: `pipeline connect` and `pipeline create` both derive the account and the repository from it, and both say on stderr what they took. When there is none - the ordinary state of a fresh `init` - ask for the repository's remote URL, which is what the pipeline binds and the only thing to ask: one URL answers the account, the name and whether the repository exists. Do not split it into separate questions; a directory name is not a repository, and the name a pipeline binds is the one this engagement carries afterwards. Then set it and push, because the pipeline reads its declaration off the default branch and a repository with no commits fails its first config sync. `pipeline repos` lists what the installation actually grants - a repository missing from it was not granted, which is fixed on GitHub and not here

Read `asgard-cli pipeline repos`.

## a new pipeline, or one the workspace already has

**Said:** there is one pipeline and its name resembles the directory, so that is it

**True:** This question has been answered wrong before. A workspace's existing pipeline may be for an entirely different repository, and one repository may carry several pipelines as long as their config paths differ. `pipeline use` and `pipeline create` are equally normal, and which one applies is not derivable from anything the tool can see

Read `asgard-cli pipeline list`.

## which platform project a release deploys into

**Said:** a workspace with no projects means something is broken

**True:** An empty workspace is the normal start. A release deploys into a platform project, and the project decides the namespace, so nothing deploys until one exists. `pipeline project create <name>` makes one with the default environment that `release create` requires - and it consumes account quota, so a refusal there is a subscription limit rather than a bad name

Read `asgard-cli pipeline projects`.

## how many releases the chart needs

**Said:** one release, because the chart is one chart

**True:** Usually one per environment. `<slug>-dev` and `<slug>-prod` name the same chart directory, differ by `on.pattern`, and are each created against a different platform project, which gives them different namespaces. One release is the shape for a POC nobody will maintain; if that is the answer, record it as a decision

Read `../guide/projects.md`.

None of these commands prompts. They are run by an agent following a
skill, not by somebody at a terminal - `init` is the one command in this tool with
a person in front of it - so the tool cannot ask these questions and the agent
has to. This list is those questions.

`asgard-cli gate` says which of these have been recorded, at any point.

**Checked:** every entry above is here because it actually happened, and each
names the document that carries the right version.

**Unchecked:** whether the list is complete, which only the next thing somebody gets wrong can show, so an activity with few entries is not a safe one.
