---
layout: page
permalink: /talk/
title: Talks
description: 
nav: true
nav_order: 3
---

<!-- Add this CSS block to your CSS file or inside a <style> tag -->
<style>
    .talks-title {
        -webkit-user-select: none; /* Safari */
        -moz-user-select: none;    /* Firefox */
        -ms-user-select: none;     /* Internet Explorer/Edge */
        user-select: none;         /* Non-prefixed version, currently supported by Chrome and Opera */
        /* Keep the existing color, assuming it's defined somewhere else or inherited */
    }
</style>

<!-- pages/talks.md -->
<div class="talks">
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
</div>
