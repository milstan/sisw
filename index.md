---
layout: default
title: SISW
---

# SISW

A gathering of people building things. Each speaker gives a short talk about what they're working on and what they've learned.

[**→ Submit your talk**](https://github.com/milstan/sisw/issues/new?template=talk-submission.yml)

Submissions open as a GitHub issue, get auto-converted into a PR, and appear in the table below once an organizer merges.

---

## Who's coming

{% assign talks = site.data.talks %}
{% if talks and talks.size > 0 %}
<table>
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
*No talks yet — be the first.*
{% endif %}
