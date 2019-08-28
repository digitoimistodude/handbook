---
ID: 102
post_title: Julkaisu
author: Roni
post_excerpt: ""
layout: page
permalink: >
  http://handbook.dude.fi/wordpress-kehitys/julkaisu
published: true
post_date: 2017-08-04 15:11:34
---
Dudella ei tehdä julkaisuja lähtökohtaisesti iltapäivisin ja perjantaisin. Jos jokin menee pieleen, on hyvä että toimistolla on vielä työntekijöitä ja kukaan ei joudu korjailemaan asioita liiaksi työaikojen ulkopuolella. Paras julkaisuajankohta on aamusta tai aamupäivästä ma-ke-akselilla.

Huomaathan, että tätä opasta käytetään ainoastaan silloin kun asiakkaan sivut julkaistaan <a href="https://handbook.dude.fi/palvelimet">Duden palvelimella</a>. Muussa tapauksessa toimitaan tilannekohtaisesti.

<h3>Miten deploy toimii</h3>
Deployn automatisointi tapahtuu <a href="http://capistranorb.com/">Capistranon</a> avulla, joka on osa <a class="github" href="https://github.com/digitoimistodude/dudestack">digitoimisto/dudestack</a>-kokonaisuutta. Ensimmäinen deploy suoritetaan aina Capistranon työkalulla, mutta esim. pienet teemapäivitykset hoidetaan suoralla sftp- tai rsync-yhteydellä.

<h3>Julkaisut vanhaan projektiin</h3>

Jatkokehitykset, freesaukset yms. hoidetaan suoralla sftp- tai rsync-yhteydellä jo aiemmin deployattuun projektiin. Isommat releaset tehdään uudella cap production deploylla.

Muutosten myötä tulee muistaa ngx-pagespeed-välimuistin tyhjennys:
<pre class="language-bash"><code>sudo rm -rf /tmp/pgsp/v3/domain.fi</code></pre>

<h3>Uuden julkaisun vaiheet</h3>
Duden julkaisutoimenpiteet eli deploy on monivaiheinen ja varsinaista tiedonsiirtoa ja kansiorakennetta lukuunottamatta (<a href="http://capistranorb.com/">Capistrano</a>) enimmäkseen manuaalinen. Käsipelillä asioiden tekemisellä pyrimme varmistamaan että kaikki on varmistettu ja menee oikein. Kokonaisuudessaan vaiheisiin kuluu testausta lukuunottamatta aikaa noin varttitunti.

26.4.2018 eteenpäin vaiheet 1, 2 on automatisoitu scripteihin (huomaathan käyttää <b>bashia</b> <i>sh</i> sijaan, sillä ubuntun sh ei tue read-komentoa).

<h4>1. Deploy-asetustiedoston luominen paikalliseen ympäristöön</h4>

<a class="github" href="https://github.com/digitoimistodude/dudestack">digitoimisto/dudestack</a>in aloitusscripti (lisää kohdassa <a href="https://handbook.dude.fi/wordpress-kehitys/projektin-aloitus">Projektin aloitus</a>) määrittää oletuskonffit valmiiksi, mutta tuotannon conffiin saattaa joskus tulla muutoksia, joten se tarkistetaan aina erikseen.

Avaa projektikansion sisällä oleva <b>config/deploy/production.rb</b>. Jos tiedostoa, ei ole, luo oletustiedostot menemällä Terminalilla projektikansioosi, esimerkiksi <code>cd ~/Projects/project</code> ja ajamalla <code>cap install</code>. Tämän jälkeen nappaa uusin deployconfig Google Drivestä hakemiston <b>Dude/Palvelin/Deployconfigs (latest)/deploy/production.rb</b> alta. Valitse kaikki, kopioi ja liitä projektin alla olevaan avattuun production.rb-tiedostoon.

Korvaa tiedostosta kaikki <b>DOMAIN</b> -tekstit projektin oikealla päädomainilla, esim. asiakas.fi. Täytä myös käyttäjätunnuksesi ja salasanasi.

Tuplatsekkaa, että komennot ovat kunnossa, etenkin testiympäristön ja staging (vaiheessa.fi) osoitteet.

<h4>2. Alustavan deployn ajaminen</h4>

Siirry Terminalilla projektikansioosi, esimerkiksi <code>cd ~/Projects/project</code> ja aja deploy-komento seuraavasti:

<pre class="language-bash"><code>cap production deploy</code></pre>

Saat viestin: <b>ERROR linked file /var/www/asiakas.fi/deploy/shared/.env does not exist</b>, tämä on normaalia ja kuuluu asiaan.

<h4>3. Tuotantoympäristön asettaminen tietokantaa varten</h4>

1. Avaa paikallisen projektin <b>.env</b>-tiedosto ja muokkaa siitä <b>WP_ENV</b>=production <b>DB_HOST</b>=ghostin tai craftin <u>paikallinen</u> IP-osoite tähän (craftin tietokantapalvelin on beardfish ja paikallinen IP on 192.168.0.4, ghostin tietokantapalvelin on faith ja paikallinen IP on 192.168.0.6).
2. Lisää <b>DB_USER</b> ja <b>DB_NAME</b>-kohtiin esimerkiksi projektin nimi. Jätä salasana toistaiseksi tyhjäksi. Vaihda <b>WP_HOME</b> ja <b>WP_SITEURL</b> -kohtiin projektin oikea tuotanto-osoite, <b>huom!</b> http:// tässä vaiheessa, ei https://. SSL-sertifikaatti nimittäin asennetaan myöhemmässä vaiheessa, sitten kun sivut näkyy ulkomaailmalle.

Tässä vaiheessa .env-tiedoston pitäisi näyttää jotakuinkin tältä:
<pre class="language-bash"><code>DB_NAME=projektinnimi
DB_USER=projektinnimi
DB_PASSWORD=
DB_HOST=192.168.0.6

WP_ENV=production
WP_HOME=http://www.asiakas.fi
WP_SITEURL=http://www.asiakas.fi/wp
AUTH_KEY=...</code></pre>

<u>Älä tallenna</u> tiedostoa paikallisen tiedostosi päälle, ota se vaan talteen! jätä auki tässä vaiheessa, luodaan seuraavaksi kannan salasana .env-tiedostoa varten.

3. Seuraavaksi kirjaudu tietokantapalvelimelle seuraavasti. Kirjaudu ensin valitulle edustapalvelimelle (<i>ghost.dude.fi</i>, <i>craft.dude.fi</i>), aliaksella <code>craft</code> tai <code>ghost</code>, jos olet luonut sellaisen, jos taas et, perinteisesti <code>ssh käyttäjänimesi@185.87.110.9</code> (ghost), <code>ssh käyttäjänimesi@185.87.110.7</code> (craft).

Kirjauduttuasi edustapalvelimelle, kirjaudu sitä kautta tietokantapalvelimelle. Jos käytät craftia, kirjaudu beardfish-tietokantapalvelimelle komennolla <code>ssh käyttäjätunnus@192.168.0.4</code>, jos taas ghostia, kirjaudu faith-tietokantapalvelimelle komennolla <code>ssh käyttäjätunnus@192.168.0.6</code>.

Kun olet palvelimella, kirjaudu tietokannan komentorivitulkille komennolla:

<pre class="language-bash"><code>mysql -u root -p</code></pre>

Tämän jälkeen aja seuraavat komennot (ylöspäin painaminen helpottaa, sillä historiasta saat pohjan myös).

Luodaan ensin tietokanta projektille:

<pre class="language-sql"><code>CREATE USER 'projektinnimi'@'192.168.0.7' IDENTIFIED BY 'TÄHÄN_1PASSWORDISSA_GENEROITU_VAIKEA_SALASANA';</code></pre>

<b>Huom!</b> IP-osoitteeksi tulee paikallinen IP, craftin on 192.168.0.5 ja ghostin 192.168.0.7.

Sitten lisätään oikeudet projektikohtaiselle käyttäjälle:

<pre class="language-sql"><code>GRANT ALL PRIVILEGES ON projektinnimi.* TO 'projektinnimi'@'192.168.0.7';</code></pre>

Otetaan muutokset käyttöön:

<pre class="language-sql"><code>FLUSH PRIVILEGES;</code></pre>

4. Tässä vaiheessa kopioi salasana talteen. Tätä salasanaa ei tallenneta mihinkään, edes 1Passwordiin. Liitä salasana auki jättämääsi tallentamattoman .env-tiedoston <b>DB_PASSWORD</b> -kohtaan.

5. Ellet jo ole, kirjaudu edustapalvelimelle (<i>ghost.dude.fi</i>, <i>craft.dude.fi</i>), aliaksella <code>craft</code> tai <code>ghost</code>, jos olet luonut sellaisen, jos taas et, perinteisesti <code>ssh käyttäjänimesi@185.87.110.9</code> (ghost), <code>ssh käyttäjänimesi@185.87.110.7</code> (craft).

Avaa muokkaukseen tiedosto, josta deploy-komento aiemmin herjasi, tämän näköisellä komennolla:

<pre class="language-bash"><code>nano /var/www/asiakas.fi/deploy/shared/.env</code></pre>

Valitse kaikki auki olevasta .env-tiedostostasi ja liitä sisältö komentorivi-ikkunassasi auki olevaan tyhjään .env-tiedostoon. Tallenna näppäinyhdistelmällä <kbd>CTRL + O</kbd> ja poistu <kbd>CMD + X</kbd>. 

<h4>4. Tietokannan luominen ja tuominen</h4>

1. Avaa <b>Sequel Pro</b>. Kirjaudu gunship -nimiselle staging palvelimelle (tunnukset ja Sequel Pro -asetukset 1Passwordista ja kollegoilta), valitse työstössä olevan projektin tietokanta, valikosta <b>File > Export...</b>.

2. Kirjaudu valitasemallesi tuotantopalvelimelle (craft tai ghost, mainittu aiemmin), valitse vasemman ylälaidan pudotusvalikko ja sieltä <b>Add Database...</b>, kirjoita projektin nimi (sama mikä .env <b>DB_NAME</b> kohdassa), valitse kanta ja tuo kanta valikosta <b>File > Import...</b>.

Tietokanta on nyt kunnossa ja voidaan siityä eteenpäin.

<h4>5. Projektin koodipohjan julkaiseminen (deploy) palvelimelle</h4>

Aja uudestaan deploy-komento:

<pre class="language-bash"><code>cap production deploy</code></pre>

Tällä kertaa komento meneee läpi sujuvasti. Komento ajaa WordPressin, teemat ja lisäosat sisään, sekä korvaa dev- ja staging-urlit tuotannon urlilla (WP-CLI).

Sillä välin kun deployscripti on ajossa, voidaan siirtyä mediakirjaston siirtämiseen.

<h4>6. Mediakirjaston vieminen palvelimelle</h4>

1. Avaa FileZilla (tai muu käyttämäsi SFTP-ohjelma) ja kirjaudu staging-palvelimelle (gunship). Mene <b>/var/www/projektinnimi/shared/media</b> ja kopioi uusimmat mediakirjaston tiedostot sekä backup-kansio paikalliseen projektiisi.

2. Vedä media-kansion kuvat (ei backup) <a href="https://imageoptim.com/mac">ImageOptimin</a> läpi.

3. Kirjaudu tuotantopalvelimelle, jonne projekti on deployattu (craft tai ghost) ja kopioi mediatiedostot tuotantoon <b>/var/www/asiakas.fi/public_html/media</b>.

<h4>7. Virtualhostin luominen tuotantopalvelimelle</h4>

Tässä vaiheessa sivuston tiedostot ja tietokanta ovat paikallaan, mutta mikään muu web-palvelimella ei ole vielä kunnossa tai vastaa osoitteisiin, koska vhostia ei ole luotu. Se tapahtuu automatisoidusti seuraavasti:

<pre class="language-bash"><code>sudo bash /etc/bin/release-site.sh</code></pre>

Scripti käytännössä kysyy pelkästään päädomainia ilman www:tä (esimerkiksi asiakas.fi) ja luo nginxiä varten tiedostot kansioihin /etc/nginx/sites-available/, symlinkittää ne käyttöön /etc/nginx/sites-enabled/, luo poolin php-fpm:lle ja käynnistää palvelimet uudestaan sen jälkeen kun on kysynyt sinulta näkyikö testikomennoilla virheitä.

<h4>8. Sivuston toiminnan testaaminen paikallisesti</h4>

Ennen sivut julkaistaan maailmalle päivittämällä domainin nimipalvelintietueita, on hyvä tehdä lopputestaukset ja varmistaa että vhost toimii. Se tehdään muokkaamalla omalla koneella hosts-tiedostoa:

<pre class="language-bash"><code>sudo nano /etc/hosts</code></pre>

Lisää tiedoston pohjalle IP (ghost tai craft) ja sen perään asiakkaalla käytössä olevat domainit. Ghostin tapauksessa rivi näyttäisi tältä:

<pre class="language-bash"><code>185.87.110.7 asiakas.fi www.asiakas.fi</code></pre>

Tallenna näppäinyhdistelmillä <kbd>ctrl + o</kbd> ja poistu <kbd>ctrl + x</kbd> näppäimillä.

Nyt sinun pitäisi päästä katsomaan sivustoa kun menet selaimella asiakkaan domainiin. Saattaa vaatia selaimen refreshausta tai jopa ihan tuoretta selainta, ei välttämättä ihan heti haista muutosta hosts-tiedostosta.

<h4>10. Oikeudet kuntoon</h4>

Deploy-komennon myötä saattaa usein jäädä esimerkiksi mediakirjaston oikeudet eri käyttäjälle, joten kannattaa ajaa automatisoitu oikeudenkorjaus script (joka pyörii säännöllisesti cronissa, mutta vain kaksi kertaa päivässä):

<pre class="language-bash"><code>sudo bash /etc/bin/correct-permissions.sh</code></pre>

<h4 id="tarkistuslista">11. Ajolista</h4>

Käy sivut läpi niin edustan puolella kuin wp-adminissakin ja katso että kaikki toimii. Sitten siirry käymään tarkistuslistaa läpi.

Ennen julkaisua ja julkaisun jälkeen käydään <u>aina</u> tarkistuslista huolellisesti läpi. Listaa päivitetään Google Sheetiin, josta se ladataan Todoist Template-yhteensopivassa .csv-muodossa ja tuodaan projektiin mukaan. Tässä vaiheessa on hyvä avata lista, ohje:

[video width="1768" height="1080" mp4="http://handbook.dude.fi/media/todoist.mp4"][/video]

<a href="https://docs.google.com/spreadsheets/d/1Dpa-aDcf6NNZMi7DT7Q-ppOgEJ_fgPxB_-pxELKurTs/edit?usp=sharing">Lataa lista Google Sheetistä</a> - Dudelta löytyy muokkausoikeus, muilta katseluoikeus.

<h4>12. Domainin ja nimipalvelinten ohjaus</h4>

Kun ajolista on käyty läpi, on aika julkaista sivusto maailmalle. Tämä vaihe koskee vain ylläpitoasiakkaita, joiden domain on Duden hallinnassa.

1. Kirjaudu <a href="https://www.cloudflare.com/">Cloudflareen</a>. Mene kohdasta <b>Menu > domainisi.fi</b>.
2. Kirjaudu <a href="https://registry.domain.fi">registry.domain.fi</a> tai jos domain on jonkun muun kuin .fi päätteinen, <a href="https://www.namecheap.com/myaccount/login">namecheap.com/myaccount/login</a>. Mene domainin asetuksiin ja päivitä nimipalvelimet ohjeiden mukaisesti (<i>chan.ns.cloudflare.com</i> ja <i>cody.ns.cloudflare.com</i>).
3. Paina Cloudflaren kautta Re-Check -nappia.
4. Poista tässä vaiheessa <b>/etc/hosts</b> -tiedostostasi aiemmin asetettu rivi. Tässä vaiheessa odotellaan että sivusto tulee näkyviin.
5. Lisää A-recordit. @ ja www -tietueet laitetaaan osoittamaan valitulle palvelimelle (craft: <i>185.87.110.7</i> tai ghost: <i>185.87.110.9</i>).
6. Odota kun domain tulee voimaan.

<h4>13. HTTPS-sertifikaatin asentaminen</h4>

Kun sivusto näkyy maailmalle ja nimipalvelimet ovat päivittyneet (tämän voit tarkistaa kirjautumalla craftille tai ghostille ja pingaamalla domainia komennolla <code>ping asiakas.dude.fi</code>, jos IP ei ole craftin tai ghostin, ei muutos ole vielä voimassa)

Tämäkin työ on automatisoitu ja homman saa hoidettua yhdellä komennolla:

<pre class="language-bash"><code>sudo bash /etc/bin/ssl.sh</code></pre>

Seuraa ohjeita tarkasti. Komento generoi sertifikaatin Let's Encryptillä, eli käytännössä ajaa certbot-auto-komennon listatuille domaineille.

Kun komento on ajettu, sivusto toimii oikein https-osoitteella ja ohjaa http:n https:ään automaattisesti.

<h4>14. Ohjaa asiakas.vaiheessa.fi tuotantoon</h4>

Jos sivustoa ei heti jatkokehitetä, kannattaa staging-osoite ohjata tuotantoon siltä varalta että asiakas menee vahingossa tekemään näyttöversioon muutoksia, jotka eivät tule voimaan tuotantoversioon.

Ohjaus tehdään simppelillä php-tiedostolla, jonka saat kopioitua esimerkiksi edellisestä projektista. Kirjaudu gunshipille komentorivillä ja kopioi edellisestä projektista tai alta tiedosto <b>redirect-to-production.php</b> projektin mu-plugins -kansioon:

<pre class="language-php"><code>&lt;?php
/**
 * Redirect staging site to production. Place this file to mu-plugins directory.
 *
 * Plugin Name: Redirect site to production
 * Plugin URI:
 * Description:
 * Version: 1.0.0
 * Author: Digitoimisto Dude Oy, Timi Wahalahti
 * Author URI: https://www.dude.fi
 * Requires at least: 4.7
 * Tested up to: 5.2
 * License: GPLv3
 * License URI: https://www.gnu.org/licenses/gpl-3.0.html
 *
 * @Author:                         sippis, Digitoimisto Dude Oy (https://dude.fi)
 * @Date:                           2019-05-15 11:48:23
 * @Last Modified by:   sippis
 * @Last Modified time: 2019-05-15 11:50:20
 */

if ( ! defined( 'ABSPATH' ) ) {
    exit();
}

add_action( 'init', function() {
    wp_redirect( 'https://asiakas.fi' );
} );</code></pre>

<h4>15. Loppusilaukset ja viimeiset testaukset</h4>

Tässä vaiheessa on hyvä rämpätä vielä sivusto kertaalleen läpi. Katso myös <a href="#tarkistuslista">ajolistan</a> <b>Julkaisun jälkeen</b> listan kohdat.

Onnittelut, olet juuri julkaissut sivuston!