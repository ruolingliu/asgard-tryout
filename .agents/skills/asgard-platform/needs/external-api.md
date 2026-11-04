# external-api: what to get from the customer

**a system with an HTTP API rather than a database**

The customer provides these; we do not design them. Ask for exactly the
thing named. If you offer options, the customer may pick one that does not
apply, and it can take a week to find that out.

## the base URL, the auth scheme, and a credential for it

endpoints and non-secret settings become chart values; a token is a secret

Stated in `../usecase/external-api.md`.

## whether there is a test environment, before designing a mock

writing into a real test environment proves the fields, the validation rules and the status codes; a mock proves none of them

Stated in `../usecase/write-path.md`.

## if it is production-only, whether they permit testing against it

in the meeting, not assumed here - the answer decides whether the first delivery can be proved at all

Stated in `../wiki/taiwan-channels.md`.

## the rate limit

it decides whether a Syncer can backfill at all

Stated in `../guide/requirements.md`.

## if the system is email — an HTTP mail API and a key for it, plus a sender address already verified with that provider. Not SMTP credentials

the platform's only outbound call is HTTPS, so a username, a password and an SMTP host cannot be used - and that is what gets handed over when you ask for mail access. The verification is their IT's to do, on their schedule, and an unverified sender is refused outright

Stated in `../wiki/integration.md`.

**Checked:** each row above names the document that owns its claim, and
`asgard-cli audit-material --links` resolves those. That is the whole of the
checking: a row is as good as the document it cites.

**Unchecked:** whether the list is complete for a shape, which only a finished engagement of that shape can show.
