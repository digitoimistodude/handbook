---
ID: 438
post_title: Saavutettavuus
author: Roni
post_excerpt: ""
layout: page
permalink: >
  https://handbook.dude.fi/wordpress-kehitys/saavutettavuus
published: true
post_date: 2019-08-07 15:48:57
---
Saavutettavuus (esteettömyys Internetissä) on Dudelle erittäin tärkeää. Sivujen täytyy toimia näppäimistöllä ja sokeain lukulaitteilla. Asiakasprojekteissa pyritään vähintään WCAG 2.0 A-tason saavutettavuuteen. Jos projekti sen sallii, keskitytään myös tarkemmin laajemman saavutettavuuden ja inklusiivisuuden parantamiseen, esimerkiksi kontrastiasioihin WCAG 2.0 AA:n ja AAA:n puitteissa.

Saavutettavuustestaukseen käytetään seuraavia työkaluja:

<ul>
<li><a href="https://chrome.google.com/webstore/detail/axe/lhdoppojpmngadmnindnejefpokejbdd">axe for Google Chrome</a></li>
<li><a href="https://github.com/pa11y/pa11y">pa11y</a></li>
<li>Maalaisjärki</li>
</ul>

<h3>Komennot</h3>

Seuraava komento edellyttää että pa11y on <b>package.json</b>-tiedostossa, npm-paketti ja Yoast SEO tai SEO Framework asennettuna.

<pre class="language-css"><code>pa11y-ci --sitemap https://sivustonnimi.test/sitemap.xml</code></pre>

<h3>Aiheesta muualla</h3>

<ul>
<li><a href="https://www.dude.fi/avainsana/saavutettavuus">Blogikirjoitukset avainsanalla saavutettavuus</a></li>
<li<a href="">Ronin WordCamp Jyväskylä 9.2.2018 esitys aiheesta "Esteettömyys osaksi WordPress-teemakehitystä"</a></li>
</ul>