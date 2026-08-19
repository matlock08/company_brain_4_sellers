# Company Brain: agent instructions

This folder is a personal knowledge wiki. You maintain it. I think with it.
When I give you new information, your job is to fold it into the right pages
and keep the whole thing consistent. Do the bookkeeping so I don't have to.

# Wiki Schema

You (the LLM agent) are the maintainer of this account knowledge wiki. The human curates sources, directs analysis, and makes the calls; you do all filing, cross-referencing, synthesis, and bookkeeping. This file defines the structure, conventions, and workflows. Follow it exactly; propose changes to it rather than silently deviating.

Pattern origin: Karpathy's LLM Wiki, adapted for role work. Core principle: **the wiki is a persistent, compounding artifact** — knowledge is integrated once and kept current, never re-derived from scratch.

## Directory layout

```
CLAUDE.md            ← this schema
index.md             ← catalog of every wiki page; read this FIRST on any task
log.md               ← append-only journal of ingests/queries/lints
raw_sources/         ← immutable raw sources. READ-ONLY. Never edit, never delete.
wiki/
  overview.md        ← living synthesis of [COMPANY] state (you keep it current)
  competitors/       ← one page per validated competitor product detected
  heat_map/          ← one page with a heat map table where columns are the Sales Plays products and one row per [COMPANY]
  org_chart/         ← one page with organization chart and one page per people with profile, linkedin information is pulled when available
  topics/            ← All other topics files
  whitespaces/       ← Documents with a compelling reason to act for all the opportunities to position any of the Sales Plays that are empty or with a clear chance to expand on the given the research on industry trends , linkedin profile signals or internal evidence provided by team
```

Source filenames: `YYYY-MM-DD_<type>.md` where `<type>` ∈ `meeting | internal | research | exploration`.

### Competitors pages — `wiki/competitors/<competitor>.md`

Frontmatter: `type: competitor`, `status: active | inactive`, `date`, `decider`, `updated`.

Sections: **Competitor's name and context** · **Actual known products in the account** · **Key IBM differentiator against competitor ** · **Competitors Weakness** (what observable facts would reopen this) · **Related**.

Rules: Competitor pages are NEVER deleted. When competitor has an active, deployed product 
`status: active` when competitor software no longer in use status  `status: inactive`. During lint, check each active competitor against new evidence.

### Heat Map pages — `wiki/heat_map/heat_map.md`

Frontmatter: `type: heat_map`, `status: active`, `date`, `updated`.

Sections: 
**Table** with his format that maps any existing Open Opportunity on ISC (Salesforce) with their corresponding Sales Play from IBM, add a single row with customer Name and fill the corresponding columns with and **X** if the opportunity existing Open (Not lost) or **IB** for Installed Base blanks if we don't have any opportunity in the current fiscal year.
<table>
  <thead>
    <tr>
      <th>Customer</th>
      <th colspan="3">Storage</th>
      <th>Z Stack</th>
      <th colspan="3">Power/Cloud</th>
      <th colspan="5">Data</th>
      <th colspan="7">Automation</th>
      <th>Expert Labs</th>
      <th colspan="2">TLS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Customer Name</td>
      <td>Flash</td>
      <td>Fusion</td>
      <td>Data Resiliency</td>
      <td>HW LinuxONE</td>
      <td>PVS</td>
      <td>Power</td>
      <td>Cloud</td>
      <td>AI</td>
      <td>Business Automation</td>
      <td>Databases</td>
      <td>Data Integration & Intelligence</td>
      <td>Data Security</td>
      <td>App Development</td>
      <td>App Integration</td>
      <td>Infra Automation</td>
      <td>Network Mgmt</td>
      <td>Identity & Asset Mgmt</td>
      <td>IT Automation & FinOps</td>
      <td>Asset Lifecycle Mgmt</td>
      <td>Expert Labs</td>
      <td>Logo</td>
      <td>MVS</td>
    </tr>
  </tbody>
</table>
**Summary of important opportunities or recent changes**.

Rules: Keep a single row with customer name NEVER deleted the row. If a new Opportunity is registered on ISC (SalesForce) review the list of products on the opportunity and map them against their corresponding Sales Play from IBM to identify the column where they belong. Update the date with the latest review of this heatmap. During lint, check each active Opportunity reversal conditions against new evidence and update Accordingly.

### Org Chart pages — `wiki/org_chart/org_chart.md`

Frontmatter: `type: org_chart`, `status: active`, `date`,  `updated`.

Sections: **Org Chart View**  With Name and current Position add a link to a detailed page of the person where you should add based on LinkedIn profile url, brief Summary, and latest communication, events attended, workshops where they have participated.

Rules: Org Chart pages are NEVER deleted or rewritten after the fact. New changes updates the field `updated`. During lint, check each active position.

### Topics pages — `wiki/topics/YYYY-MM-DD_<topic>.md`

Frontmatter: `type: topic`, `status: active`, `date`, `updated`.

Sections: **Context** · **Summary**.

Rules: Topics pages are NEVER deleted or rewritten after the fact.

### Whitespaces pages — `wiki/whitespaces/YYYY-MM-DD_<brand>_white_space.md`

Frontmatter: `type: whitespace`, `status: active`, `date`, `updated`.

Sections: **Context** · **Summary**.

Rules: Whitespaces pages are NEVER deleted or rewritten after the fact. New changes updates the field `updated`. During lint, check each sales play.


