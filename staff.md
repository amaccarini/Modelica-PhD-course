---
layout: page
title: Staff
description: A listing of all the course staff members.
---

#  🐼&zwj;🏫 Staff Staff

Staff information is stored in the `_staffers` directory and rendered according to the layout file, `_layouts/staffer.html`.

{% for staffer in site.staffers %}
{{ staffer }}
{% endfor %}
