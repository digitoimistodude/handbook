---
ID: 88
post_title: 'Git &#038; open source'
author: Roni
post_excerpt: ""
layout: page
permalink: >
  http://handbook.dude.fi/wordpress-kehitys/git-open-source
published: true
post_date: 2017-08-04 15:01:06
---
Dude käyttää versionhallintaan gitiä, asiakasprojekteihin BitBucketia, julkisiin projekteihin GitHubia. Kaikki oleellinen koodi tulisi säilyttää git-repositoriossa, mutta arkaluontoiset tiedot kuten tunnukset .env-tiedostossa.

<b>Kaikki minkä voi, tulee julkaista open sourcena</b>, avoimena täysin julkisena <a class="github" href="https://github.com/digitoimistodude">Duden GitHub-tilin alla</a>. Näitä voivat olla omat tekniikat, WordPress-teemat tai -lisäosat, joita voisi kuvitella muidenkin käyttävän. Asiakkaisiin suoraan liittyviä asioita ei tule missään nimessä laittaa GitHubiin.
<h3>Commit-viestit muutoksista</h3>
Commit-viestien tulee olla selkeitä ja kuvaavia. Massiivisia committeja tulisi välttää ja pyrkiä committaamaan sen sijaan jokainen toiminto erikseen. Pienetkin muutokset pitää committaa mahdollisimman aikaisessa vaiheessa, jotta vältytään konflikteilta. Edes keskeneräisyydellä ei ole väliä, ellei muutos ole menossa suoraan tuotantoon.

<h3>Gitin käyttö asiakasprojekteissa</h3>

Committeja ei saa jättää jemmaan, vaan ne tulee pushata aina hyvissä ajoin, etenkin silloin kun kun tietää olevansa poissa ruudulta. Front-end ja back-end branchit tulee myös mergetä pääbranchiin työpäivän päätteeksi, etenkin projektin aktiivisessa kehitysvaiheessa ja suurempien muutosten jälkeen. Näin projektin jatkokehittäjä eli työkaveri saa uusimmat muutokset ajoissa, eikä tule konflikteja.

Muutoksia voi niputtaa samaan committiin, esimerkiksi "Improving readability", jossa voi olla useampi typografiamuutos samassa. Nyrkkisääntönä sopiva toimintovälin etappi, jossa saa käyttää maalaisjärkeä.

<h3>Git-pikaohje komentorivillä</h3>

<pre class="language-bash"><code>git status</code></pre>

Näe nykyisen edistymisesi tila, mitä on committaamatta, mitä lisättynä, missä mennään.

<pre class="language-bash"><code>git add --all</code></pre>

Lisää kaikki tiedostot ja alikansioiden tiedostot gittiin. Eli sen jälkeen kun olet tehnyt mitä tahansa muutoksia, kannattaa ajaa tämä. Muutosten suuruus ja laajuus on kiinni sinusta, mutta pidä muutosten vientiväli järkevänä. Esimerkiksi: olet lisännyt värit elementeille tai napeille ja haluat viedä ne muutokset muille devaajille.

<pre class="language-bash"><code>git push -u origin HEAD</code></pre>

Pushaa eli "työnnä" muutokset muiden nähtäville ja työstettäville. Push-viestit menevät myös Slackiin, jotta koko työyhteisö näkee edistymisen. Dude <b>ei käytä</b> push-to-deploy tapaa, joten ei ole vaaraa siitä että muutokset menisivät minnekään tuotantoympäristöön näkyville. Muistathan kuitenkin tarkistaa mitä pushaat.

<h3>Aliaksia</h3>

Tuntuuko työläältä kirjoittaa aina kaikki komennot käsin? komennot on päätetty tehdä kirjoittamalla eikä esim jotain appia käyttämällä, koska silloin pysyy parhaiten kärryillä muutoksista kun ne "hyväksyy" itse. Elämää kuitenkin helpottaa huomattavasti seuraavat aliakset. Muokkaa tietokoneesi ~/.bashrc -tiedostoa esim. komennolla <code>nano ~/.bashrc</code> tai avaamalla tiedoston editoriisi (huom. tiedosto voi olla piilotettuna):

<pre class="language-bash"><code>alias s='git status'
alias a='git add --all'
alias c='git commit -m'
alias p='git push -u origin HEAD'</code></pre>

Tämän jälkeen voit katsoa tilanteen kirjoittamalla <code>s</code>, lisätä kaikki muutokset kirjoittamalla <code>a</code>, committaa muutokset kirjoittamalla <code>c</code> ja pushata muutokset kirjoittamalla <code>p</code>.