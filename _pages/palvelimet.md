---
ID: 108
post_title: Palvelimet
author: Roni
post_excerpt: ""
layout: page
permalink: http://handbook.dude.fi/palvelimet
published: true
post_date: 2017-08-04 15:16:10
---
<h3>Sijainti</h3>
Duden <b>WordPress-optimoidut</b> dedikoidut rautapalvelimet sijaitsevat fyysisesti <a href="https://www.multim.fi/">Multim Oy:n</a> datacenterissä Ulvilassa, Ficolo Oy:n Suomen armeijan vanhaan peruskallioluolastoon rakennetussa korkean turvaluokituksen konesalissa.

Duden palvelimet ovat fyysisesti Multimin hoidossa, mutta palvelintekniikan ylläpito kuuluu Duden tekniselle tiimille.
<h3>Verkkokartta</h3>
Duden verkon takaa neljä isointa Internet-palveluntarjoajaa. Jos yksi verkko kaatuu, ei koko infrastruktuuri jää tavoittamattomiin vaan voidaan hyödyntää toisen palveluntarjoajan verkkoa. Private vlan on Duden hopealuoti niin tietoturvan kuin korkean tason saatavuudenkin osalta.
<figure class="wp-block-image size-large"><img class="alignnone wp-image-614 size-full" src="http://handbook.dude.fi/media/infra-web.jpg" alt="" width="800" height="684" /></figure>
<h3>Vastuullisuus</h3>
Dude käyttää <a href="https://www.dude.fi/vihreaa-hostingia-100-green-web-hosting">vihreää hostingia</a> palvelimet käyvät 100% ekologisella tuulivoimalla. Tästä osoituksena Dudella on päästövapaan <a href="https://www.thegreenwebfoundation.org/green-web-check/?url=https%3A%2F%2Fwww.dude.fi">Green Web Foundationin</a> virallinen sertifiointi.
<h3>Rauta</h3>
Palvelimet on räätälöity perusteita myöten Multimin kanssa vuonna 2016 Duden tarpeisiin mahdollisimman sopivaksi, WordPress-optimoidusti ja suorituskyky edellä. Kehitys on jatkuvaa.

Rautapalvelimen sisällä on neljän coren ja kahdeksan säikeen Intel(R) Xeon(R) CPU E3-1230 v3 @ 3.30GHz suoritinta ja 32 gigatavua RAM-muistia. Virtuaalipalvelimissamme on SSD-levyjärjestelmä, joka on tavallseen HDD:seen verrattuna huomattavasti nopeampi suorituskyvyltään.
<h3>Palvelintekniikka</h3>
Käyttöjärjestelmänä käytetään Ubuntu 16.04 Xenial Xerus LTS:ää, ellein toisin päätetä. Web-palvelintekniikkana toimii LEMP (Linux, Nginx, MariaDB, php-fpm), lähtökohtaisesti uusimmat versiot Nginxistä, MariaDB:stä sekä PHP7:sta.

Välimuistituksessa on käytössä uusin <a href="https://developers.google.com/speed/pagespeed/module">ngx-pagespeed</a>, joka tekee lukuisia toimenpiteitä suoraan RAM-muistiin, kuten lazylaodaa, pakkaa ja muuntaa sivustojen kuvat uuden sukupolven webp-muotoon fallbackeineen, minifoi HTML:n, CSS:n, JS:n, kuvakkeet ja näin ollen nopeuttaa kaikkia sivustoja. Kannan välimuistituksessa WP:n sisäänrakennettujen transientien ja cache-pluginien lisäksi käytössä on palvelintasolla <a href="https://redis.io/">Redis</a>.
<h3>Päivitykset</h3>
WordPress-päivitykset hoidetaan joka <b>maanantai</b> ja <b>torstai</b> ja <a href="https://wpscan.org/">WPSCAN</a>-tarkistukset ajetaan päivittäin WordPress-lisäosien haavoittuvuuksien varalta.

Palvelinten huoltoikkuna on joka kuukauden toinen tiistai. Lisää tietoa huolloista ja palvelinten tilasta löytyy osoitteesta <a href="https://status.dude.fi">status.dude.fi</a>.
<h3>Varmuuskopiot</h3>
Varmuuskopiot otetaan aina ennen muutoksia dev-staging-production ympäristöjen välillä, yleisesti tuotannon tietokannoista (.sql) tunnin välein, koko sivuston snapshot eli tiedostot ja mediakirjastot (.zip) kerran päivässä. Varmuuskopiontisijainteja ovat ulkoinen verkkolevy, sisäinen verkkolevy sekä ulkoinen pilvipalvelu (<a href="https://managewp.com/">ManageWP</a>).
<h3>Nimipalvelut ja domainit</h3>
Dude on virallinen Traficomin verkkotunnusvälittäjä. Domaineissa Dude luottaa <a href="https://registry.domain.fi/">Suomen viestintävirastoon</a> (.fi-domainit), <a href="https://www.namecheap.com/">Namecheapiin</a> (.com, .net, .info ja muut ulkomaiset päätteet) sekä <a href="https://iwantmyname.com/">iwantmynameen</a> (ulkomaiset ja erikoisemmat päätteet, esim. .business tai .coffee).

Nimipalvimet Dudelle tarjoaa <a href="https://www.cloudflare.com/">Cloudflareen</a>.
<h3>Sähköpostivälitys</h3>
Sähköpostiliikenteessä välittäjänä käytämme <a href="https://sendgrid.com/">SendGridiä</a> ja <a href="https://www.mailgun.com/">Mailgunia</a>.
<h3>Aiheeseen liittyviä bloggauksia</h3>
<ul>
 	<li><a href="https://www.dude.fi/wordpress-optimoitu-palvelin">15.3.2016: Palvelimen merkitys WordPress-sivustoille</a></li>
 	<li><a href="https://www.dude.fi/harharetki-palvelinmaailmassa">10.1.2017: Duden harharetki palvelinmaailmassa</a></li>
</ul>