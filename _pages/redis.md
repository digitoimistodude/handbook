---
ID: 380
post_title: Redis
author: Timi Wahalahti
post_excerpt: ""
layout: page
permalink: http://handbook.dude.fi/palvelimet/redis
published: true
post_date: 2019-01-25 14:48:46
---
Palvelimilla on asennettuna <a href="https://redis.io/">Redis</a> object-cache joka nopeuttaa sivustojen toimintaa huomattavasti. Kaikila vanhoilla sivustoilla ei ole Redistä käytössä ja uusissakin projekteissa se otetaan käyttöön tarvekohtaisen harkinnan perusteella.

Rediksen käyttämiseksi sivustolle on asennettava <a href="https://wordpress.org/plugins/redis-cache/">Redis Object Cache</a> -lisäosa (automaattisesti uusissa projekteissa), <code>config/application.php</code> tiedostoon lisättävä Rediksen <a href="https://github.com/digitoimistodude/dudestack/blob/5f0c2f6b4d676403e7265e24601faf23c269afd6/config/application.php#L51-L58">asetukset</a> (automaattisesti uusissa projekteissa) sekä <code>.env</code> tiedostoon lisättävä Rediksen salasana.
<h2>Hyödyllisiä komentoja</h2>
<h3>Monitorointi</h3>
Rediksen käyttöönoton jälkeen sen toimintaa kannattaa tarkkailla hetki komennolla
<pre class="language-bash"><code class="language-bash">redis-cli -a PASSWORD monitor</code></pre>
