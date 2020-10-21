---
ID: 630
post_title: Sisäinen tekninen kehitys
author: Roni
post_excerpt: ""
layout: page
permalink: >
  http://handbook.dude.fi/sisainen-tekninen-kehitys
published: true
post_date: 2020-10-21 11:03:45
---
<!-- wp:paragraph -->
<p>Dudelle on tärkeää kehittää omia työkaluja ja toimintamalleja tehokkaammaksi jo päivä- tai viikkotasolla. Tämä sivu koskee sisäistä tekniikkaa ja toimintatapaa.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Keskisimpiä sisäisiä projekteja ja työkaluja voivat olla esimerkiksi:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><a class="github" href="https://github.com/digitoimistodude/dudestack">dudestack</a></li><li><a class="github" href="https://github.com/digitoimistodude/macos-lemp-setup">macos-lemp-setup</a></li><li><a href="https://github.com/digitoimistodude/devpackages">devpackages</a></li><li><a class="github" href="https://github.com/digitoimistodude/air-light">air-light</a></li><li><a class="github" href="https://github.com/digitoimistodude/air-helper">air-helper</a></li><li><a class="github" href="https://github.com/digitoimistodude/dude">dude</a></li><li><a class="github" href="https://github.com/ronilaukkarinen/vscode-settings">vscode-settings</a></li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>Kehityksen toimintamalli</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Pohjateemaa (<a class="github" href="https://github.com/digitoimistodude/air-light">air-light</a>) ja tukilisäosaa (<a class="github" href="https://github.com/digitoimistodude/air-helper">air-helper</a>) on tarkoitus päivittää aina kun vastaan tulee perusteltavissa oleva asia, jota esimerkiksi käyttää jokaisessa projektissa. Kehityksen toimintamalli on hyvinkin nopeatempoinen ja joustava, jossa erityisesti <a href="https://github.com/digitoimistodude/air-light">pohjateemaan</a> muutoksia lisätään sitä mukaa kun niitä tulee vastaan. Tarvittaessa muutoksia käydään läpi ja iteroidaan devitsekissä.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Lähtökohtaisesti sisäisessä kehityksessä noudatetaan <a href="https://handbook.dude.fi/wordpress-kehitys/git-open-source">Duden tuttuja git-käytänteitä</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Nyrkkisääntö muutoksiin: On parempi että <em>jatkuvaa</em> kehitystä syntyy kuin että se jää paikoilleen odottamaan "sopivaa hetkeä".</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Releaset</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><strong>Pienet ei-breaking change muutokset:</strong> Relesointia voi tehdä GitHub-versioon, jos sille on hyvät perusteet. Muissa tapauksissa, kuten isommissa pompseissa muutoksia tai perusteellisempaa tutkailua vaativissa asioissa on syytä tehdä Pull Request tai oma branch.</p>
<!-- /wp:paragraph -->