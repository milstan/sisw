---
layout: default
title: SISW
---

<style>
  /* Match GitHub's own README rendering for wide tables: collapse to
     horizontal-scroll on narrow viewports rather than squeezing the
     summary column into a tall narrow strip. Primer applies
     `display: table !important` so we use !important to win the
     cascade.

     The trick that actually produces horizontal scroll (vs just block
     layout) is wrapping the inner table-cell layout in a child that
     keeps its natural width. We can't add a wrapper around the
     markdown-rendered table, so we use display:block on the outer
     table and put the table-layout children back into table mode at
     min-width: 100% so they extend horizontally past the viewport. */
  .markdown-body table {
    display: block !important;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
    max-width: 100%;
  }
  .markdown-body table > thead,
  .markdown-body table > tbody {
    display: table;
    min-width: 100%;
    width: max-content;
  }
  /* Cells align to top so the Speaker name stays visible even when the
     summary cell is many lines tall. */
  .markdown-body table th,
  .markdown-body table td { vertical-align: top !important; }
  /* On desktop, summary column wraps to a comfortable line length
     (~70 chars) instead of stretching to fill the available width. */
  .markdown-body table td:nth-child(4) { max-width: 56ch; white-space: normal; }
</style>

# SISW

**Self-Improving Software Workshop** — a gathering of people building things. Each speaker gives a short talk on what they're working on and what they've learned. Audience: other builders.

> **Date and venue:** TBA — submit anyway, organizers will follow up via your GitHub profile as we firm up the schedule.
>
> **Format:** ~10 minute talks, slides or live demo. **Organizer:** [@milstan](https://github.com/milstan).

[**→ Submit your talk**](https://github.com/milstan/sisw/issues/new?template=talk-submission.yml)

*Submissions open as a GitHub issue, get auto-converted into a PR, and appear in the table below once an organizer merges. One talk per speaker; gist URLs are welcome.*

---

## Who's coming

{% assign talks = site.data.talks %}
{% if talks and talks.size > 0 %}

| Speaker | Startup | Project / gist | What they're talking about |
|---|---|---|---|
{% for t in talks -%}
| {% if t.submitter_github %}[{{ t.first }} {{ t.last }}](https://github.com/{{ t.submitter_github }}) (@{{ t.submitter_github }}){% else %}{{ t.first }} {{ t.last }}{% endif %} | [{{ t.domain }}](https://{{ t.domain }}) | [{{ t.repo | remove: 'https://github.com/' | remove: 'http://github.com/' | remove: 'https://gist.github.com/' | remove: 'http://gist.github.com/' }}]({{ t.repo }}) | {{ t.summary }} |
{% endfor %}

{% else %}
*No talks yet — be the first to share what you're building.*
{% endif %}
