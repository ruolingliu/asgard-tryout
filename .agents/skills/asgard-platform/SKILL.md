---
name: asgard-platform
description: The Asgard platform as greppable files - what the platform has, which CR a UI name maps to, how each deployment shape is assembled field by field, what to get from the customer before one can be built, and where each has been got wrong before. Use when writing or reading an Asgard CR or Helm chart, when a customer names something and you need to know what it maps to, before a customer meeting, or before answering any question about what the platform can do. Read aliases.md first when the question came in a language other than English.
---

# The Asgard platform, as files

The platform knowledge an agent in a customer repository does not otherwise
have. That repository describes one customer's systems, not the platform they
run on.

    wiki/       what the platform has, and which CR a UI name maps to
    usecase/    how ONE deployment shape is assembled, field by field
    needs/      what to get from the customer before a shape can be built
    brief/      what this activity gets wrong, before you do it
    guide/      which decision to make now, and what reversing it costs
    aliases.md  what a customer said -> what to search for

Start at [`index.md`](index.md): it says which directory answers which
kind of question, how a pointer becomes a path, and what is not here.
`wiki/index.md` and `usecase/README.md` list their documents grouped by
the question each answers.

This directory is generated. `asgard-cli init` writes it from the corpus
inside the binary and the next run replaces it, so do not edit it; file a
correction instead.

## Grep it

    grep -ril "<term>" .
    grep -n "<term>" wiki/processors.md

## Two things grep will not do for you

Read `aliases.md` before searching a question that arrived in another
language. The material is English, so a word taken from what somebody said may
match nothing, which looks the same as a subject the material lacks. The file
has two tables: words that replace a term, and names that are added to it.

Check `wiki/glossary.md` for the word you searched. A few words mean one
thing here and something else to a customer. `payment` is billing between
Asgard and the customer, and also the customer's own payment gateway; results
in the wrong sense look like an answer.

## When the answer is not here

File a page that is wrong, or a question these files do not answer, rather
than working around it. This material is compiled into the binary, so a note in
one repository reaches no other engagement:

    asgard-cli issue-report --new > report.md
    asgard-cli issue-report --send report.md

## Staleness

These files came from one binary and a newer one may carry different pages.
Nothing in this directory can tell you which:

    asgard-cli init

That compares what is here against the running binary and reports its state.
`ahead` means these files were written by a newer build than the one you are
running: your binary is the stale one, and `--force` would be a downgrade.

The platform's own reference material is a separate half with its own record -
`asgard-cli skill status` - because a customer's server can be several
versions from this CLI in either direction, and only the server can say what it
accepts.
