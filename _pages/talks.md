---
layout: page
permalink: /talk/
title: Talks
description: Listed here are invited presentations. For further project talks, check my <a href='https://jorgeacunam.github.io/assets/pdf/CV_Jorge_Acuna_2024.pdf'>CV by clicking HERE</a>.
nav: true
nav_order: 3
---


<!-- pages/talks.md -->
<div class="talks">
{% if site.talks != blank -%} 
<div class="table-responsive">
    <table class="table table-sm table-borderless">
    {%- assign talks = site.talks | reverse -%} 
    {% for item in talks %} 
    <tr>
        <th scope="row">{{ item.date | date: "%b %-d, %Y" }}</th>
        <td>
        {% if item.inline -%} 
            {{ item.content | remove: '<p>' | remove: '</p>' | emojify }}
        {%- else -%} 
            <a class="talks-title" href="{{ item.url | relative_url }}">{{ item.title }}</a>
        {%- endif %} 
        </td>
        <td>
        {% if item.place -%} 
            <span class="talks-place">{{ item.place }}</span>
        {%- endif %}
        </td>
    </tr>
    {%- endfor %} 
    </table>
</div>
{%- else -%} 
<p>No talks so far...</p>
{%- endif %} 
</div>
