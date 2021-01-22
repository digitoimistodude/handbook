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
Dude käyttää versionhallintaan gitiä, vuodesta 2013 vuoteen 2018 asti Bitbucketia, vuodesta 2019 eteenpäin GitHubia. Kaikki oleellinen koodi tulisi säilyttää git-repositoriossa, mutta arkaluontoiset tiedot kuten tunnukset .env-tiedostossa.

<b>Kaikki minkä voi, tulee julkaista open sourcena</b>, avoimena täysin julkisena <a class="github" href="https://github.com/digitoimistodude">Duden GitHub-tilin alla</a>. Näitä voivat olla omat tekniikat, WordPress-teemat tai -lisäosat, joita voisi kuvitella muidenkin käyttävän. Asiakasprojektit ja muut ei-julkiset kehityskohteet julkaistaan GitHubissa Private repositoriossa, jotka näkyvät ainoastaan Duden tiimille.
<h2>Gitin käyttö asiakasprojekteissa</h2>
Committeja ei saa jättää jemmaan, vaan ne tulee pushata aina hyvissä ajoin, etenkin silloin kun kun tietää olevansa poissa ruudulta. Omat branchit tulee mergetä pääbranchiin aina kun tarvitsee viedä muutoksia muiden käyttöön ja jos ei niin merge tehdään viimeistään työpäivän päätteeksi. Etenkin projektin aktiivisessa kehitysvaiheessa tämä on tärkeää ja suurempien muutosten jälkeen edellytys. Näin projektin jatkokehittäjä eli työkaveri saa uusimmat muutokset ajoissa, eikä pääse syntymään merge conflicteja, jossa useampi taho on muokannut samaa kohtaa vahingossa.

Muutoksia voi niputtaa samaan committiin, esimerkiksi "Improving readability", jossa voi olla useampi typografiamuutos samassa. Nyrkkisääntönä sopiva toiminto-/ tai tyylittelyvälin etappi. Näissä on suotavaa käyttää omaa maalaisjärkeään.
<h2>Git-pikaohje komentorivillä</h2>
<pre class="language-bash"><code>git status</code></pre>
Näe nykyisen edistymisesi tila, mitä on committaamatta, mitä lisättynä, missä mennään. Tälle komennolle on luotu elämää helpottamaan alias <code>s</code> (tämän sivun alalaidassa).
<pre class="language-bash"><code>git add --all</code></pre>
Lisää kaikki tiedostot ja alikansioiden tiedostot gittiin. Eli sen jälkeen kun olet tehnyt mitä tahansa muutoksia, kannattaa ajaa tämä. Muutosten suuruus ja laajuus on kiinni sinusta, mutta pidä muutosten vientiväli järkevänä. Esimerkiksi: olet lisännyt värit elementeille tai napeille ja haluat viedä ne muutokset muille devaajille. Tälle komennolle on luotu elämää helpottamaan alias <code>a</code> (tämän sivun alalaidassa).
<pre class="language-bash"><code>git commit -m 'Some really fancy and descriptive commit message'</code></pre>
Commit-viestien tulee olla selkeitä ja kuvaavia, jotka kertovat mitä muutoksia commitin mukana tulee. Massiivisia committeja (esim. yksi commit joka sisältää puolen päivän työt yhdessä commitissa) tulisi välttää ja pyrkiä committaamaan sen sijaan jokainen toiminto erikseen. Pienetkin tyylimuutokset pitää pyrkiä committaamaan (esim. nappien tyylit tai fonttien säädöt) ja pushaamaan mahdollisimman aikaisessa vaiheessa, jotta vältytään konflikteilta. <b>Ei hillota committeja!</b> Tämä tarkoittaa sitä että tehdään esimerkiksi 3-6 committia ja pushataan ne sitten GitHubiin. Keskeneräisyydellä ei ole väliä, ellei muutos ole menossa suoraan tuotantoon.
<pre class="language-bash"><code>git push -u origin HEAD</code></pre>
Pushaa eli "työnnä" muutokset muiden nähtäville ja työstettäville. Push-viestit menevät myös Slackiin, jotta koko työyhteisö näkee edistymisen. Dude <b>ei käytä</b> push-to-deploy tapaa, joten ei ole vaaraa siitä että muutokset menisivät minnekään tuotantoympäristöön näkyville. Muistathan kuitenkin tarkistaa mitä pushaat. Tälle komennolle on luotu elämää helpottamaan alias <code>p</code> (tämän sivun alalaidassa).
<h2 id="branchit">Branchit</h2>
Jokaisella dudella on oma branchinsa eli "kehitysoksansa" kun työskennellään samassa projektissa. Omassa työstövaiheessa luodaan branch muotoa <code>wip-omanimi</code>, esimerkiksi Ronin työstö tapahtuu koko ajan branchissa <code>wip-roni</code> (<i>wip</i> as in Work in Progress). Jos vain ja ainoastaan yksi kehittäjä kehittää projektia koko projektin ajan tai tekee yksittäisen muutoksen esimerkiksi julkaisun jälkeen, voi tarvittaessa muutokset tehdä suoraan <code>master</code>-branchiin.

Isompia ominaisuuksia tai leiskoja rakentaessa luodaan oma branch, muotoon <code>feature-featurennimi</code> tai <code>layout-viewinnimi</code>. Ominaisuuden branch voi olla esimerkiksi <code>feature-events-2018</code> tai <code>feature-shop-integrations</code> kun taas uuden layoutin branch voi olla <code>layout-new-staffmembers</code>.
<h2 id="branchin-luominen">Branchin luominen projektin alussa</h2>
Branchin luominen gitissä on yksinkertaista. Seuraavalla komennolla näet mitä brancheja on tällä hetkellä saatavilla ja missä olet:
<pre class="language-bash"><code>git branch</code></pre>
Seuraavalla komennolla luot oman branchisi:
<pre class="language-bash"><code>git branch branchisinimi</code></pre>
Seuraavalla komennolla siirryt omaan branchiisi:
<pre class="language-bash"><code>git checkout branchisinimi</code></pre>
Muista että voit tarkistaa missä olet komennolla <code>git status</code> (tai aliaksella <code>s</code>).
<h2>Branchien mergeäminen eli yhdistäminen</h2>
Brancheja pitäisi kehityksen aikana mergetä mahdollisimman tiuhaan masteriin, mutta mielellään aina silloin kun ei ole isompia kesken.

Muista kommunikaatio, varmista että työkaveri on mergennyt oman branchinsa masteriin. Sitten, hae masterista uusin versio menemällä master branchiin:
<pre class="language-bash"><code>git checkout master</code></pre>
Tämän jälkeen hae masterista uusin versio:
<pre class="language-bash"><code>git pull</code></pre>
Sitten mergeä master omaan branchiisi:
<pre class="language-bash"><code>git merge branchisinimi</code></pre>
Tämän jälkeen voit siirtyä omaan branchiisi takaisin:
<pre class="language-bash"><code>git checkout branchisinimi</code></pre>

Mergeä vielä mahdollisesti muuttunut master omaan branchiisi:

<pre class="language-bash"><code>git merge master</code></pre>

<h2>Merge conflict</h2>
Tuliko merge conflicti? Yleensä merge conflict on helppo selvittää. Merge conflictin tullessa tärkeintä on selvittää mitä tiedostoja on muokattu ja mikä muokkaus on uusin. Muuttuneet tiedostot saat näkyviin tuttuun tapaan <code>git status</code> (tai aliaksella <code>s</code>).

Jos merge conflictissa on <i>global.min.css</i>, voit vain kääntää tyylit uudestaan komennolla <code>gulp styles</code>. Jos merge conflictissa on mukana <i>all.js</i> tai <i>dist/front-end.js</i>, compilaa js komennolla <code>gulp js</code> niin se ratkaisee tämän tiedoston conflictin. Jos mukana on muita konfliktaavia tiedostoja, avaa tiedosto Visual Studio Codeen. VSCode osaa ehdottaa merge konfliktiin ratkaisuja automaattisesti. Yhdistä koodi tai hyväksy joko nykyinen tai kommitissa tuleva muutos. Tämän voi tehdä myös manuaalisesti esim. nanolla etsimällä tiedostosta "&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt; branchinnimi", joka osoittaa mihi muutos päättyy ja mihin se loppuu ja poista "&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;" -kommentit. Korjausten jälkeen lisää muutokset (<code>git add --all</code> tai <code>a</code>), committaa ne (<code>git commit 'Fix merge conflicts'</code> tai <code>c 'Fix merge conflicts'</code>) ja pushaa ne (<code>git push</code> tai <code>p</code>). Tämän jälkeen kaikki on kunnossa ja merge on tehty onnistuneesti. Voit vielä tarkistaa mergeämällä uudestaan niin voit varmistua siitä että kaikki on mergetty eikä uusia muutoksia tule.
<h2>Aliaksia</h2>
Tuntuuko työläältä kirjoittaa aina kaikki komennot käsin? komennot on päätetty tehdä kirjoittamalla eikä esim jotain appia käyttämällä, koska silloin pysyy parhaiten kärryillä muutoksista kun ne "hyväksyy" itse. Elämää kuitenkin helpottaa huomattavasti seuraavat aliakset. Muokkaa tietokoneesi ~/.bashrc -tiedostoa esim. komennolla <code>nano ~/.bashrc</code> tai avaamalla tiedoston editoriisi (huom. tiedosto voi olla piilotettuna):
<pre class="language-bash"><code>alias s='git status'
alias a='git add --all'
alias c='git commit -m'
alias p='git push -u origin HEAD'</code></pre>
Tämän jälkeen voit katsoa tilanteen kirjoittamalla <code>s</code>, lisätä kaikki muutokset kirjoittamalla <code>a</code>, committaa muutokset kirjoittamalla <code>c</code> ja pushata muutokset kirjoittamalla <code>p</code>.