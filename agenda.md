---
layout: page
title: 📅 Agenda
nav_order: 2
description: Listing of course modules and topics.
---

# 📅 Agenda (Preliminary)

{% for module in site.modules %}
{{ module }}
<br>
{% endfor %}
