---
ID: 85
post_title: Projektin aloitus
author: Roni
post_excerpt: ""
layout: page
permalink: >
  https://handbook.dude.fi/wordpress-kehitys/projektin-aloitus
published: true
post_date: 2017-08-04 14:58:17
---
Dude-ympäristön pystytysohjeet uudelle tietokoneelle löytyy GitHubista, <a class="github" href="https://github.com/digitoimistodude/dudestack-instructions">dudestack/instructions</a>.

Vaikka projektin aloitustoimenpiteemme ovatkin enimmäkseen automatisoituja (yksi aloituskomento säästää 10 tuntia aikaa työstä joka normaalisti pitäisi tehdä käsipelillä), on jonkin verran manuaalista työtä, sillä kaikkea ei voi eikä kannata automatisoida huolellisuuden kustannuksella. Lisäksi projektin jatkaja hyppää projektiin mukaan myöhemmin, eikä voi käyttää aloituskomentoja ja näin ollen asioita on tehtävä käsin.
<h3>Ensimmäisen aloittajan tehtävät</h3>
Vaiheet:

1. Ensimmäinen projektin parissa aloittava dude aloittaa projektin ajamalla aloituskomennon:
<pre class="language-bash"><code>createproject</code></pre>
Scripti kysyy oleelliset tiedot projektista, kuten projektin nimen. Sen jälkeen automaatio luo projektin raamit (<a class="github" href="https://github.com/digitoimistodude/dudestack">digitoimistodude/dudestack</a>), luo paikalliselle kehityskonelle (<a class="github" href="https://github.com/digitoimistodude/marlin-vagrant">digitoimistodude/marlin-vagrant</a>) virtualhostin sekä WordPress-stackin asiakkaan projektia varten.

2. Seuraavaksi ajetaan newtheme.sh (<a class="github" href="https://github.com/digitoimistodude/air">digitoimistodude/air</a>), joka tarpeelliset tiedot kysyttyään luo projektiin aloitusteeman.

3. Ensimmäinen aloittaja luo seuraavaksi tietokannan kehityspalvelimelle (gunship) seuraavasti. Tämä siksi, että sivustolla tehdyt muutokset pysyy samaan aikaan syncassa asiakkaalla ja kaikilla devaajilla ilman että tarvitsee jatkuvasti harrastaa import-export-import-rallia.

Luodaan ensin tietokanta projektille (gunship):

<pre class="language-sql"><code>CREATE USER 'projektinnimi'@'%' IDENTIFIED BY 'TÄHÄN_1PASSWORDISSA_GENEROITU_VAIKEA_SALASANA';</code></pre>

Sitten lisätään oikeudet projektikohtaiselle käyttäjälle:
<pre class="language-sql"><code>GRANT ALL PRIVILEGES ON projektinnimi.* TO 'projektinnimi'@'%';</code></pre>

Otetaan muutokset käyttöön:
<pre class="language-sql"><code>FLUSH PRIVILEGES;</code></pre>

4. Uploadaa createprojectin kautta luotu paikallinen tietokanta gunshipille Sequel Prolla ja vaihda tiedot .env-tiedostoon.

5. Tämän jälkeen projektin aloittaja tallentaa .env- määritykset sekä <a href="https://www.resilio.com/individuals/">Resilio Sync</a> -linkin 1Passwordiin Secure Noteksi. Tarvittaessa aloittajadevaaja jakaa tunnareita Slackin tai Trellon kautta muille projektissa mukana oleville devaajille.

6. Avaa projekti editoriisi käyttämäsi editorin komennolla, esim. <code>code ~/Projects/projektinnimitähän</code> (Visual Studio Code) tai <code>subl ~/Projects/projektinnimitähän</code> (Sublime Text). Tämän jälkeen tallenna projekti nimellä painamalla <kbd><kbd>⌘</kbd> <span>+</span> <kbd>⇧</kbd> <span>+</span> <kbd>P</kbd></kbd> ja kirjoittamalla <b>Add New Project</b> ja enter. Nimeä projekti samalla nimellä kuin kansio, eli uudelleen enter. Tämän jälkeen löydät projektisi jatkossa kun painat <kbd><kbd>⌘</kbd> <span>+</span> <span>+</span> <kbd>⇧</kbd> <span>+</span> <kbd>O</kbd></kbd> (jos ei toimi niin varmista että <a href="https://github.com/ronilaukkarinen/vscode-settings/blob/01ad756ad23364365543bc0268cf61da08359465/keybindings.json#L8" class="github">keybindings.json</a> on käytössä, tämän saat varmistettua kun haet <kbd><kbd>⌘</kbd> <span>+</span> <kbd>⇧</kbd> <span>+</span> <kbd>P</kbd></kbd> "Preferences: Open Keyboard Shortcuts (JSON)" ja katsot löytyykö kyseinen näppäinkomento).
<h3 id="myohemmin-projektiin-mukana-tulevan-devaajan-tehtavat">Myöhemmin projektiin mukana tulevan devaajan tehtävät</h3>
Vaiheet:

1. Muut mukaan tulevat devaajat menevät <a href="https://github.com/digitoimistodude/">Duden Githubiin</a>, josta valitsevat aloitetun projektin kloonaavat projektin <b>Code</b>-nappulan avulla <code>~/Projects</code> -hakemistoon (Terminalissa: <code>cd ~/Projects</code> ja sen jälkeen git clone <i>url</i>).

<img src="https://handbook.dude.fi/media/Screen-Shot-2021-01-21-13-29-22.56.png" alt="Ohjeistuskuva, paina ensin Code-nappia" />

2. Luo uusi tiedosto projektikansion alle nimeltä <code>.env</code> (esim. <code>code .env</code> tai <code>nano ~/Projects/projektinnimi/.env</code>) ja lisää sinne saamasi tiedot. Tyypillinen .env-tiedosto näyttää tältä:
<pre class="language-properties"><code>DB_NAME=tässä_on_oikea_tietokannan_nimi
DB_USER=tässä_on_oikea_käyttäjätunnus
DB_PASSWORD=tässä_on_oikea_salasana
DB_HOST=tässä_on_oikea_ip

WP_ENV=development
WP_HOME=https://projektinnimi.test
WP_SITEURL=https://projektinnimi.test/wp
AUTH_KEY='ts[h@+i#]w`Zj%$!*+N:b*K$re9;w*mQ:;Y76G@~wx?::9%j@~}i3dmz|Jcl{|'
SECURE_AUTH_KEY='gJ6.c|6+v~`s}0,^945V#uY]TXuW9gV&amp;Po!SnCKJsB2fV-WlLd]629mm~8_;qXL'
LOGGED_IN_KEY='Eu`SWA&lt;^2P_P:1?i|c=541(&amp;QMYM3h[,B$L]az02%He@;c).e#08zEL&amp;*;oGd/AF'
NONCE_KEY='@#p@/&amp;A@jEJeGo|K}0fm`R8NcaQaA @??J:%97[|c&gt;Gr&gt;*eO[qFAe|$h|qhA?)z'
AUTH_SALT=':ov!]~U]=Jqjy.o#*EddJd*Qd,YD=D3~S{ZC%gn7QD*%y+MbwQf5U iX&amp;69:QYP'
SECURE_AUTH_SALT='Ck(dq+!6vNHTF-U1xZt*IBAk.n)+4DH=Nl;4d5xyf4*LLy?8]sLsT@DO]iGOM$H}'
LOGGED_IN_SALT=']CR.^maG`L*oKL?3 qiTTXE2~)b2m&gt;NPFBKhOKNE qSt1R K8+`nOu&amp;Ea*,n6G2'
NONCE_SALT='?8|fjJSNs8=LwJt6dkWrY*.~(# +EpUC]TI,~}HhVzS*9@K$ =+H!{wOYeG&gt;t}rd'

ACF_PRO_KEY=tässä_on_oikea_API_key
SENDGRID_API_KEY=tässä_on_oikea_API_key
IMAGIFY_API_KEY=tässä_on_oikea_API_key</code></pre>
3. Jos <b>et käytä</b> gunshippiä vaan paikallista tietokantaa, avaa Sequel Pro, luo tyhjä tietokanta, sitten lataa työkaverilta saamasi tietokanta sisään valikosta File &gt; Import.

4. Seuraavaksi haetaan riippuvuudet ajamalla projektin juuressa:
<pre class="language-bash"><code>composer install &amp;&amp; npm install</code></pre>

5. Sitten teeman riippuvuudet menemällä teemakansioon

<pre class="language-bash"><code>cd ~/Projects/projektinnimi/content/themes/teemannimi</code></pre>

Tämän jälkeen asenna paketit komennolla:

<pre class="language-bash"><code>npm install</code></pre>

6. Sitten asetetaan manuaalisesti <i>/etc/hosts</i> -tiedostoon projektin isäntärivi, jotta kehityspalvelin osaa yhdistää oikeaan projektiin, esimerkiksi suoraan komentoriviltä muokkaamalla hosteja seuraavasti:

<pre class="language-bash"><code>sudo nano /etc/hosts</code></pre>

IP on Duden vagrant-koneella (<a class="github" href="https://github.com/digitoimistodude/marlin-vagrant">digitoimistodude/marlin-vagrant</a>) <code>10.1.2.4</code> ja Duden natiivilla macOS LEMPillä (<a class="github" href="https://github.com/digitoimistodude/macos-lemp-setup">digitoimistodude/macos-lemp-setup</a>) <code>127.0.0.1</code>. Jos esimerkiksi käytät macos-lempiä, lisää hosts tiedostoon viimeiselle riville seuraavasti:
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
Jos taas LEMP (<a class="github" href="https://github.com/digitoimistodude/macos-lemp-setup">digitoimistodude/macos-lemp-setup</a>), muokkaa komentoriviltä:

<pre class="language-bash"><code>sudo nano /etc/nginx/sites-enabled/projekti.test</code></code></pre>

Lisää yllä oleva server-block tähän tiedostoon. Tallenna näppäinyhdistelmällä <kbd><kbd>ctrl</kbd> <span>+</span> <kbd>O</kbd></kbd> ja poistu <kbd><kbd>ctrl</kbd> <span>+</span> <kbd>X</kbd></kbd>. Seuraavaksi testaa että konffi on oikein:

<pre class="language-bash"><code>sudo nginx -t</code></pre>

Tämän pitäisi antaa tulokseksi:
<pre class="language-bash"><code>nginx: the configuration file /usr/local/etc/nginx/nginx.conf syntax is ok
nginx: configuration file /usr/local/etc/nginx/nginx.conf test is successful
</code></pre>

Tämän jälkeen käynnistä web-palvelin uudelleen komennolla:

<pre class="language-bash"><code>sudo brew services restart nginx</code></pre>

Tai jos sinulla on <a href="https://github.com/digitoimistodude/macos-lemp-setup#use-linux-style-aliases">alias</a>, käytä seuraavaa samoin kuin käyttäisit staging/production-palvelimella:

<pre class="language-bash"><code>sudo service nginx restart</code></pre>

<b>Huom!</b> komennon ajaminen sudolla on tässä tärkeää, muuten muutokset eivät tule voimaan.

Yllä olevat tukeutuvat täysin siihen, että olet esimerkiksi noudattanut vagrant-boksimme asennusohjeita (<a class="github" href="https://github.com/digitoimistodude/marlin-vagrant">digitoimistodude/marlin-vagrant</a>) tai asentanut LEMP-web-palvelimemme oikeaoppisesti (<a class="github" href="https://github.com/digitoimistodude/macos-lemp-setup">digitoimistodude/macos-lemp-setup</a>) JA lisännyt myös aliakset <a href="https://github.com/digitoimistodude/macos-lemp-setup#post-install">tämän sivun pohjalta</a>.

7. Aseta mediakansio paikalleen Resilio Syncillä (olet saanut projektin aloittajalta linkin tai zip-tiedoston) projektikansion alle <code>media/</code> -hakemistoon.

8. Luo itsellesi branch, <a href="https://handbook.dude.fi/wordpress-kehitys/git-open-source#branchin-luominen">katso ohjeet tästä</a>.

9. Kirjaudu tarvittaessa sisään käyttämällä 1Passowordista löytyviä tunnuksia tai jos niitä ei ole, luo itsellesi WordPress-tunnus ajamalla wp-cli projektikansiossa (täydennä tähän komentoon tietosi):
<pre class="language-bash"><code>./vendor/wp-cli/wp-cli/bin/wp user create etunimi nimesi@dude.fi --role=administrator --user_pass=TÄHÄN_ONEPASSWORDILLA_GENEROITU_VAIKEA_SALASANA --first_name=Etunimi --last_name=Sukunimi --display_name=Etunimi</code></pre>
Näin projektin kollaboraatio saa alkaa!

<a href="https://handbook.dude.fi/wordpress-kehitys/git-open-source">Lisää git-käytänteistä.</a>

<h3>Mahdolliset virhetilanteet legacy-projekteissa</h3>

Siirryimme käyttämään gulpin versio 4:sta 26.8.2020 (<a href="https://github.com/digitoimistodude/air-light/commit/088bece978d530b795aaddcb7b134cd8ceb4dbd7#diff-3d7a4d229da48a5168c38ae7c9481d90654c540d6e389128f5d567d76d12ff78" class="github">Migrate to gulp 4, #088bece</a>). Tätä edeltävät projektit käyttävät gulp v3:sta. Gulp 3 tukee gulp 4:sta, mutta gulp 4 ei tue gulp 3:sta. Gulp3 ja gulp4 välillä tuli muutamia breaking changeja ja esimerkiksi autoprefixerin 7-versio vaatii vähintään gulp v4:n. Gulp v3 ei toimi node v12 tai uudemmalla, joten nämä voivat aiheuttaa ongelmatilanteita. Tässä pari tyypillisintä:

<pre class="language-bash"><code>ReferenceError: primordials is not defined</code></pre>

Jos käytät Gulpin versiota, joka alkaa numerolla 3 ja samanaikaisesti järjestelmässäsi on asennettuna node, jonka versio on uudempi kuin 12, ei gulp lähde käyntiin. Paras tässä kohtaa on downgradettaa node versioon 10.22.0, jolla toimii sekä uudet että vanhat projektit. Oman gulp-versiosi näet komennolla:

<pre class="language-bash"><code>gulp --version</code></pre>

Ja node-versiosi komennolla:

<pre class="language-bash"><code>node --version</code></pre>

Laske node versioon 10.22.0 seuraavasti:

<pre class="language-bash"><code>sudo npm install -g n<br>
sudo n 10.22.0</code></pre>

Jos saat seuraavanlaisen virheen node-sassista tai muusta paketista, se johtuu siitä että noden riippuvuuksia on vielä olemassa uudemmalle nodelle.

<pre class="language-bash"><code>Node Sass could not find a binding for your current environment: OS X 64-bit with Node.js 10.x</code></pre>

Tämän voit korjata helposti rebuildaamalla paketin vanhemmalle nodelle:

<pre class="language-bash"><code>npm rebuild node-sass</code></pre>

Nyt kaiken pitäisi toimia oikein.