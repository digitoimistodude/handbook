---
ID: 85
post_title: Projektin aloitus
author: Roni
post_excerpt: ""
layout: page
permalink: >
  http://handbook.dude.fi/wordpress-kehitys/projektin-aloitus
published: true
post_date: 2017-08-04 14:58:17
---
Dude-ympäristön pystytysohjeet uudelle tietokoneelle löytyy GitHubista, <a href="https://github.com/digitoimistodude/dudestack-instructions" class="github">dudestack/instructions</a>.

<h3>Ensimmäisen aloittajan tehtävät</h3>

Ensimmäinen projektin parissa aloittava dude aloittaa projektin ajamalla aloituskomennon:

<pre class="language-bash"><code>createproject</code></pre>

Scripti kysyy oleelliset tiedot projektista, kuten projektin nimen. Sen jälkeen automaatio luo projektin raamit (<a class="github" href="https://github.com/digitoimistodude/dudestack">digitoimistodude/dudestack</a>), luo paikalliselle kehityskonelle (<a class="github" href="https://github.com/digitoimistodude/marlin-vagrant">digitoimistodude/marlin-vagrant</a>) virtualhostin sekä WordPress-stackin asiakkaan projektia varten. Seuraavaksi ajetaan newtheme.sh (<a class="github" href="https://github.com/digitoimistodude/air">digitoimistodude/air</a>), joka luo projektiin aloitusteeman.

Ensimmäinen aloittaja luo seuraavaksi tietokannan kehityspalvelimelle (gunship), jakaa .env- määritykset sekä <a href="https://www.resilio.com/individuals/">Resilio Sync</a> -linkin mediatiedostoihin Trellon/Slackin kautta muille projektissa mukana oleville devaajille.

BitBucket-repositoryyn lisätään logo ja Slackin #dev-kanavalle projektin integraatio + logo osoitteessa <a href="https://dudet.slack.com/apps/manage">dudet.slack.com/apps/manage</a>.

<h3>Myöhemmin projektiin mukana tulevan devaajan tehtävät</h3>

Muut mukaan tulevat devaajat hakevat Duden kloonaavat projektin koneensa kotihakemiston alla olevaan Projects -hakemistoon projektin BitBucketista, ajavat <pre class="language-bash"><code>composer update && npm install</code></pre> projektin juuressa, asettavat manuaalisesti /etc/hosts -tiedoston kuntoon sekä Vagrantin vhostin paikalleen. Mediatiedostolinkki sekä .env-kredentiaalit poimitaan Trellosta ja projektin kollaboraatio saa alkaa.

Jos jälkikäteen lähdetään työstämään back-endiä, luodaan branch back-end. Jos taas front- endiä, luodaan branch front-end. Masteriin mergetään kohtuullisin väliajoin tai merkkipaalujen aikaan.