---
ID: 384
post_title: fail2ban
author: Timi Wahalahti
post_excerpt: ""
layout: page
permalink: >
  http://handbook.dude.fi/palvelimet/fail2ban
published: true
post_date: 2019-01-25 15:15:11
---
Pääsy palvelimille on rajoitettu sekä tehty muita tietoturvaa parantavia toimenpiteitä. Yksi näistä toimenpiteistä on palvelimille asennettu <a href="https://github.com/fail2ban/fail2ban">fail2ban</a> joka tarkkailee erilaisia lokitiedostoja ja tarvittaessa estää IP-osoitteen josta tulee haitalliselta vaikuttavaa liikennettä tai hyökkäys. Fail2ban monitoroi mm. WordPressin kirjautumisyrityksiä sekä yleisesti http(s) pyyntöjen määrää. Asetetut estot nollautuvat automaattisesti määrätyn ajan kuluttua.
<h2>Hyödyllisiä komentoja</h2>
Alla on listattu yleisimmin käytetyt hyödylliset komennot. Täyden listan mahdollisista komennoista löydät fail2banin <a href="https://www.fail2ban.org/wiki/index.php/Commands">wikistä</a>.
<h3>Listaa käytössä olevat tarkistukset</h3>
<pre class=" language-bash"><code class=" language-bash">sudo fail2ban-client status</code></pre>
<h3>Aktiivisten estojen tarkistaminen</h3>
Listaa estot tarkistuskohtaisesti:
<pre class=" language-bash"><code class=" language-bash">sudo fail2ban-client status JAILNAME</code></pre>
Listaa kaikki aktiiviset estot:
<pre class=" language-bash"><code class=" language-bash">sudo iptables --list-rules</code></pre>
<h3>Eston poistaminen</h3>
<pre class=" language-bash"><code class=" language-bash">sudo fail2ban-client set JAILNAME unbanip IP</code></pre>
<h3>Eston manuaalinen asettaminen</h3>
<pre class=" language-bash"><code class=" language-bash">sudo fail2ban-client set JAILNAME banip IP</code></pre>