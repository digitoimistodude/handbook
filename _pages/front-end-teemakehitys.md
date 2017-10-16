---
ID: 92
post_title: 'Front End &#038; teemakehitys'
author: Roni
post_excerpt: ""
layout: page
permalink: >
  https://handbook.dude.fi/wordpress-kehitys/front-end-teemakehitys
published: true
post_date: 2017-08-04 15:02:36
---
Front End devaaja keskittyy erityisesti teemakehityksen visuaalisen puoleen. CSS- preprosessorikielenä dude käyttää SASS-kielen SCSS-syntaksia. SCSS-kehitykessä tulee käyttää scss-lintiä laadukkaan koodin tarkistamista ja varmistamista varten sekä stylefmt:tä tarvittaessa automaattiseen koodin paranteluun.

Front End -kehittäjä voi myös tarvittaessa ehdottaa/committaa muutoksia tai korjauksia back endiin ja erityisesti toteuttaa front end -puolta helpottavia muutoksia vapaasti.

<a href="https://github.com/digitoimistodude/air" class="github">digitoimistodude/air</a> ja <a href="https://github.com/digitoimistodude/devpackages" class="github">digitoimistodude/devpackages</a> tarjoavat WordPress-teemakehitykseen edellyttävät paketit ja työkalut, kuten gulp, npm ja browsersync. <a href="https://github.com/digitoimistodude/dudestack" class="github">digitoimistodude/dudestack</a>in createproject-skripti sekä <a href="https://github.com/digitoimistodude/air" class="github">digitoimistodude/air</a>in newtheme.sh sisältävät näiden oikeaoppisen, automatisoidun asennuksen.

<h3>Modulaarinen rakenne</h3>

SCSS-tyylit on toteutettava modulaarisesti, eli jokainen oleellinen layout tai view on tallennettava omaksi tiedostokseen. Esimerkkinä toimii airin tiedostorakenne, joka näyttää tältä:

<b>sass/</b>
- base
--- _accessibility.scss 
--– _config.scss
--- _helpers.scss
--- _global.scss
- layout
--- _forms.scss
--- _general.scss
--- _sidebar.scss
... ja niin edelleen.

Rakenteeseen voi ehdottaa muutoksia suoraan Airin GitHub- repositorioon sass/ -hakemistoon. Lähtökohta on, että esim. template-partsissa sijaitsevilla php-tiedostoilla olisi aina views/ -kansiossa saman niminen SCSS-pari.

Front End devaaja aloittaessaan rakentaa WordPressin teematiedostoihin HTML-rakenteen back end -kehittäjälle valmiiksi. Järkeviä PHP-ratkaisuja voi rakentaa valmiiksi, kuten tietyt echot, svg includet, oleelliset functions.php:n muutokset tai vastaavat, mutta WP Queryt ja laajemmat PHP-toiminnallisuudet jätetään back end -kehittäjän työstettäväksi.

Front End käyttää aina branchia front-end ja mergeää säännöllisesti masteriin. Muista brancheista keskustellaan erikseen.

<h3>Riippuvuudet</h3>

Projektissa käytettävät SCSS- ja JS-palikat haetaan npm upstreamista ja lisätään vaatimuksina teeman package.jsoniin aina kun mahdollista. Jos kyseessä on esimerkiksi muutaman rivin <code>@mixin</code>, voidaan tehdä poikkeus ja tarvittavan dependenssin toistuessa keskustella siitä, lisättäisiinkö tämä myös airiin defaultiksi.

Front endissä tarvittavat lisäosat tai muut PHP:ta käyttävät riippuvuudet on lisättävä <b>composer.json</b>-tiedostoon tarvittaessa.

<h3>Tuetut selaimet</h3>

Front End koodin on toimittava julkaisuhetkellä vallitsevissa selaimissa, kuten Mozilla Firefoxin, Google Chromen, Safarin ja Internet Explorerin uusimmissa versioissa. Tämän lisäksi <a href="https://github.com/digitoimistodude/air/blob/master/gulpfile.js#L106" class="github">air-teeman gulpfile.js:ssä</a> määritetty autoprefixer varmistaa, että prefixit on kunnossa kolmeen vanhempaan versioon.

Internet Explorerissa tuetaan versioita 11 ja ylöspäin. Versiota 11 vanhemmille tuki rakennetaan lisätyönä.