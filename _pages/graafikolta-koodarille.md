---
ID: 204
post_title: Suunnittelijalta koodarille
author: Roni
post_excerpt: ""
layout: page
permalink: >
  https://handbook.dude.fi/wordpress-kehitys/graafikolta-koodarille
published: true
post_date: 2017-10-10 14:43:35
---
Kun suunnittelija on saanut visuaalisen suunnittelun päätökseen, tulee hänen toimittaa koodareille tarvittavat materiaalit.

<h3>Ulkoasut</h3>

Visuaalisen suunnittelijan on varmistettava, että uusin hyväksytty versio löytyy aina XD:stä (työkalusta lisää kohdassa <a href="https://handbook.dude.fi/tyoskenteleminen-dudella/tyokalut-workflow">Työkalut & Workflow</a>). XD prototyyppi on jaettava Specs -tilassa, jotta koodari voi tarkastella yksityiskohtaisesti ulkoasussa olevia elementtejä.

<h3>Valokuvat</h3>

Kuvat toimitetaan Adobe XD:n Specs -näkymän tai Zeplinin kautta ladattavina assetteina. Suunnittelijan on huolehdittava, että kaikki kuvat ovat ladattavissa. Kuvat ovat valmiiksi leikattuja ja syvättyjä. CSS-koodeja yms. ei tarvitse, assetit riittää.

<h3>Fontit</h3>

Emme käytä Adobe/Typekit/Google -upotuksia, vaan fontit olisi hyvä olla tiedostoina paremman toimivuuden, hallinnan ja latausnopeuksien vuoksi, näin säästymme ylimääräiseltä ulkoiselta HTTP-kutsulta. 

Paikallisilla fonteilla varaudumme myös, että sivusto toimii ilman JS:ää eikä Adblockerit tai muut tietoturvatyökalut blokkaa fonttien latautumista. Jos muita webfonttimuotoja ei ole saatavilla, .ttf riittää.

<h3>Logo sekä kuvakkeet</h3>

Logoista ja kuvakkeista tarvitaan taittoa varten <strong>SVG</strong>-versiot, jotta sivustolle saadaan retinaa tukeva moderni versio, joka näkyy joka laitteella terävästi. Logot ja kuvakkeet toimitetaan Adobe XD:n Specs -näkymässä.

Joissain tapauksissa logot tai kuvakkeet voidaan toimittaa suoraan koodarille. Tällöin ne tulee tallentaa Illustratorissa käyttäen <code>Presentation attributes</code> -asetusta, jolloin SVG-tiedostoon ei tule ylimääräisiä inline style-määritteitä. Filleinä tai strokeina tulee olla currentColor-arvo hexan sijaan, näin väri saadaan määriteltyä koodeitse helpommin.

Tarvittaessa, monimutkaisempien SVG-kuvakkeiden kohdalla voidaan käyttää style-attributes-määrityksiä, mutta nämä varmistellaan aina erikseen.
