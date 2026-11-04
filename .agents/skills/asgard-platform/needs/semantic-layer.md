# semantic-layer: what to get from the customer

**a database we can read, with an agent asking questions of it**

The customer provides these; we do not design them. Ask for exactly the
thing named. If you offer options, the customer may pick one that does not
apply, and it can take a week to find that out.

## host, port, database or schema, and the account name

there is no connection without them

Stated in `../guide/requirements.md`.

## is that account read-only? Ask explicitly

the one offered first usually is not, and finding out later means going back for a second credential

Stated in `../guide/requirements.md`.

## that Asgard's four outbound addresses go on their allowlist - ask their network team for exactly that, not for "a VPN, an allowlist or a jump host"

Asgard is hosted and the agent runs in the platform's own cloud; there is nothing of ours to put on their network. In most companies this change needs a ticket, an approval and a maintenance window, so discovering it late delays the project by weeks

Stated in `../wiki/operations.md`.

## if the database has no address reachable from outside and they already run an SSH bastion that does: its host, port, user, a password or a private key, and its host key - and the allowlist goes on the bastion's SSH port

a postgres, mysql, mssql, oracle, hana or trino DataConnector can tunnel through the bastion with `sshTunnel`; without the host key the bastion's identity is not checked

Stated in `../wiki/operations.md`.

## whether the allowlist change can be done, and roughly when

a date changes the plan. Do not ask who approves it - a name changes nothing we build

Stated in `../guide/requirements.md`.

## a description of every cube, dimension and measure, in the customer's own words

the CRD requires a description on each, and it is what the model matches on - not the column name

Stated in `../usecase/semantic-layer.md`.

**Checked:** each row above names the document that owns its claim, and
`asgard-cli audit-material --links` resolves those. That is the whole of the
checking: a row is as good as the document it cites.

**Unchecked:** whether the list is complete for a shape, which only a finished engagement of that shape can show.
