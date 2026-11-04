---
name: asgard-workbench-api
description: Use when reading or writing Asgard Workbench issues, comments, labels, relationships or attachments over the platform REST API — for example from an agent harness acting for a signed-in member. Every /v1/workbench endpoint, its query parameters and snake_case enum values, the error codes (workbench_conflict_retry, workbench_assistant_forbidden, workbench_issue_locked, workbench_pin_limit_reached, workbench_parent_already_set, workbench_unknown_query_param, workbench_subscription_required), the X-Asgard-Via-Assistant header and what the assistant may not do, the workspace audit log (Console Explore) read-through, the ISS-N display rule, attachment rules (byte-identical, supersedes, pull only what exists), and the known limit that there is no atomic batch across issues.
alwaysApply: false
---

# The Workbench REST API

The Workbench is a workspace's issue tracker. An issue belongs to a
**workspace**, not to a pipeline (called a **Deployment** in the UI; the API
always says pipeline): a pipeline is only an optional field on it. This
document describes what **this platform** accepts and answers. It is served by the platform, so it matches the server you are
talking to.

## Calling it

- Base path `/v1/workbench`. Every request carries
  `Authorization: Bearer <member JWT>` and `x-asgard-workspace: <workspace id>`.
  There is no project header.
- **You always act as the signed-in member.** The server takes the actor from
  the token. No request body field can name another person; one that tries is
  ignored.
- Responses are `{"success": true, "data": …}`, lists add `"paging": {…}`.
  Errors are `{"success": false, "message": …, "details": {"error_code": …}}`
  where an error code applies.
- Any workspace member may use everything here except the **admin** actions
  (pin, lock, delete an issue, manage labels), which need a workspace admin.

## Numbers: `ISS-N`

Issues are numbered per workspace: 1, 2, 3 …, never reused (a deleted number
stays taken). The API takes and returns the **bare number** (`number: 12`,
`/issues/12`). **On screen, and in anything a person reads, write `ISS-12` —
never `#12`**: next to a GitHub repository, `#12` reads as a GitHub issue or
pull request. The API never returns an `ISS-` or `#` string, and a path like
`/issues/ISS-12` is a 400.

## Enum values

Always snake_case on the wire. The spec's display names ("To Do", "In
progress") are for screens only; sending them is a 400.

| Field | Values |
|---|---|
| `status` | `backlog` `to_do` `ready` `in_progress` `pending_fix` `in_review` `done` (board order; everything before `done` is "not done") |
| `type` | `question` `request` `task` `bug` `feedback` |
| `priority` | `urgent` `high` `normal` `low` (new issues: `normal`) |
| relation `type` | `parent` `sub_issue` `blocked_by` `blocking` `duplicate_of` |
| `sort` | `updated_desc` (default) `created_desc` `priority` `due_date` |

There is no open/closed and no "close": finishing an issue is moving it to
`done`; reopening is moving it out. "Won't do" is the `not planned` label;
"stuck" is the `blocked` label.

## Issues

| Method | Path | Notes |
|---|---|---|
| POST | `/issues` | `title` and `type` required; optional `body` (markdown), `status`, `priority`, `due_date` (`YYYY-MM-DD`), `pipeline_id`, `assignee_ids`, `label_ids` |
| GET | `/issues` | filters below; cursor-paged |
| GET | `/issues/:number` | |
| PATCH | `/issues/:number` | send only what changes (see below) |
| DELETE | `/issues/:number` | admin; soft delete |
| GET | `/issues/:number/events` | the timeline, oldest first |
| GET | `/issues/suggest?q=&exclude=` | `#` completion: up to 8, not-done first |
| GET | `/summary` | the five summary cells, always the whole workspace |
| GET | `/board-counts` | cards per status under the list filters |
| GET | `/issues/group-counts?group_by=` | issues per group under the list filters, for "Group by" (below) |

**List filters** (`GET /issues`, `GET /board-counts`, `GET /issues/group-counts`). A multi-valued filter
may repeat or be comma-separated (`status=to_do,in_progress`). Values within a
filter are ORed; filters are ANDed.

- `status`, `type`, `priority`: enum values
- `pipeline_id`: pipeline ids, or `none` for issues about no pipeline — the
  same value as the issue's `pipeline_id` field. The old name `deployment` is
  a 400 `workbench_unknown_query_param`, never silently ignored
- `assignee`: IAM user ids, `me` for the signed-in member, or `none` for
  issues with no assignee (`assignee=none,me` = unassigned or mine)
- `label`: label ids
- `q`: title substring, or an issue number (`12` or `ISS-12`)
- `sort`: see enums
- `done_after` (RFC 3339, list only): done issues only if done at or after it
- `page_size` (0 → 20, max 100) and `page_token`: pass
  `paging.next_page_token` back; empty means the last page.
  `paging.total_count` counts all matches.

**Group by** (`GET /issues/group-counts`). `group_by` is required: `status`,
`assignee`, `type`, `priority` or `pipeline`. Returns
`{"group_by": …, "groups": [{"key": …, "count": …}]}`. It takes exactly
the list filters above, so **the counts follow the current filter** — unlike
`/summary`, which always counts the whole workspace. Each `key` is the value
to filter the list by to open that group:

- `status`, `type`, `priority`: the snake_case value; every value is listed
  in fixed order, zero counts included.
- `assignee`: an IAM user id, or `none` for issues with no assignee. An issue
  with three assignees counts once in each of their groups, so the groups
  can add up to more than the number of issues.
- `pipeline`: a pipeline id, or `none` for issues about no pipeline.

**PATCH semantics.** Omitted fields are left alone. A board drag is
`{"status": "in_progress"}` alone.

- `due_date: ""` removes the due date; `pipeline_id: ""` detaches the issue.
- Assignees and labels change by lists, never by replacing the set:
  `add_assignee_ids` / `remove_assignee_ids`, `add_label_ids` /
  `remove_label_ids` (each at most 20, no duplicates). An added assignee must
  be a workspace member (400 naming the ones who are not). Removing does not
  check membership, so someone who has left can still be unassigned. `me` in
  `assignee_ids`, `add_assignee_ids` or `remove_assignee_ids` stands for the
  signed-in member.
- Relationships, by issue number: `parent_number` and `duplicate_of_number`
  (omitted = unchanged, `0` = clear, any other number = replace);
  `add_sub_issue_numbers` / `remove_sub_issue_numbers`;
  `add_blocked_by_numbers` / `remove_blocked_by_numbers`. A cycle of parents
  or an issue relating to itself is a 400 that says which.
- **Parent: replace from below, refuse from above.** A non-zero
  `parent_number` **replaces** the issue's current parent and writes **one**
  event with both `from` and `to` (`parent:3` → `parent:7`). But
  `add_sub_issue_numbers` naming an issue that already has another parent is
  **refused** (400 `workbench_parent_already_set`); clear that issue's parent
  first. This asymmetry is deliberate: changing your own parent is an explicit
  intent, taking another issue's child away is not.
- The reverse edges (`sub_issue`, `blocking`) appear
  in the other issue's `relations` by themselves.
- Setting a field to the value it already has is not a change and writes no
  timeline event.

## Comments

| Method | Path | Notes |
|---|---|---|
| GET | `/issues/:number/comments` | oldest first, cursor-paged |
| POST | `/issues/:number/comments` | `body` (markdown); optional `status` = "comment and mark as done", both in one batch; optional `mention_user_ids` |
| PATCH | `/issues/:number/comments/:comment_id` | `body` (required) and optional `mention_user_ids`; only the author may edit (403 otherwise, admins included) |
| DELETE | `/issues/:number/comments/:comment_id` | the author, or a workspace admin for anyone's comment (403 otherwise); allowed on a locked issue |

**Mentions.** `mention_user_ids` is the list of IAM user ids the member
@-mentioned, **as the editor recorded them** when the mention was inserted.
The server never derives mentions from the body text, so send the list
whenever the text mentions someone; `@alice` typed into the body alone
mentions nobody. At most 50, no duplicates; `me` is the signed-in member.
Ids are not checked against membership (someone who has left can still be
mentioned). On PATCH: **omitted or `null` keeps the mentions**, `[]` clears
them, a list replaces them — so an edit that only fixes a typo must leave
the field out. Every comment comes back with `mention_user_ids` (`[]` when
none).

Comments are not timeline events: merge `GET …/comments` with
`GET …/events` by time. On a **locked** issue only admins may comment or edit
a comment (403 `workbench_issue_locked`). **The assistant may post and edit
comments** (the timeline marks them as made via the assistant) but never
deletes one. When the member asks to see a comment before it is posted, write
the draft to a file in the working directory, let them read it, and post it
only once they say so.

## Timeline events

`GET /issues/:number/events`, oldest first. Each event has `kind`
(`created` `status` `field` `comment_meta` `pin` `lock` `attachment`), `field`
when `kind` is `field`, `from`/`to` (null = absent), `from_display`/
`to_display` (a name snapshot for labels, pipelines and attachment files),
`actor_id`, `via_assistant` and `batch_id` (merge a batch into one line).

- **A deleted comment** is a `comment_meta` event: `from` is the comment id
  and `comment_author_id` the comment's author (present only on this kind).
  When `comment_author_id` differs from `actor_id`, an admin deleted someone
  else's comment: show "deleted a comment by {author}".

- Status, type and priority values in `from`/`to` are the snake_case enums.
- **Relation events** (`kind: field`, `field: relation`): `from`/`to` is `<type>:<number>` — `parent:1`,
  `blocked_by:1`, `duplicate_of:3` — and `from_display`/`to_display` are null.
- **A relation event is written only on the issue that owns the edge**: adding
  a sub-issue writes `parent:N` on the sub-issue (the parent's timeline shows
  nothing); `blocked_by` is written on the blocked issue, not on the blocker.
  This is deliberate. To show both sides, read `relations` on each issue.

## Labels

`GET /labels` (any member). `POST /labels`, `PATCH /labels/:label_id`,
`DELETE /labels/:label_id` are admin-only. Names are unique per workspace,
case-insensitively (409 when taken); `color` is `#rrggbb`. A new workspace is
seeded with defaults, among them `blocked` and `not planned`, which the UI
reads by name. Deleting a label takes it off every issue.

## People

- `GET /members?q=`: up to 6 members whose name or email contains `q`
  (case-insensitive). Anyone listed here can be assigned.
- `GET /members?ids=a,b` (at most 50): resolve the IAM user ids you meet on
  issues, comments, events and attachments (`assignee_ids`, `actor_id`,
  `author_id`, `comment_author_id`, `uploader_id`, `created_by`) to `display_name` and `email`, in
  the order given. Someone who has left the workspace still resolves, with
  `is_member: false` — the timeline is history. An id nobody knows comes back
  with no name.

## Attachments

Attachments are **material, not fact**: a file on an issue does not make its
content true — facts are the issue's fields and comments.

| Method | Path | Notes |
|---|---|---|
| POST | `/issues/:number/attachments` | multipart: `file`, `what` (what it is), `from` (who gave it — a role, not a person's name), `dated` (the document's own date, `YYYY-MM-DD`), optional `supersedes` |
| GET | `/issues/:number/attachments` | metadata only |
| GET | `/attachments?pipeline_id=&issue=` | every attachment in the workspace, metadata only, cursor-paged (`paging` has `next_page_token` only, no `total_count`) |
| GET | `/issues/:number/attachments/:attachment_id/download` | the original bytes |
| DELETE | `/issues/:number/attachments/:attachment_id` | the uploader or an admin |

- At most **25 MiB** per file (413 beyond).
- Bytes are kept **byte-identical**: never transcoded, rewritten or
  compressed. The response header `X-Attachment-Sha256` carries the checksum;
  compare it with what you wrote to disk.
- A newer version is a **new upload** with `supersedes` set to the earlier
  attachment's id (same issue only; another issue's attachment is a 400). The
  earlier version stays — that is what makes the two diffable. Never delete
  the old one to "update" it.
- Downloads are always `application/octet-stream` with
  `Content-Disposition: attachment` and the original filename.
- **Pull only what exists.** Deleted attachments are left out of every list,
  and their bytes are gone. When mirroring attachments into a repository
  (for example into `references/`), take what the list returns now, write the
  three source fields (`what`, `from`, `dated`) next to each file, and do not
  resurrect anything the list no longer shows.
- Uploading is allowed on a locked issue.

## The assistant: `X-Asgard-Via-Assistant: true`

An agent acting for the member sends `X-Asgard-Via-Assistant: true` on every
request. Only the exact value `true` counts. It **grants nothing**: the
request runs with the member's own permissions — what the member cannot do,
the assistant cannot do. It marks the writes, so the timeline shows them as
made via the assistant.

With the header, these are refused with **403 `workbench_assistant_forbidden`**
even when the member could do them:

- deleting an issue; pinning or unpinning; locking or unlocking
- creating, renaming, recolouring or deleting labels
- deleting an attachment
- deleting a comment
- anything under `/v1/workbench/assistant/` — that is the member's own chat
  panel talking to you; you never call it

The assistant **may** create issues (several at once), change any sidebar
field, move statuses, set relationships, post and edit comments, upload
attachments, and read the audit log (below).

## Audit log

The workspace's Asgard Console › Explore records, read with the member's own
token. Console decides who may read them — a workspace owner or a platform
admin (IAM action `audit-log/read`); anyone else gets Console's 403, and the
right answer is to say so, not to report an empty summary. The shapes are
Console's and come back unchanged.

| Method | Path | Notes |
|---|---|---|
| GET | `/audit-log/dictionary` | display names for the raw keys on rows (projects, accounts, agents, events, products) |
| GET | `/audit-log/options/:dimension` | the values one dimension takes in a range, with counts; query string passed through |
| POST | `/audit-log/query` | Console's query body; the answer streams as JSON Lines (`meta`, then `row`s, then `end` with `nextCursor`; a late failure is an `error` line) |

Reading it right: rows carry **raw keys only** (namespace, IAM user id, CR
name) — translate them with the dictionary and show the raw key when there is
no entry. There is **no success/failure dimension**: events are named
(`user_prompt`, `assistant_response`, `tool_call`, `subagent_start`,
`subagent_complete`, `model_usage`, `run_done`, `run_error`, `other`), so never
summarise as "N failed operations". The account may be null (an external API
caller or a bot), debug runs are excluded by default, and data lags by up to
about 20 minutes.

## Error codes

| HTTP | `details.error_code` | Meaning, and what to do |
|---|---|---|
| 409 | `workbench_conflict_retry` | the write lost a race with another write at the same moment and nothing was written (the server already retried once). Re-read the issue and try again |
| 403 | `workbench_assistant_forbidden` | the assistant may not do this; ask the member to do it themselves |
| 403 | `workbench_issue_locked` | the issue is locked and only admins may comment on it |
| 400 | `workbench_pin_limit_reached` | the workspace already has 3 pinned issues; unpin one first |
| 400 | `workbench_parent_already_set` | the issue you made a sub-issue already has another parent; clear it first |
| 400 | `workbench_unknown_query_param` | the request sent a renamed query parameter (`deployment`); send `pipeline_id` instead |
| 402 | `workbench_subscription_required` | the workspace has no active subscription, so the assistant cannot run; the issues themselves still work |

`workbench_pin_limit_reached` and `workbench_parent_already_set` are attached
when the backend reports the reason; a 400 for either without the code still
says which in its `message`.

Other failures carry a `message` saying which rule was broken (a 400 for bad
input or a refused relation, 403 for a permission the member lacks, 404 for an
issue, comment or attachment that does not exist or was deleted).

## Known limit: no atomic batch across issues

Each request is one batch on **one issue**: it applies entirely or not at all.
There is **no request that changes several issues atomically**. When you open
or change several issues at once, do it issue by issue, check each response,
and report exactly which ones succeeded and which did not — never assume a set
landed together, and do not leave the member believing a half-applied set is
complete.
