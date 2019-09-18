---
ID: 98
post_title: Päivitykset ja ylläpito
author: Roni
post_excerpt: ""
layout: page
permalink: >
  http://handbook.dude.fi/wordpress-kehitys/paivitykset-ja-yllapito
published: true
post_date: 2017-08-04 15:10:51
---
Dudelle on tärkeää, ettei pienikään sivusto jää mätänemään. Päivitykset suoritetaan jokaisen viikon maanantai ja torstai (<a href="https://managewp.com/">ManageWP</a>). Ennen päivityksen suorittamista on katsottava Changelogista mitä päivitys pitää sisällään. Jos kyseessä on korjauspäivitys, voi päivityksen suorittaa ilman ennakkotarkistuksia.

Isompia päivityksiä varten otetaan aina tietokannasta varmuuskopio ennen päivittämistä. Automaattiset varmuuskopiot lähtevät kolmelle verkkolevylle joka yö, mutta silti otetaan paikallinen kopio omalle koneelle. Tarvittaessa tehdään rollback-toimenpiteet.

<h3>Vanhan hostingin siirtäminen Duden ylläpitoon</h3>

Asiakkaalta tarvitaan siirtoa varten .fi -domaineista <i>välittäjänvaihtoavain</i>, ulkomaisista .com-domainista lukituksen poisto sekä <i>EPP Code</i>, eli siirtokoodi.

Uudet kotimaiset domainit varataan <a href="https://registry.domain.fi">Viestintäviraston</a> kautta suoraan, ulkomaiset domainit varataan <a href="https://www.cloudflare.com">Cloudflarelta</a> tai erikoisemmat TLD:t <a href="https://iwantmyname.com/">iwantmyname.comin</a> kautta.

Jos asiakas haluaa pitää nimipalvelun ja/tai domainin itsellään, on asiakkaalle ilmoitettava IP-osoite A-recordien (@ ja www) päivittämistä varten. Vanhan sivuston varmuuskopionti voidaan myös tehdä, silloin asiakas toimittaa SFTP + MySQL -tunnukset vanhaan hostingpalveluunsa.

Sähköpostit voidaan myös siirtää Dudelle (G Suite) tarvittaessa siirtotyömaksua vastaan.