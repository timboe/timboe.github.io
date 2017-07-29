---
layout: page
title: Publications
permalink: /publications/
feature-img: "img/header_04.jpg"
---

[Publications on INSPIRE](https://inspirehep.net/author/profile/T.A.Martin.1){: .button}

## Main Publications

 > Papers and notes in which I made major contributions.

{% for contribution in site.data.talks_pubs.pubs %}
{% if contribution.cat == "1" %}
------
* **{{ contribution.type }}**: {{ contribution.title }}
  *  {{ contribution.author }}, [{{ contribution.display }}]({{ contribution.link }})
{% endif %}
{% endfor %}
------

## Additional Publications

 > Papers and notes in which I have editorial involvement through editorial boards and physics convenorship.

{% for contribution in site.data.talks_pubs.pubs %}
{% if contribution.cat == "2" %}
------
* **{{ contribution.type }}**: {{ contribution.title }}
  *  {{ contribution.author }}, [{{ contribution.display }}]({{ contribution.link }})
{% endif %}
{% endfor %}
------
