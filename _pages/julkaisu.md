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
<h3>Deploy-toimenpiteet</h3>
Deployn automatisointi tapahtuu <a href="http://capistranorb.com/">Capistranon</a> avulla, joka on osa <a class="github" href="https://github.com/digitoimistodude/dudestack">digitoimisto/dudestack</a>-kokonaisuutta. Ensimmäinen deploy suoritetaan aina Capistranon työkalulla, mutta esim. pienet teemapäivitykset hoidetaan suoralla sftp- tai rsync-yhteydellä.

Muutosten myötä tulee muistaa ngx-pagespeed-välimuistin tyhjennys:
<pre class="language-bash"><code>sudo rm -rf /tmp/pgsp/v3/domain.fi</code></pre>
Uusin deployconfig tuotantoon ja stagingiin löytyvät Dropboxista, hakemistopolusta <b>Dude/Palvelin/Deployconfigs (latest)</b>.
<h3>Vaiheet</h3>
Duden julkaisutoimenpiteet eli deploy on monivaiheinen ja varsinaista tiedonsiirtoa ja kansiorakennetta lukuunottamatta (Capistrano) enimmäkseen manuaalinen. Käsipelillä asioiden tekemisellä pyrimme varmistamaan että kaikki menee varmasti kuten pitääkin. Kokonaisuudessaan vaiheisiin kuluu testausta lukuunottamatta aikaa noin varttitunti.

<b>Huom!</b> Vaiheiden järjestys on projektikohtainen, seuraavassa esitetty järjestys ei välttämättä päde käynnissä olevaan projektiisi. Julkaisun työvaiheet ovat seuraavat:
<h4>1. Virtualhostin luominen tuotantopalvelimelle</h4>
Kirjaudu valitulle edustapalvelimelle (<i>ghost.dude.fi</i>, <i>craft.dude.fi</i>). Ota vhost-pohja (Dropbox tai edellinen sivusto) ja tallenna vhost seuraavasti:
<pre class="language-bash"><code>sudo pico -w /etc/nginx/sites-available/domain.fi
sudo ln -s /etc/nginx/sites-available/domain.fi /etc/nginx/sites-enabled/domain.fi</code></pre>
Kommentoi piiloon rivit <b>ssl_certificate</b> ja <b>ssl_certificate_key</b> tässä vaiheessa, sillä sertifikaattia ei voida hakea ennen kuin domain on toiminnassa. Tallenna näppäinyhdistelmillä <kbd>ctrl + o</kbd> ja poistu <kbd>ctrl + x</kbd> näppäimillä.
<h4>2. Kansioiden ja käyttöoikeuksien luominen</h4>
Luo tarvittavat kansiot:
<pre class="language-bash"><code>sudo mkdir -p /var/www/domain.fi &amp;&amp; sudo mkdir -p /var/www/domain.fi/public_html &amp;&amp; sudo mkdir -p /var/www/domain.fi/tmp</code></pre>
Vaihda väliaikaisesti käyttöoikeudet itsellesi deployta varten:
<pre class="language-bash"><code>sudo chown -R $(whoami) /var/www/domain.fi</code></pre>
Testaa syntaksivirheiltä:
<pre class="language-bash"><code>sudo nginx -t</code></pre>
Käynnistä nginx uudelleen:
<pre class="language-bash"><code>sudo service nginx restart</code></pre>
<h4>3. Deploy-config tiedoston asettaminen</h4>
<a class="github" href="https://github.com/digitoimistodude/dudestack">digitoimisto/dudestack</a>in aloitusscripti (lisää kohdassa <a href="https://handbook.dude.fi/wordpress-kehitys/projektin-aloitus">Projektin aloitus</a>) määrittää oletuskonffit valmiiksi, mutta julkaistaessa on hyvä tarkistaa että config on ajan tasalla. Ensin säädä siis <b>config/deploy/production.rb</b> -tiedosto kuntoon.
<h4>4. Nimipalvelinten ohjaus</h4>
<b>Ylläpitoasiakkaille:</b> Ota talteen domainin siirtoavain tai välittäjänvaihtotunnus (siirtyvä domain) tai rekisteröi uusi domain. Tämän jälkeen päivitä nimipalvelimet Cloudflarelle. Lisää @ ja www -tietueet osoittamaan valitulle palvelimelle (craft: <i>185.87.110.7</i>, ghost: <i>185.87.110.9</i>).

Odota kun domain tulee voimaan. Jos aikataulu on kriittinen, voit testata tuotantopalvelimen jo etukäteen lisäämällä rivin /etc/hosts-tiedostoon seuraavasti:
<pre class="language-bash"><code>185.87.110.7 domain.fi www.domain.fi</code></pre>
<h4>5. HTTPS-sertifikaatti</h4>
Kun nimipalvelimet ovat päivittyneet, laita SSL-sertifikaatti paikalleen:
<pre class="language-bash"><code>/opt/letsencrypt/certbot-auto certonly --webroot -w /var/www/domain.fi/public_html -d domain.fi -d www.domain.fi</code></pre>
Jos palvelimella on ohjauksia muista domaineista, lisää seuraava ennen muita location-blokkeja ohjausten server-blokkien sisään:
<pre class="language-nginx"><code>location /.well-known/ {
    root /var/www/domain.fi/public_html;
}</code></pre>
<h4>6. Tietokantatunnuksen ja käyttöoikeuksien luominen tuotantopalvelimelle</h4>
Kirjaudu tuotannon tietokantapalvelimelle (<i>beardfish.dude.fi</i>, <i>faith.dude.fi</i>) ja luo tietokanta seuraavilla komennoilla (kohtiin <i>projektinnimi</i>, <i>turvallinensalasana</i> ja edustapalvelimesta riippuen <i>192.168.0.5</i> (craft) tai <i>192.168.0.7</i> (ghost)):
<pre class="language-sql"><code>CREATE USER 'käyttäjänimi'@'192.168.0.5' IDENTIFIED BY 'turvallinensalasana';
GRANT ALL PRIVILEGES ON käyttäjänimi.* TO 'tietokannannimi'@'192.168.0.5';
FLUSH PRIVILEGES;
</code></pre>
Nämä komennot löytyvät myös kun painat ylöspäin, jos olet laittanut ne aikaisemminkin. Lopuksi kirjaudu ulos palvelimelta.
<h4>7. Luo tietokanta tuotantopalvelimelle</h4>
Kirjaudu SSH-tunneloinnin avulla (Sequel Pro) tietokantapalvelimelle. Luo tyhjä tietokanta valitsemallesi nimelle.
<h4>8. Siirrä tietokanta</h4>
Exporttaa tietokanta staging-ympäristöstä (<i>gunship.dude.fi</i>) ja importtaa se tuotantoympäristöön (Sequel Pro).
<h4>9. Aja ensimmäinen (initial) deploy ja lisää ympäristön määrittelyt ja tunnukset .env-tiedostoon</h4>
Tarkista tässä vaiheessa että composer.json-tiedosto on ajan tasalla ja sisältää kaikki oleelliset lisäosat. Sitten aja deploykomento projektikansiossa:
<pre class="language-bash"><code>cap production deploy</code></pre>
Ensimmäisellä kerralla saat virheen, tämä on normaalia.
<pre class="language-bash"><code>00:02 deploy:check:linked_files
      ERROR linked file /var/www/domain.fi/deploy/shared/.env does not exist on 185.87.110.7</code></pre>
Kopioi hakemistopolku talteen ja luo .env-tiedosto seuraavasti
<pre class="language-bash"><code>sudo pico -w /var/www/domain.fi/deploy/shared/.env</code></pre>
Liitä .env-tiedosto projektikansiosta muuttaen saltteja ja avaimia lukuunottamatta tiedot vastaamaan tuotantoa (<i>WP_ENV=production</i>).
<h4>10. Siirrä ja optimoi mediakirjasto</h4>
Kirjaudu staging-palvelimelle SFTP:llä (<i>craft.dude.fi</i>) ja hae kuvat projektihakemistosi <i>shared/media</i> -kansiosta. Tämän jälkeen vedä media-kansio ImageOptimin läpi.

Siirrä optimoidut kuvat tuotantopalvelimelle <i>/var/www/domain.fi/deploy/shared/media</i> -kansioon.
<h4>11. Julkaisu! Aja varsinainen deploy-komento</h4>
On virallisen julkaisutoimenpiteen aika. Aja uudestaan komento:
<pre class="language-bash"><code>cap production deploy</code></pre>
<h4>13. Ohjaa testiympäristö tuotantoon</h4>
Muokkaa testiympäristön vhostia:
<pre class="language-bash"><code>sudo pico -w /etc/nginx/sites-enabled/asiakas.dude.fi</code></pre>
Lisää rivi:
<pre class="language-nginx"><code>rewrite ^/projektinnimi(.*)$ https://www.domain.fi permanent;</code></pre>
Testaa syntaksivirheiltä:
<pre class="language-bash"><code>sudo nginx -t</code></pre>
Tallenna ja käynnistä nginx-prosessit uudelleen:
<pre class="language-bash"><code>sudo service nginx restart</code></pre>
<h4>14. Loppusilaukset, käyttöoikeuksien tarkistus ja sivuston testaus</h4>
Vaihda käyttöoikeudet ja varmista samalla että tiedostojen lisääminen mediakirjastoon toimii:
<pre class="language-bash"><code>sudo chown -R www-data:developers /var/www/domain.fi &amp;&amp; sudo chown -R $(whoami) /var/www/domain.fi/public_html/content/themes &amp;&amp; sudo chown -R $(whoami) /var/www/domain.fi/tmp &amp;&amp; sudo chmod -R 775 /var/www/domain.fi/public_html/content &amp;&amp; sudo chmod -R 775 /var/www/domain.fi/deploy/current/content &amp;&amp; sudo chmod -R 775 /var/www/domain.fi/deploy/shared</code></pre>
Käy sivut läpi niin edustan puolella kuin wp-adminissakin ja katso että kaikki toimii. Sitten siirry käymään tarkistuslistaa läpi.
<h3>Tarkistuslista</h3>
Ennen julkaisua ja julkaisun jälkeen käydään <u>aina</u> seuraava tarkistuslista huolellisesti läpi. Lista löytyy myös Dropboxista, kansiosta <b>Dude/Tärkeät asiakirjat/muut/Ennen julkaisua huomioitavaa.todo</b>, jota on ylläpidettävä samaan tahtiin kuin alla olevaa. Dokumentin voi myös kopioida projektikansioon ja ruksata SublimeTextin PlainTasks -packagea hyödyntämällä.
<h3>Ennen julkaisua</h3>
☐ WordPress yleiset asetukset
☐ Faviconit ja muut ikonit
☐ Testaa templatet läpi: haku, arkisto, avainsanat, ym.
☐ Google Analytics
☐ Tarvittavat uudelleenohjaukset
☐ Bloggauksen muotoilujen tarkistaminen
☐ Lomakkeiden testaus
☐ Katso ettei missään lue "Etusivu", perus SEO-asiat kuntoon
☐ screenshot.png päivittäminen
☐ style.css - teeman tiedot kuosiin
☐ Optimoi kuvat ImageOptimilla/Imagify (/media ja teeman kuvakansio)
☐ Lisää maksullisien lisäosien lisenssit paikalleen
☐ WordPress-päivitykset
☐ .htaccess Redirect 301 /asiakas http://www.asiakas.fi tai nginx-redirectit, jos on
☐ Jos sopii projektiin/sovittu/saittiuudistus: kuvakaappauksia Google-näkyvyyden tilanteesta ennen julkaisua (Firefoxin full-page screenshot-toiminto)
☐ Esteettömyystestaus WAVElla
☐ Esteettömyys: Tarkista, että wp_localize_script stringit lukulaitteille (screenReaderText) ovat oikealla kielellä
☐ Aja <b>gulp uncss</b> kun tiedät että CSS:ään ei tule enää muutoksia
☐ SendGrid API key ja .env tarkistus
☐ <a href="http://a11yproject.com/checklist.html">Web Accessibility Checklist</a>
<h3>WooCommerce</h3>
☐ Tarvittaessa: <a href="http://docs.wp-rocket.me/article/27-using-wp-rocket-on-your- ecommerce-site">Verkkokaupan Cache</a>
☐ Maksut päälle
<h3>Julkaisun jälkeen</h3>
☐ WP Rocket päälle
☐ ManageWP päälle
☐ <a href="https://dashboard.adminlabs.com/">AdminLabs</a> -seuranta päälle
☐ <a href="https://analytics.google.com/analytics/web/">Google Analytics</a> -tsekkaus
☐ HTTPS-sertifikaatti
☐ Nopeuden testaus <a href="http://developers.google.com/speed/pagespeed/insights/">PageSpeed Insightin</a> avulla
☐ Testaa nopeus <a href="https://tools.keycdn.com/speed">KeyCDN palvelulla</a>
☐ Lomakkeiden testaus
☐ Sähköpostiliikenteen testaus (SendGrid)
☐ Backupit päälle (muokkaa /etc/bin/backup.conf ja lisää uudelle riville sivustonnimi. , tietokannannimi)
☐ Asiakastyytyväisyyskysely (Typeform)
☐ Testaa Internet Exporer 11
☐ Maililla tieto asiakkaalle joka kuukauden huoltokatkosta sekä status.dude.fi osoite
<h3>Extraa</h3>
☐ "Toteutus: DUDE" footeriin, linkki ja lupa
☐ Testaa typografia blogissa, <a href="https://dudetest.xyz/air/wp/wp-admin/post.php? post=1134&amp;action=edit">kopioi mallipohja tästä</a>
☐ HTML:n validointi <a href="https://validator.w3.org/">W3 validaattorilla</a>
☐ Estä trace- ja pingbackien lähettäminen
☐ Mikroformaatit, schemat, ks. <a href="http://www.google.com/webmasters/tools/richsnippets">Google Rich Snippets</a>
☐ Käy pääpiirteittäin läpi <a href="http://webdevchecklist.com/">Webdev checklist</a>