# Contributing

Everything lives in [README.md](README.md). Adding a post means editing that one file — there are no per-post files.

The bar is simple: **you read the post, and you can say something specific about it.** A link with a generated summary attached is worse than no link, because it costs the next person time to find that out.

## How

1. Open `README.md` and find the topic section your post fits. Add a new `##` section if none do, and link it in the **Jump to** line at the top.
2. Paste the skeleton below at the end of that section and fill it in.
3. Open a PR titled with the post title. One post per PR, so they're easy to discuss and easy to revert.

## Skeleton

```markdown
### <Exact post title>

**[domain.com](<url>)** · <Company> · <Author(s)> · <YYYY-MM-DD>
`tag-one` `tag-two` `tag-three` · added by @<your-handle>

<Two or three sentences: what does this post give you that a dozen others on the
same topic don't? Be specific and be honest — "great read" helps nobody.>

- **<Idea>** — <what it is and why it matters>
- **<Idea>** — <...>
- **<Idea>** — <...>
```

Keep entries separated by a `---` rule, same as the existing ones.

## What belongs here

- Engineering posts from teams describing something they actually built and ran.
- Postmortems, architecture retrospectives, "why we rewrote X," migration writeups.
- Deep technical posts from individuals, if they're substantive.

## What doesn't

- Marketing posts with an architecture diagram stapled on.
- Tutorials and getting-started guides. Useful, wrong repo.
- Conference talks and papers as primary entries — link them as a bullet on a related post instead.
- Posts you haven't read.

## Style

- Write the summary in your own words. If it reads like the post's own abstract, rewrite it.
- Takeaways are specific. `Uses a custom storage layer` is not a takeaway; `built LedgerStore in-house because off-the-shelf DBs couldn't give tamper-evident records under their regulatory constraints` is.
- Include real numbers when the post gives them, and frame them as the post's claims rather than measured facts.
- Say what the post gets wrong or skips. That's the most valuable part of an entry and the part you can't get anywhere else.
- Three to five bullets. If you need more, the post deserves its own writeup somewhere else.

## Reviewing

Anyone with write access can merge. Check that the summary matches the post, the takeaways are specific, and the links work. Don't bikeshed prose.
