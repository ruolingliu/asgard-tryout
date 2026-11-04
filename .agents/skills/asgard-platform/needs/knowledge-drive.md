# knowledge-drive: what to get from the customer

**documents the agent reads - manuals, FAQs, pages**

The customer provides these; we do not design them. Ask for exactly the
thing named. If you offer options, the customer may pick one that does not
apply, and it can take a week to find that out.

## the documents themselves, or the place they live and access to it

a Drive syncs from somewhere; without the source there is nothing to index

Stated in `../usecase/knowledge-drive.md`.

## who keeps them current, and how often they change

each Syncer carries its own `schedule` and the index its own cron, so the answer sets both - and with incremental sync the same record lands in several dated partitions, where the graph treats a stale one as a fact unless somebody says which copy wins

Stated in `../usecase/knowledge-drive.md`.

## when the documents are in Google Drive, OneDrive or Dropbox: whose account signs in to grant the connection, and that they can be there after the deploy, for the authorize step

the chart declares the credential but cannot grant it; the grant happens after the deploy, when somebody signs in and consents, and until then the Syncer fails while every check passes. Whoever signs in decides whose files the Syncer reads, and the platform does not check which account it was

Stated in `../wiki/settings.md`.

**Checked:** each row above names the document that owns its claim, and
`asgard-cli audit-material --links` resolves those. That is the whole of the
checking: a row is as good as the document it cites.

**Unchecked:** whether the list is complete for a shape, which only a finished engagement of that shape can show.
