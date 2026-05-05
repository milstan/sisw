---
layout: default
title: SISW
---

<style>
  /* The minimal theme renders content into a 500px-wide section, which
     squeezes the talks table's summary column into a tall narrow strip.
     Widen the wrapper + section at desktop widths so the four columns get
     reasonable proportions, then constrain each column so a long summary
     doesn't push everything else off-screen. */
  @media (min-width: 1100px) {
    .wrapper { width: 1100px; }
    section  { width: 780px; }
  }
  table.talks { table-layout: fixed; width: 100%; }
  table.talks th, table.talks td { vertical-align: top; word-wrap: break-word; overflow-wrap: anywhere; }
  table.talks th:nth-child(1), table.talks td:nth-child(1) { width: 18%; }
  table.talks th:nth-child(2), table.talks td:nth-child(2) { width: 16%; }
  table.talks th:nth-child(3), table.talks td:nth-child(3) { width: 22%; word-break: break-all; }
  table.talks th:nth-child(4), table.talks td:nth-child(4) { width: 44%; }

  /* Below ~720px the minimal theme drops to a single-column flow. The
     four-col table still fits in the viewport but speaker names need to
     wrap (no nowrap), and the summary column shouldn't dominate.
     Stacked-card-on-mobile would be nicer; the row layout keeps the
     spec's "table" promise. */
  @media (max-width: 720px) {
    table.talks th:nth-child(4), table.talks td:nth-child(4) { width: 36%; }
    table.talks th:nth-child(1), table.talks td:nth-child(1) { width: 22%; }
  }
</style>

# SISW

**Self-Improving Software Workshop** — a gathering of people building things. Each speaker gives a short talk on what they're working on and what they've learned. Audience: other builders.

[**→ Submit your talk**](https://github.com/milstan/sisw/issues/new?template=talk-submission.yml)

Submissions open as a GitHub issue, get auto-converted into a PR, and appear in the table below once an organizer merges. One talk per speaker; gist URLs are welcome.

---

## Who's coming

{% assign talks = site.data.talks %}
{% if talks and talks.size > 0 %}
<table class="talks">
  <thead>
    <tr>
      <th>Speaker</th>
      <th>Startup</th>
      <th>Repo</th>
      <th>What they're talking about</th>
    </tr>
  </thead>
  <tbody>
  {% for t in talks %}
    <tr>
      <td>{{ t.first }} {{ t.last }}</td>
      <td><a href="https://{{ t.domain }}" rel="noopener">{{ t.domain }}</a></td>
      <td><a href="{{ t.repo }}" rel="noopener">{{ t.repo | remove: 'https://github.com/' | remove: 'http://github.com/' | remove: 'https://gist.github.com/' | remove: 'http://gist.github.com/' }}</a></td>
      <td>{{ t.summary }}</td>
    </tr>
  {% endfor %}
  </tbody>
</table>
{% else %}
*No talks yet — be the first to share what you're building.*
{% endif %}
