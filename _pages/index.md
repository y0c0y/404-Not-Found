---
layout: page
title: Home
id: home
permalink: /
---

# Welcome! ☘️

<p style="padding: 3em 1em; background: #f5f7ff; border-radius: 4px;">
  <span style="font-weight: bold">[[y0c0y]]</span> 의 소개 입니다!
</p>

<strong>최근 업로드한 노트들</strong>

<ul>
  {% assign recent_notes = site.notes | sort: "last_modified_at_timestamp" | reverse %}
  {% for note in recent_notes limit: 5 %}
    <li>
      {{ note.last_modified_at | date: "%Y-%m-%d" }} — <a class="internal-link" href="{{ site.baseurl }}{{ note.url }}">{{ note.title }}</a>
    </li>
  {% endfor %}
</ul>

<style>
  .wrapper {
    max-width: 46em;
  }
</style>
