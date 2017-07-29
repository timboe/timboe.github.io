---
layout: page
title: Talks
permalink: /talks/
feature-img: "img/header_05.jpg"
---

> A record of all my coference and public talks.

{% for contribution in site.data.talks_pubs.talks %}
------
* **{{ contribution.conf_short }}**: {{ contribution.conf_long }}, _{{ contribution.conf_location }}_ 
{% if contribution.talk %}  * **Talk:** {{ contribution.talk }}, [{{ contribution.talk_display }}]({{ contribution.talk_link }})
{% endif %}{% if contribution.poster %}  * **Poster:** {{ contribution.poster }}, [{{ contribution.poster_display }}]({{ contribution.poster_link }})
{% endif %}{% if contribution.proc_display %}  * **Proceedings:** [{{ contribution.proc_display }}]({{ contribution.proc_link }})
{% endif %}
{% endfor %}
------
