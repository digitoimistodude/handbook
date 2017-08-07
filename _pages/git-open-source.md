---
ID: 88
post_title: 'Git &#038; open source'
author: Roni
post_excerpt: ""
layout: page
permalink: >
  https://handbook.dude.fi/wordpress-kehitys/git-open-source
published: true
post_date: 2017-08-04 15:01:06
---
Dude käyttää versionhallintaan gitiä, asiakasprojekteihin BitBucketia, julkisiin projekteihin GitHubia. Kaikki oleellinen koodi tulisi säilyttää git-repositoriossa, mutta arkaluontoiset tiedot kuten tunnukset .env-tiedostossa.

<h3>Commit-viestit muutoksista</h3>

Commit-viestien tulee olla selkeitä ja kuvaavia. Massiivisia committeja tulisi välttää ja pyrkiä committaamaan sen sijaan jokainen toiminto erikseen. Pienetkin muutokset voi committaa vapaasti.

Muutoksia voi niputtaa samaan committiin, esimerkiksi "Improving readability", jossa voi olla useampi typografiamuutos samassa. Nyrkkisääntönä sopiva toimintovälin etappi, jossa saa käyttää maalaisjärkeä.

<b>Kaikki minkä voi, tulee julkaista open sourcena</b>, avoimena täysin julkisena <a class="github" href="https://github.com/digitoimistodude">Duden GitHub-tilin alla</a>. Näitä voivat olla omat tekniikat, WordPress-teemat tai -lisäosat, joita voisi kuvitella muidenkin käyttävän. Asiakkaisiin suoraan liittyviä asioita ei tule missään nimessä laittaa GitHubiin.