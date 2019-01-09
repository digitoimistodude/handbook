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

Vaikka projektin aloitustoimenpiteemme ovatkin enimmäkseen automatisoituja (yksi aloituskomento säästää 10 tuntia aikaa työstä joka normaalisti pitäisi tehdä käsipelillä), on jonkin verran manuaalista työtä, sillä kaikkea ei voi eikä kannata automatisoida huolellisuuden kustannuksella. Lisäksi projektin jatkaja hyppää projektiin mukaan myöhemmin, eikä voi käyttää aloituskomentoja ja näin ollen asioita on tehtävä käsin.

<h3>Ensimmäisen aloittajan tehtävät</h3>

Vaiheet:

1. Ensimmäinen projektin parissa aloittava dude aloittaa projektin ajamalla aloituskomennon:

<pre class="language-bash"><code>createproject</code></pre>

Scripti kysyy oleelliset tiedot projektista, kuten projektin nimen. Sen jälkeen automaatio luo projektin raamit (<a class="github" href="https://github.com/digitoimistodude/dudestack">digitoimistodude/dudestack</a>), luo paikalliselle kehityskonelle (<a class="github" href="https://github.com/digitoimistodude/marlin-vagrant">digitoimistodude/marlin-vagrant</a>) virtualhostin sekä WordPress-stackin asiakkaan projektia varten.

2. Seuraavaksi ajetaan newtheme.sh (<a class="github" href="https://github.com/digitoimistodude/air">digitoimistodude/air</a>), joka tarpeelliset tiedot kysyttyään luo projektiin aloitusteeman.

3. Ensimmäinen aloittaja luo seuraavaksi tietokannan kehityspalvelimelle (gunship)

4. Tämän jälkeen projektin aloittaja jakaa .env- määritykset sekä <a href="https://www.resilio.com/individuals/">Resilio Sync</a> -linkin mediatiedostoihin Trellon tai Slackin kautta muille projektissa mukana oleville devaajille.

5. Slackin #dev-kanavalle projektin integraatio tapahtuu komennolla: <code>/github subscribe digitoimistodude/repo issues pulls deployments statuses public commits commits:all releases comments branches reviews</code>

<h3 id="myohemmin-projektiin-mukana-tulevan-devaajan-tehtavat">Myöhemmin projektiin mukana tulevan devaajan tehtävät</h3>

Vaiheet:

1. Muut mukaan tulevat devaajat menevät <a href="http://bitbucket.org/digitoimistodudeoy/">Duden Bitbucketiin</a>, josta valitsevat aloitetun projektin kloonaavat projektin <b>Clone</b>-nappulan avulla <code>~/Projects</code> -hakemistoon (Terminalissa: <code>cd ~/Projects</code> ja sen jälkeen git clone <i>url</i>).

2. Luo uusi tiedosto projektikansion alle nimeltä <code>.env</code> (esim. <code>subl ~/Projects/.env</code> tai <code>nano ~/Projects/.env</code>) ja lisää sinne saamasi tiedot. Tyypillinen .env-tiedosto näyttää tältä:

<pre class="language-bash"><code>DB_NAME=tässä_on_oikea_tietokannan_nimi
DB_USER=tässä_on_oikea_käyttäjätunnus
DB_PASSWORD=tässä_on_oikea_salasana
DB_HOST=tässä_on_oikea_ip

WP_ENV=development
WP_HOME=http://projektinnimi.test
WP_SITEURL=http://projektinnimi.test/wp
AUTH_KEY='ts[h@+i#]w`Zj%$!*+N:b*K$re9;w*mQ:;Y76G@~wx?::9%j@~}i3dmz|Jcl{|'
SECURE_AUTH_KEY='gJ6.c|6+v~`s}0,^945V#uY]TXuW9gV&Po!SnCKJsB2fV-WlLd]629mm~8_;qXL'
LOGGED_IN_KEY='Eu`SWA<^2P_P:1?i|c=541(&QMYM3h[,B$L]az02%He@;c).e#08zEL&*;oGd/AF'
NONCE_KEY='@#p@/&A@jEJeGo|K}0fm`R8NcaQaA @??J:%97[|c>Gr>*eO[qFAe|$h|qhA?)z'
AUTH_SALT=':ov!]~U]=Jqjy.o#*EddJd*Qd,YD=D3~S{ZC%gn7QD*%y+MbwQf5U iX&69:QYP'
SECURE_AUTH_SALT='Ck(dq+!6vNHTF-U1xZt*IBAk.n)+4DH=Nl;4d5xyf4*LLy?8]sLsT@DO]iGOM$H}'
LOGGED_IN_SALT=']CR.^maG`L*oKL?3 qiTTXE2~)b2m>NPFBKhOKNE qSt1R K8+`nOu&Ea*,n6G2'
NONCE_SALT='?8|fjJSNs8=LwJt6dkWrY*.~(# +EpUC]TI,~}HhVzS*9@K$ =+H!{wOYeG>t}rd'

ACF_PRO_KEY=tässä_on_oikea_API_key
SENDGRID_API_KEY=tässä_on_oikea_API_key
IMAGIFY_API_KEY=tässä_on_oikea_API_key</code></pre>

3. Jos <b>et käytä</b> gunshippiä vaan paikallista tietokantaa, avaa Sequel Pro, luo tyhjä tietokanta, sitten lataa työkaverilta saamasi tietokanta sisään valikosta File > Import.

4. Seuraavaksi haetaan riippuvuudet ajamalla projektin juuressa: 

<pre class="language-bash"><code>composer install && npm install</code></pre> 

5. Sitten teeman riippuvuudet menemällä teemakansioon <code>cd ~/Projects/projektinnimi/content/themes/teemannimi</code> ja ajamalla <code>npm install</code>

6. Sitten asetetaan manuaalisesti <code>/etc/hosts</code> -tiedostoon projektin isäntärivi, jotta kehityspalvelin osaa yhdistää oikeaan projektiin, esimerkiksi suoraan komentoriviltä muokkaamalla <code>sudo nano /etc/hosts</code> ja antamalla oman pääkäyttäjän salasana. IP on Duden vagrant-koneella (<a class="github" href="https://github.com/digitoimistodude/marlin-vagrant">digitoimistodude/marlin-vagrant</a>) <code>10.1.2.4</code> ja Duden natiivilla macOS LEMPillä (<a class="github" href="https://github.com/digitoimistodude/macos-lemp-setup">digitoimistodude/macos-lemp-setup</a>) <code>127.0.0.1</code>. Tällöin lisää hosts tiedostoon viimeiselle riville seuraavasti (IP sen mukaan mitä käytät ja projektiosoite sen mukaan mikä on käytössä):

<pre class="language-bash"><code>127.0.0.1 projektinnimi.test</code></pre>

Jos käytössä on vagrant (<a class="github" href="https://github.com/digitoimistodude/marlin-vagrant">digitoimistodude/marlin-vagrant</a>), lisää vhosts-kansioon tiedosto <code>projekti.test</code> (jos projektisi nimi on "projekti"), jonne sisältö:

<pre class="language-nginx"><code>server {
    listen 80;
    include php7.conf;
    include global/wordpress.conf;
    root /var/www/projekti;
    index index.html index.htm index.php;
    server_name projekti.test;
}
</code></pre>

Jos taas LEMP (<a class="github" href="https://github.com/digitoimistodude/macos-lemp-setup">digitoimistodude/macos-lemp-setup</a>), muokkaa komentoriviltä <code>sudo nano /etc/nginx/sites-available/projekti.test</code> ja lisää yllä oleva sinne. Linkitä se sitten päällä olevaksi saitiksi aivan kuten tekisit tuotantopalvelimellakin, komennolla <code>sudo ln -s /etc/nginx/sites-available/projekti.test /etc/nginx/sites-enabled/projekti.test</code>. Sen jälkeen käynnistä web-palvelin uudelleen komennolla <code>nginx.restart</code>.

Huom. Ylläolevat tukeutuvat täysin siihen, että olet esimerkiksi noudattanut vagrant-boksimme asennusohjeita (<a class="github" href="https://github.com/digitoimistodude/marlin-vagrant">digitoimistodude/marlin-vagrant</a>) tai asentanut LEMP-web-palvelimemme oikeaoppisesti (<a class="github" href="https://github.com/digitoimistodude/macos-lemp-setup">digitoimistodude/macos-lemp-setup</a>) JA lisännyt myös aliakset <a href="https://github.com/digitoimistodude/macos-lemp-setup#post-install">tämän sivun pohjalta</a>.

7. Aseta mediakansio paikalleen Resilio Syncillä (olet saanut projektin aloittajalta linkin tai zip-tiedoston) projektikansion alle <code>media/</code> -hakemistoon.

8. Luo itsellesi branch, <a href="https://handbook.dude.fi/wordpress-kehitys/git-open-source#branchin-luominen">katso ohjeet tästä</a>.

9. Luo itsellesi WordPress-tunnus, aja wp-cli projektikansiossa (täydennä tähän komentoon tietosi): <code>./vendor/wp-cli/wp-cli/bin/wp user create etunimi nimesi@dude.fi --role=administrator --user_pass=TÄHÄN_ONEPASSWORDILLA_GENEROITU_VAIKEA_SALASANA --first_name=Etunimi --last_name=Sukunimi --display_name=Etunimi</code> 

Näin projektin kollaboraatio saa alkaa!

<a href="https://handbook.dude.fi/wordpress-kehitys/git-open-source">Lisää git-käytänteistä.</a>