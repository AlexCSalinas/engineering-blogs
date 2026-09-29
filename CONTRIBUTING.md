# Contributing

The whole list is the table in [README.md](README.md). Adding a post is one row. No files, no sections.

The bar: **you read the post.** Nothing in a row proves that, so it's on you — an unread link costs the next person the time it takes to find out it wasn't worth it.

## How

1. Add a row at the bottom of the table in `README.md`:

   ```markdown
   | [<Exact post title>](<url>) | <Company> | `tag` `tag` `tag` | <YYYY-MM-DD> |
   ```

   Use the post's exact title and its original publication date.

2. Open a PR titled with the post title. One post per PR — easy to discuss, easy to revert.

## Tags

Two or three, lowercase, hyphenated, in backticks. Reuse tags already in the table before inventing one — the tags are the only way to find anything here, and they only work if they group things.

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

Anyone with write access can merge. Check that the link works, the title and date match the post, and the tags are reused rather than invented. If you want to argue a post doesn't clear the bar, say so in the PR — that's what the PRs are for.
