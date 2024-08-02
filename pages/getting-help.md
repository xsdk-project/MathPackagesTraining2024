---
layout: page
show_meta: false
title: "Getting help"
header:
   image_fullwidth: "tech_support8.jpg"
permalink: "/getting-help/"
---
{% assign vroom = nil %}
{% for vr in site.data.vrooms %}
  {% if vr.name == "Amphitheater" %}
    {% assign vroom = vr %}
    {% break %}
  {% endif %}
{% endfor %}

SLACK ALCF-Workshops workspace provides channles for help

* [#atpesc-2024-helpdesk](https://alcf-workshops.slack.com/archives/C07DL3ZASF5)
* [#atpesc-2024-track-5-numerical](https://alcf-workshops.slack.com/archives/C07DL3F7A59)
* [#atpesc-2024-track-5-numerical-breakout](https://alcf-workshops.slack.com/archives/C07FCTENW12)

{% include link-shortcuts %}
