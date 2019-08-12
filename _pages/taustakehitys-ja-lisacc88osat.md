---
ID: 95
post_title: Taustakehitys ja lisäosat
author: Roni
post_excerpt: ""
layout: page
permalink: 'http://handbook.dude.fi/wordpress-kehitys/taustakehitys-ja-lisa%cc%88osat'
published: true
post_date: 2017-08-04 15:08:01
---
Taustakehittäjä eli Back End Developer kehittää WordPress-sivuston taustalogiikoita, lisäosia ja toiminnallisuuksia enimmäkseen PHP:lla, WP REST API:lla ja JavaScriptilla (tarpeen mukaan frameworkeilla tai jatkeilla, kuten Vue, React tai Angular).

<h3>Riippuvuudet</h3>

PHP:n dependenssimanagerina toimii Composer. Lisäosien dependenssit on lisättävä composer.json-tiedostoon asianmukaisesti ja lisäosasta tehtävä joko vcs-composer-repository (GitHub) tai suoraan Packagistiin. Mielellään jälkimmäinen, koska silloin jatkokehittäjän tarvitsee lisätä ainoastaan yksi require composer.json-tiedostoon tai ajaa require-komento.

<h3>Composer, packagist ja päivitykset</h3>

Lisäosien päivitykset tulee toteuttaa siten, että uuden projektin aloittaessa saa aina uusimman version requireen. Esimerkiksi jos julkaisee version 1.0.5, tulee versiot korvata uusilla package.json, composer.json sekä pää-php-tiedostoon. Tämän lisäksi tulee ajaa <b>komentoriviltä</b> rimpsu:

<pre class="language-bash"><code>git tag -a '1.0.5' && git push --tags</code></pre>

Packagist ei osaa nimittäin hakea payloadia, jos tagin/releasen tekee GitHubin webkäyttöliittymästä. Updateria varten tämän jälkeen draftataan uusi release.

<h3>Lisäosat</h3>

Lisäosat sivustoille valitaan aina asiakkaan tarpeiden mukaan. Ennen aloitusta Dude käyttää projekteissa seuraavia vakiolisäosia. Nämä löytyy <a href="https://github.com/digitoimistodude/dudestack/blob/master/composer.json" class="github">digitoimistodude/dudestack</a> composer.json-tiedostosta ja kaikki muutokset on tehtävä kyseiseen tiedostoon.

<h4>Google Analytics Dashboard for WP (GADWP)</h4>

Helppokäyttöinen, hyvin rakennettu lisäosa Google Analyticsia varten.

<h4>Imagify</h4>

Pakkaa kuvat lennosta pienempään kokoon ilman laadun huononemista.

<h4>Simple history</h4>

Lisäosa, joka näyttää reaaliajassa sen mitä WordPress-sivustolla tapahtuu. Kätevä esimerkiksi käyttäjien toimien seuraamiseen ja muutoksien havaitsemiseen.

<h4>SendGrid</h4>

Sähköpostinvälittäjälisäosa. Varmistaa, että viestit menevät aina perille WordPress-saitilta. Kätevä myös viestimäärien seurantaan ja analysointiin saittikohtaisesti.

<h4>WP Sanitize Accented Uploads</h4>

Poistaa lisätessä ylimääräiset merkit ja ääkköset tiedostonimistä sekä pienentää isot kirjaimet. Näin mediakirjastoon ladatut tiedostot on helpompi linkata.

<h4>Air helper</h4>

Duden pohjateeman Airin apulisäosa, joka laajentaa teemaa toivottuun tapaan. Tällä hetkellä sisältää toimintoja kuten päivitysilmoitusten piilotuksen, custom-mediakansion (wp-uploadsin sijaan media/), SendGrid-kredentiaalit .env-tiedostosta jne. Air-helperiin voi tutustua tarkemmin täällä: https://github.com/digitoimistodude/air-helper

<h4>WP Rocket</h4>

Välimuistitukseen käytetään oletuksena WP Rocketia.

<h4>Cerber Security</h4>

Tietoturvaa vahvistamaan, logineiden rajoittamiseen.

<h3>Projekteihin valittavat lisäosat</h3>

Projekteihin valitaan hyvin toteutetut, sellaiset lisäosat, joita asiakkaan on mieluista käyttää. Lisäosien laadukas tekninen toteutus on tärkeää, mutta hyvin koodattu lisäosa ei saa koskaan mennä käytettävyyden edelle. WPML lisäosaa ei tule kuitenkaan käyttää <u>missään tapauksessa</u> koskaan.

<h4>Polylang</h4>

Jos on tulossa kielikäännöksiä, sivustolle asennetaan vakiona Polylang. Muita kielikäännösplugareita ei ole sallittua käyttää.

<h4>WooCommerce</h4>

Jos verkkokauppa.

<h4>Carbon Fields</h4>

Yksinkertaisempiin sekä suoraviivaisiin projekteihin suositellaan käytettäväksi Carbon Fieldsiä. Paljon käyttöä vaativissa sivuissa suositellaan kuitenkin ACF:ää, sillä Carbon Fieldsissä ei tällä hetkellä toimi esikatselu. Seurataan CF:n kehitystä tiiviisti.

<h4><span class="accent">tai</span> Advanced Custom Fields Pro</h4>

Jos sivustolle kaivataan modulaarista rakennetta, käytetään ACF Pro:ta custom  eldsien ja sivupohjien rakentamiseen. ACF Pro päivittyy tiuhaan ja on tällä hetkellä kaikista suosituin custom  eldseihin käytetty ratkaisu.

<h4>SEO Framework</h4>

Sivustolle asennetaan vakiona SEO Framework, joka on kevyt SEO-lisäosa WordPressille.

<h4><span class="accent">tai</span> Yoast SEO</h4>

Erityisiä SEO-tarpeita omaaville asiakkaille laitetaan Yoast SEO, mm. snippet-previewin, focus keywordsin, sitemappien ja Social -toimintojen vuoksi. Rinnalle asennetaan SO Hide Seo Bloat, joka piilottaa vakiona kaiken turhan sekä asiakasta häiritsevät ilmoitukset. Lisäosasta laitetaan julkaistaessa Advanced-toiminnot päälle.

<h4>WP Libre Form</h4>

Jos tulee lomakkeita, sivustolle asennetaan vakiona WP Libre Form.

<h4><span class="accent">tai</span> Gravity Forms</h4>

Jos lomakkeita halutaan muokkailla vapaammin, niille tarvitsee tehdä jotain Gravity Formsin mahdollistavaa customia, käytetään Gravity Formsia.

<h3>Muut lisäosat</h3>

Loput lisäosista ovat projektikohtaisia.

<h3>Aiheeseen liittyviä bloggauksia</h3>

<ul>
<li><a href="https://www.dude.fi/mita-lisaosia-dude-kayttaa">4.8.2017: Mitä lisäosia Dude käyttää?</a></li>
<li><a href="https://www.dude.fi/sivuston-tekemisen-nakymaton-osuus-tietorakenteen-suunnittelu">25.9.2017: Sivuston tekemisen näkymätön osuus – tietorakenteen suunnittelu</a></li>
</ul>