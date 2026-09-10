---
permalink: /seminars/
title: "Algebraic Models for Spaces"
author_profile: false
---
{% assign seminar = site.data.seminar %}
{% comment %}
  The content of this page comes from _data/seminar.yml -- edit that file to
  add a talk or to attach notes to one. The "Notes" column below appears
  automatically as soon as at least one talk has a `notes:` link.
{% endcomment %}
{% assign has_notes = false %}
{% for talk in seminar.talks %}{% if talk.notes and talk.notes != "" %}{% assign has_notes = true %}{% endif %}{% endfor %}
{% if has_notes %}{% assign columns = 4 %}{% else %}{% assign columns = 3 %}{% endif %}

{% if seminar.semester %}*{{ seminar.semester }}*{% endif %}

{% if seminar.description %}{{ seminar.description | markdownify }}{% endif %}

**Practical information**

{% if seminar.when %}-**When:** {{ seminar.when }}  
{% endif %}{% if seminar.where %}-**Where:** {{ seminar.where }}  
{% endif %}{% if seminar.audience %}-**Who:** {{ seminar.audience }}  
{% endif %}{% if seminar.organisers %}-**Organised by:** {% for o in seminar.organisers %}{% if o.url %}[{{ o.name }}]({{ o.url }}){% else %}{{ o.name }}{% endif %}{% unless forloop.last %} and {% endunless %}{% endfor %}  
{% endif %}{% if seminar.syllabus %}-[Syllabus]({{ seminar.syllabus }})  
{% endif %}

## Programme

{% if seminar.talks and seminar.talks.size > 0 %}
<table>
  <thead>
    <tr>
      <th>Date</th>
      <th>Talk</th>
      <th>Speaker</th>
      {% if has_notes %}<th>Notes</th>{% endif %}
    </tr>
  </thead>
  <tbody>
  {% assign current_part = "" %}
  {% for talk in seminar.talks %}
    {% if talk.part and talk.part != current_part %}
    <tr>
      <td colspan="{{ columns }}"><strong>{{ talk.part }}</strong></td>
    </tr>
    {% assign current_part = talk.part %}
    {% endif %}
    <tr>
      <td>{% if talk.date %}{{ talk.date | date: "%-d %b %Y" }}{% else %}TBA{% endif %}</td>
      <td>{% if talk.number %}Talk {{ talk.number }}. {% endif %}{{ talk.title | default: "TBA" }}{% if talk.details %}<br /><small>{{ talk.details | markdownify | remove: "<p>" | remove: "</p>" | strip_newlines }}</small>{% endif %}</td>
      <td>{% if talk.speaker %}{% if talk.url %}<a href="{{ talk.url }}">{{ talk.speaker }}</a>{% else %}{{ talk.speaker }}{% endif %}{% elsif talk.number %}TBA{% else %}&mdash;{% endif %}</td>
      {% if has_notes %}<td>{% if talk.notes and talk.notes != "" %}<a href="{{ talk.notes }}">Notes</a>{% else %}&mdash;{% endif %}</td>{% endif %}
    </tr>
  {% endfor %}
  </tbody>
</table>
{% else %}
The programme will appear here soon.
{% endif %}

{% if seminar.contact %}{{ seminar.contact | markdownify }}{% endif %}
