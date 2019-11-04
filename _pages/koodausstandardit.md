---
ID: 90
post_title: Koodausstandardit
author: Roni
post_excerpt: ""
layout: page
permalink: >
  https://handbook.dude.fi/wordpress-kehitys/koodausstandardit
published: true
post_date: 2017-08-04 15:01:29
---
Dude käyttää <a href="https://github.com/squizlabs/PHP_CodeSniffer" class="github">squizlabs/PHP_CodeSniffer</a>in WordPress-standardeja taustatekniikoiden sekä teemojen kehityksessä ja <a href="https://github.com/Automattic/_s" class="github">Automattic/_s</a> standardia frontend-kehityksessä. WordPress VIP -sääntöjä emme noudata ja osa WordPress-säännöistä on excludettu hyvin perustein.

<a href="https://github.com/digitoimistodude/air" class="github">digitoimistodude/air</a>-pohjateeman kehityksessä suositaan underscoresin tapaa tehdä asioita. Automaattiset testit ajetaan <a href="https://travis-ci.org/digitoimistodude/air">Travisilla</a>.

<h3>phpcs.xml</h3>

Excludettavia sääntöjä voi ehdottaa lisää, mutta ehdotuksen pitää olla perusteltavissa. Sääntöihin voi tehdä Pull Requesteja tai committeja suoraan <a href="https://github.com/digitoimistodude/air" class="github">digitoimistodude/air</a>-repositorion <a href="https://github.com/digitoimistodude/air/blob/master/phpcs.xml" class="github">phpcs.xml</a> -tiedostoon.

<h3>PHP Code Beautifier and Fixer (phpcbf)</h3>

Phpcbf:llä on nopea refaktoroida koodia. Teemakansiossa komento ajetaan seuraavasti:

<pre class="language-bash"><code>phpcbf --standard=phpcs.xml page.php</code></pre>

<h3>Indentointi ja linttaus</h3>
Koodin tulee olla selkeää ja dokumentoitua. Indentaatiossa käytämme 2 merkin väliä.

PHP-puolella tulee aina noudattaa phpcs.xml:ää. Jos tarvitsee ignorata sääntöjä, lisätään ne projektikohtaisesti kunkin projektin teemakansion alla olevaan phpcs.xml:ään tai seuraavasti koodiin:

<pre class="language-php"><code>&lt;?php // phpcs:disable ?&gt;</code></pre>

Jos taas ignorettavaa on SCSS-puolella, lisää seuraava ignorettavaa riviä ennen:

<pre class="language-scss"><code>// scss-lint:disable</code></pre>

Disabloinnille/ignoroinnille pitää aina olla hyvä syy, lähtökohtaisesti varoitukset korjataan aina.

<h3>Editorin linter</h3>

Sublime Textille linter-asetukset ja exclude löytyvät GitHubista: <a href="https://github.com/digitoimistodude/sublime-settings/blob/master/Library/Application%20Support/Sublime%20Text%203/Packages/User/SublimeLinter.sublime-settings" class="github">SublimeLinter.sublime-settings</a>.