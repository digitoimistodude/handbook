---
ID: 429
post_title: Stagingiin vieminen
author: Roni
post_excerpt: ""
layout: page
permalink: >
  http://handbook.dude.fi/wordpress-kehitys/stagingiin-vieminen
published: true
post_date: 2019-08-07 15:02:50
---
Kun sivuston saatu siihen pisteeseen, että sitä voi selata, se laitetaan testiin ja näytille testipalvelimelle, jota myös näyttöpalvelimeksi (engl. <i>staging server</i>) kutsutaan. Duden staging-sivustot sijaitsevat aina omassa domainissaan, joka on muotoa <a href="https://asiakas.vaiheessa.fi">asiakas.vaiheessa.fi</a>. Tietokantapalvelin staging-sivustoille on nimeltään gunship ja sijaitsee osoitteessa gunship.dude.fi.

<h3>Ennakkoasetukset (tehdään vain kerran, jos ei ole aiemmin tehty)</h3>

Varmista että sinulla on oikea versio Capistranosta kirjoittamalla projektin juuressa:

<pre class="language-bash"><code>bundle install</code></pre>

Jos saat <i>Permission denied (publickey)</i> -ilmoituksen, varmista että sinulla on oikeudet käyttää palvelimella GitHubia kirjautumalla sisään ssh:lla: tunnus@gunship.dude.fi ja luomalla avainpari komennolla:

<pre class="language-bash"><code>ssh-keygen -t rsa</code></pre>

Tämän jälkeen avainpari haetaan komennolla:

<pre class="language-bash"><code>cat ~/.ssh/id_rsa.pub</code></pre>

Sitten GitHubiin, klikkaa avataria ja <b>Settings > SSH and GPG keys > Title:</b> <i>gunship.dude.fi</i>, <b>Key</b>, copy paste komentoriviltä.

<h3>Tietokannan luominen</h3>

Kanta täytyy olla Gunshipillä. Kannan luominen: Mene Sequel Pro:hon, avaa localhost, exporttaa lokaali kanta, <b>File > Export</b>. Avaa yhteys Gunshipin tietokantapalvelimeen, <b>Choose Database > Add database > projektinnimi, File > Import</b>, <i>kannan sql-tiedosto</i>.

Tietokantatunnareiden luominen: Kirjaudu ssh:lla:

<pre class="language-bash"><code>ssh tunnus@gunship.dude.fi</code></pre>

Sitten kirjoita:

<pre class="language-bash"><code>mysql -u root -p</code></pre>

Katso 1Passwordin gunshipistä MySQL root pass. Luo kanta seuraavasti:

<pre class="language-bash"><code>CREATE USER 'projektinnimi'@'%' IDENTIFIED BY '1passwordissa generoitu salasana';</code></pre>

Anna oikeudet komennolla:

<pre class="language-bash"><code>GRANT ALL PRIVILEGES ON projektinnimi.* TO 'projektinnimi'@'%';</code></pre>

Ota oikeudet käyttöön:

<pre class="language-bash"><code>FLUSH PRIVILEGES;</code></pre>

Huom: Jatkoa ajatellen paina ylöspäin niin saat aiemmat komennot ja voit kopata niistä mallia. Älä sulje MySQL-komentoriviä vaan kopioi salasana ja lisää se projektin juureen, .env-tiedoston <b>DB_PASSWORD</b> -kohtaan.

<h3>Tiedostojen vieminen staging-palvelimelle</h3>

<ol>
<li>Mene komentorivillä projektiin, cd ~/Projects/projektinnimi ja varmista että kaikki muutokset ovat masterissa, siirry master branchiin git checkout master ja mergeä tarvittaessa.</li>
<li>Kirjoita <code>cap install</code></li>
<li>Avaa config/deploy/staging.rb, sublilla tai nanolla. Korvaa tiedoston sisältö uusimmalla staging.rb deploy-configilla.</li>
<li>Korvaa <b>{{{USERNAME}}}</b> omalla käyttäjätunnuksella ja <b>{{{PASSWORD}}}</b> omalla salasanalla, tarkista 1Passwordista kohdasta gunship.dude.fi. Korvaa <b>{{{PROJECTNAME}}}</b> projektin nimellä, (alt + cmd + F). Tarkista että wp-cli komentojen urlit ovat oikein, pitäisi olla <i>http://projektinnimi.test</i> ja <i>https://projektinnimi.vaiheessa.fi</i>. Tallenna tiedosto.</li>
<li>Tarkista että <i>config/deploy.rb</i> näyttää oikealta.</li>
<li>Mene komentoriville projektikansioon ja aja <code>cap staging deploy</code></li>
<li>Saat viestin: <b>ERROR linked file /var/www/projektinnimi/shared/.env does not exist</b>, kuuluu asiaan. Kirjaudu palvelimelle tunnuksillasi ssh tunnus@gunship.dude.fi, kopioi polku virheilmoituksesta ja aja komento seuraavasti: <code>nano /var/www/projektinnimi/shared/.env</code> (kopioi polku virheilmoituksesta)</li>
<li>Avaa projektin paikallinen .env ja muokkaa tiedostosta seuraavat kohdat kuntoon:

<pre class="language-bash"><code>DB_NAME=projektinnimi
DB_USER=projektinnimi
DB_PASSWORD=gunship-kannan salasana tähän
DB_HOST=185.87.110.10

WP_ENV=staging
WP_HOME=https://projektinnimi.vaiheessa.fi
WP_SITEURL=https://projektinnimi.vaiheessa.fi/wp
</code></pre>

Saltit ja muut mahdolliset ympäristömuuttujat samat kuin lokaalissa.</li>
<li>Poistu palvelimelta komennolla exit. Aja uudestaan komento <code>cap staging deploy</code>.</li>
<li>Mene FileZillaan. Siirrä mediatiedostot kansioon <i>/var/www/projektinnimi/shared/media</i></li>
<li>Määrittele kertakäyttösalasana muokkaamalla tiedostoa <i>/var/www/projektinnimi/shared/.staging_password</i>. Lisää salasana Trelloon ja 1Passwordiin.</li>
</ol>

Lopuksi testaa sivustoa projektin virallisessa osoitteessa projektinnimi.vaiheessa.fi.
