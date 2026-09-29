# Contributing

The whole list is the table in [README.md](README.md). Adding a post is one row. No files, no sections.

The bar: **you read the post, and you can say something specific about it.** A link with a generated blurb attached is worse than no link, because it costs the next person time to find that out.

## How

1. Add a row at the bottom of the table in `README.md`:

   ```markdown
   | [<Exact post title>](<url>) | <Company> | `tag` `tag` `tag` | <YYYY-MM-DD> | @<your-handle> | <one line> |
   ```

2. Open a PR titled with the post title. One post per PR — easy to discuss, easy to revert.

## Writing the "Why read it" line

One line, and specific. It answers *why this post and not the dozen others on the same topic.*

- Good: `Immutable, zero-sum money orders: two invariants that survived a decade of new business lines`
- Bad: `Great deep dive into payments architecture`

Name the actual mechanism, the surprising number, or the claim the post is making. If the post's best feature is a benchmark result or a technique with a name, that's your line. Skip adjectives.

## Tags

Two or three, lowercase, hyphenated, in backticks. Reuse tags already in the table before inventing one — the tags are only useful if they group things.

## What belongs here

- Engineering posts from teams describing something they actually built and ran.
- Postmortems, architecture retrospectives, "why we rewrote X," migration writeups.
- Deep technical posts from individuals, if they're substantive.

## What doesn't

- Marketing posts with an architecture diagram stapled on.
- Tutorials and getting-started guides. Useful, wrong repo.
- Papers and conference talks — link the post that covers them instead.
- Posts you haven't read.

## Reviewing

Anyone with write access can merge. Check that the link works, the tags are reused rather than invented, and the line says something real. Don't bikeshed prose.
