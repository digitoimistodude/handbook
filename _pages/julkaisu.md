---
ID: 102
post_title: Julkaisu
author: Roni
post_excerpt: ""
layout: page
permalink: >
  https://handbook.dude.fi/wordpress-kehitys/julkaisu
published: true
post_date: 2017-08-04 15:11:34
---
<h3>Deploy-toimenpiteet</h3>

Deployn automatisointi tapahtuu <a href="http://capistranorb.com/">Capistranon</a> avulla, joka on osa <a href="https://github.com/digitoimistodude/dudestack" class="github">digitoimisto/dudestack</a>-kokonaisuutta. Ensimmäinen deploy suoritetaan aina Capistranon työkalulla, mutta esim. pienet teemapäivitykset hoidetaan suoralla sftp- tai rsync-yhteydellä.

Uusin deployconfig tuotantoon ja stagingiin löytyy Dropboxista, hakemistopolusta <b>Dude/Palvelin/Deployconfigs (latest)</b>.

<h3>Tarkistuslista</h3>

Ennen julkaisua ja julkaisun jälkeen käydään <u>aina</u> seuraava tarkistuslista huolellisesti läpi. Lista löytyy myös Dropboxista, kansiosta <b>Dude/Tärkeät asiakirjat/muut/Ennen julkaisua huomioitavaa.todo</b>, jota on ylläpidettävä samaan tahtiin kuin alla olevaa. Dokumentin voi myös kopioida projektikansioon ja ruksata SublimeTextin PlainTasks -packagea hyödyntämällä.

<h3>Ennen julkaisua</h3>

☐ WordPress Yleiset Asetukset
☐ Faviconit ja muut ikonit
☐ Testaa templatet läpi: haku, arkisto, avainsanat, ym.
☐ Google Analytics
☐ Tarvittavat 301 redirectit
☐ Bloggauksen muotoilut
☐ Formien testaus
☐ Katso ettei missään lue "Etusivu", perus SEO-asiat kuntoon
☐ screenshot.png
☐ style.css - teeman tiedot kuosiin
☐ Optimoi kuvat ImageOptimilla/Imagify (/media ja teeman kuvakansio)
☐ Lisää maksullisien lisäosien lisenssit paikalleen
☐ WordPress-päivitykset
☐ .htaccess Redirect 301 /asiakas http://www.asiakas.fi tai nginx-redirectit, jos on
☐ Jos sopii projektiin/sovittu/saittiuudistus: Screenshotteja Google-näkyvyyden tilanteesta ennen julkaisua (Firefoxin full-page screenshot-toiminto)
☐ Esteettömyystestaus päällisin puolin Chromen Alix-lisäosalla
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
☐ Let's Encrypt auto renew -scripti paikalleen (/etc/letsencrypt/con gs, /etc/bin/ josta renew-scriptin kopiointi uudelle sivustolle ja sitten <b>sudo crontab -e</b> johon entry)
☐ Nopeuden testaus <a href="http://developers.google.com/speed/pagespeed/insights/">PageSpeed Insightin</a> avulla
☐ Testaa nopeus <a href="https://tools.keycdn.com/speed">KeyCDN palvelulla</a>
☐ Formien testaus
☐ Sähköpostiliikenteen testaus (SendGrid)
☐ Päivitä urlit lisärillä, wp-clillä tai Go Live Update Urls -lisäosalla, tai SQL-versio <pre class="language-mysql"><code>update wp_posts set post_content = replace(post_content, 'https:\/\/asiakas.dude. \/PROJEKTINIMI_TÄHÄN', 'http:\/\/www.PROJEKTINIMI_TÄHÄN.com');</code></pre>
☐ Backupit päälle (muokkaa /etc/bin/backup.conf ja lisää uudelle riville sivustonnimi. , tietokannannimi)
☐ Asiakastyytyväisyyskysely (Typeform)
☐ Testaa Internet Exporer 11

<h3>Extraa</h3>

☐ "Toteutus: DUDE" footeriin, linkki ja lupa
☐ Testaa typografia blogissa, <a href="https://dudetest.xyz/air/wp/wp-admin/post.php?
post=1134&action=edit">kopioi mallipohja tästä</a>
☐ HTML:n validointi <a href="https://validator.w3.org/">W3 validaattorilla</a>
☐ Estä trace- ja pingbackien lähettäminen
☐ Testaa esteettömyys <a href="http://achecker.ca/checker/index.php">aCheckerillä</a>
☐ Mikroformaatit, schemat, ks. <a href="http://www.google.com/webmasters/tools/richsnippets">Google Rich Snippets</a>
☐ Käy pääpiirteittäin läpi <a href="http://webdevchecklist.com/">Webdev checklist</a>