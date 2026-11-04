# chat-channel: what to get from the customer

**the agent reached from a chat platform the customer's users already use**

The customer provides these; we do not design them. Ask for exactly the
thing named. If you offer options, the customer may pick one that does not
apply, and it can take a week to find that out.

## which channel, asked together with who is on the other end

`botProviderClass` is immutable once created, so changing it later is a new BotProvider rather than an edit

Stated in `../guide/requirements.md`.

## LINE: that Messaging API is enabled on the Official Account, before anything else

it is their step in their console, and it gates every other LINE question. The Channel Secret and Channel Access Token do not exist until it is done

Stated in `../wiki/integration.md`.

## LINE: Channel Secret and Channel Access Token — and somebody who can paste a Webhook URL back into the LINE Developers Console and enable Use webhook

LINE is the only two-way setup: Asgard produces a URL that has to go back. The rest only take credentials inward

Stated in `../wiki/integration.md`.

## Slack: an app-level token and a bot token - the `xapp-` and `xoxb-` pair, not a Client ID

those are different credentials, and the Client ID is often asked for by mistake. The client id, client secret, signing secret and scopes are what the platform's own UI flow installs an OAuth app with; a chart's `spec.slack` requires `appToken` and `botToken` and neither of those four. Ask for the client pair as well only if the engagement is going through the UI

Stated in `../wiki/integration.md`.

## Discord: the Bot Token, and the bot authorised and invited to the server in their Developer Portal

the invitation is their step in their console rather than ours, and none of it is the token - a chart with the right `botToken` still has nowhere to speak

Stated in `../wiki/integration.md`.

## Telegram: the Bot Token from BotFather. The second field is ours, not theirs

`spec.telegram` requires `webhookSecretToken` beside the bot token and no documentation page mentions it - it is a secret we choose, so it is not something to ask for, but a CR without it is refused

Stated in `../wiki/integration.md`.

## whether anything sits between the channel and us

an existing bot, a middleware, a support desk already on that channel - it changes the entry point

Stated in `../guide/requirements.md`.

**Checked:** each row above names the document that owns its claim, and
`asgard-cli audit-material --links` resolves those. That is the whole of the
checking: a row is as good as the document it cites.

**Unchecked:** whether the list is complete for a shape, which only a finished engagement of that shape can show.
