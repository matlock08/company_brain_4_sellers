---
name: ingest
description: Processes new files from raw_sources and Updates the wiki with new information.
allowed-tools: [linkedin]
---

# Skill Documentation

## Instructions
1. Read the new file in `raw_sources/`. 
2. Tell the ATL the 3–5 key takeaways. 
3. Update Competitors, Org Chart, Heat Map pages or create new Topics (bump `mentions`, extend evidence). For Org Chart people, check LinkedIn for updates on profile and activity — but treat it as a secondary, often-stale channel: many stakeholder profiles go months or years without meaningful posts, so a quiet profile is not evidence of anything. Only record a LinkedIn signal if it's a specific post, comment, or activity, and note its age; do not infer interest or pain points from silence or from generic/reposted content (course listicles, motivational posts).
4. Update `wiki/overview.md` if the picture changed. Lead the page with the account name as an H1 title (e.g. `# ProceSAR`), not just buried in the `State as of` heading, so the account is identifiable at a glance. Track regulatory context (e.g. CONSAR, SAR framework) as its own section — capture the specific regulator by name (don't default to a generic "regulator"), and log new circulars, deadlines, or obligations as they surface in sources. Order sections so the most decision-relevant information leads: regulatory changes and open gaps/risks near the top, ahead of static background (org, competitor catalog) — whatever most changed or is most time-sensitive this update should be easiest to find.
5. Update `index.md`. 
6. Append to `log.md`.

Skip rule: if a source changes no Competitors, Heat Map, Org Chart — say so and file
nothing beyond the log line.

