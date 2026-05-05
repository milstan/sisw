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

  /* Submit CTA — the single most important pixel on the page.
     Minimal theme styles all anchors as plain blue text, so the link
     blends with every other link nearby. Make it visually distinct:
     real button shape, comfortable padding, hover-darken. */
  a.submit-cta {
    display: inline-block;
    padding: 12px 22px;
    margin: 8px 0 12px 0;
    background: #267CB9;
    color: #fff !important;
    border-radius: 6px;
    font-weight: 700;
    font-size: 16px;
    text-decoration: none;
    border: 1px solid #1f6699;
    box-shadow: 0 1px 0 rgba(0,0,0,0.05);
  }
  a.submit-cta:hover, a.submit-cta:focus {
    background: #1f6699;
    color: #fff !important;
    text-decoration: none;
    font-weight: 700;
  }

  /* Event details strip — sits above the CTA so a speaker knows when/where
     before clicking. */
  .event-details {
    background: #f6f8fa;
    border: 1px solid #e1e4e8;
    border-radius: 6px;
    padding: 10px 14px;
    margin: 12px 0;
    font-size: 14px;
  }
  .event-details strong { color: #222; }
</style>

# SISW

**Self-Improving Software Workshop** — a gathering of people building things. Each speaker gives a short talk on what they're working on and what they've learned. Audience: other builders.

<div class="event-details" markdown="1">
**Date and venue:** TBA — submit anyway, organizers will follow up via your GitHub profile as we firm up the schedule.<br>
**Format:** ~10 minute talks, slides or live demo. <strong>Organizer:</strong> <a href="https://github.com/milstan">@milstan</a>.
</div>

<a class="submit-cta" href="https://github.com/milstan/sisw/issues/new?template=talk-submission.yml">→ Submit your talk</a>

*Submissions open as a GitHub issue, get auto-converted into a PR, and appear in the table below once an organizer merges. One talk per speaker; gist URLs are welcome.*

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
