# Contributing

The bar for this repo is simple: **you read the post, and you can say something specific about it.** A link with a generated summary attached is worse than no link, because it costs the next person time to find that out.

## Adding a post

1. Copy the template:
   ```sh
   cp blogs/_TEMPLATE.md blogs/company-short-title.md
   ```
   Name the file `company-short-title.md` — lowercase, hyphens, no dates in the filename.

2. Fill it in. All header fields are required except `Topics`, which should still have two or three.

3. Add a row to **both** tables in [README.md](README.md): the main index and the by-topic list. Keep the index sorted by nothing in particular for now — newest at the bottom is fine.

4. Open a PR with the post title as the PR title. One post per PR, so they're easy to discuss and easy to revert.

## What belongs here

- Engineering posts from teams describing something they actually built and ran.
- Postmortems, architecture retrospectives, "why we rewrote X," migration writeups.
- Deep technical posts from individuals, if they're substantive.

## What doesn't

- Marketing posts with an architecture diagram stapled on.
- Tutorials and getting-started guides. Useful, wrong repo.
- Conference talks and papers as primary entries — link them under **Notes** on a related post instead.
- Posts you haven't read.

## Style

- **Summary** is a paragraph in your own words. If it reads like the post's own abstract, rewrite it.
- **Key takeaways** are specific. `Uses a custom storage layer` is not a takeaway; `built LedgerStore in-house because off-the-shelf DBs couldn't give tamper-evident records under their regulatory constraints` is.
- Include real numbers when the post gives them, and say they're the post's claims rather than measured facts.
- Say what the post gets wrong or skips. That's the most valuable part of an entry and the part you can't get anywhere else.

## Reviewing

Anyone with write access can merge. Look for: does the summary match the post, are the takeaways specific, do the links work. Don't bikeshed prose.
