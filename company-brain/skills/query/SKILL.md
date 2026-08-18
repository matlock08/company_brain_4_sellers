---
name: query
description: Queries the wiki looking for the requested information.
allowed-tools: [Optional list of permitted tools]
---

# Skill Documentation

## Instructions
1. Read `index.md`, then only the relevant pages under `wiki/`.
2. Answer using **only** information found in `wiki/` pages. Do not use `raw_sources/` directly, prior conversation memory, or general/external knowledge to fill gaps — if the wiki doesn't say it, the answer is "not in the wiki," not an inference. `raw_sources/` is the wiki's own evidence trail and may be opened only to verify a citation the wiki already makes, never as an independent source of new facts.
3. For every claim in the answer, cite the specific wiki page as a link (and section/heading if the page is long). Re-read the cited passage before including it and confirm it still supports the claim as written — don't cite from memory of an earlier read in this conversation, since pages may have changed. If a claim can't be traced to a specific current wiki passage, drop it or flag it as unconfirmed rather than stating it plainly.
4. Note staleness where relevant: if the cited page's `updated` frontmatter is old relative to the question, or the page itself flags the fact as unresolved/unconfirmed, say so rather than presenting it as settled.
5. Offer to file valuable answers back as a wiki page (analyses, comparisons, prioritizations compound too — file under `wiki/` and log as `exploration`).

## Examples
Concrete usage scenarios