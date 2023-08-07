---
layout: page
title: Agenda
nav_order: 2
description: Listing of course modules and topics.
---

# 📅 Agenda

{% for module in site.modules %}
{{ module }}
{% endfor %}
