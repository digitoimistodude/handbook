---
ID: 690
post_title: Kehittäjälle
author: Roni
post_excerpt: ""
layout: page
permalink: >
  https://handbook.dude.fi/tyoskenteleminen-dudella/kehittajalle
published: true
post_date: 2021-01-20 13:30:08
---
<!-- wp:paragraph -->
<p>Kun kohdan <a href="https://handbook.dude.fi/tyoskenteleminen-dudella/aloittaminen">Aloittaminen</a> yleiset tunnukset on luotu ja otettu käyttöön, luodaan tunnukset seuraaviin palveluihin:</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li><a href="https://github.com">GitHub</a>-tunnus</li><li><a href="https://github.com/digitoimistodude">GitHub Teamin</a> owner-oikeudet</li><li><a href="https://www.cacher.io">Cacher</a></li></ol>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>Asennettavat ohjelmat koodarille</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Tärkeimmistä ohjelmista on avattu lisää osiossa <a href="https://handbook.dude.fi/tyoskenteleminen-dudella/tyokalut-workflow">Työkalut &amp; Workflow</a>. Asenna kuitenkin seuraavat (MacOS päivitysten jälkeen):</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><a href="https://itunes.apple.com/fi/app/xcode/id497799835?mt=12">XCode</a></li><li><a href="https://brew.sh/index_fi">Homebrew</a></li><li><a href="https://www.firefox.com">Firefox</a></li><li><a href="https://www.google.com/chrome/">Google Chrome</a></li><li><a href="https://code.visualstudio.com/">Visual Studio Code</a></li><li><a href="https://www.resilio.com/individuals/">Resilio Sync</a></li><li><a href="https://sequelpro.com/test-builds">Sequel Pro (Nightly Test Build)</a></li><li><a href="https://simplenote.com/">Simplenote</a></li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>Työntekoon vaaditut komentorivikomponentit</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Terminal -komentorivitulkin selkeyttämiseksi suositellaan <a href="https://draculatheme.com/terminal/">Dracula-teemaa</a> ja <a href="https://sourcefoundry.org/hack/">Hack-fonttia</a> (12pt). Nämä saa asennettua <a href="https://draculatheme.com/terminal/">Dracula Themen ohjeiden</a> mukaisesti.

<p>1. Vaihdetaan macOs Catalinan zsh term bashiksi ja poistetaan zsh:sta nalkuttava viesti:</p>

<pre class="language-bash"><code class="language-bash">chsh -s /bin/bash</code></pre>

<p>Lisätään vaaditut tiedostot:</p>

<pre class="language-bash"><code class="language-bash">touch ~/.aliases && touch ~/.aliases_private</code></pre>

<p>Käynnistä tässä kohtaa terminal uudestaan tappamalla se näppäinyhdistelmällä <kbd><kbd>⌘ cmd</kbd> <span>+</span> <kbd>Q</kbd></kbd> ja avaamalla uudestaan. Seuraavaksi luodaan .bash_profile-tiedosto seuraavasti:</p>

<pre class="language-bash"><code class="language-bash">nano ~/.bash_profile</code></pre>

<p>Lisää tiedostoon copy-pastettamalla seuraava:</p>

<pre class="language-bash"><code class="language-bash"># Silence Catalina zsh notification<br />
export BASH_SILENCE_DEPRECATION_WARNING=1<br /><br />

# Editor<br />
export EDITOR=nano<br /><br />

# Title bar - "user@host: ~"<br />
title="\u@\h: \w"<br />
titlebar="\[\033]0;"$title"\007\]"<br /><br />

# Define colors<br />
black="\[$(tput setaf 0)\]"<br />
red="\[$(tput setaf 1)\]"<br />
green="\[$(tput setaf 2)\]"<br />
yellow="\[$(tput setaf 3)\]"<br />
blue="\[$(tput setaf 4)\]"<br />
magenta="\[$(tput setaf 5)\]"<br />
cyan="\[$(tput setaf 6)\]"<br />
white="\[$(tput setaf 7)\]"<br />

# Git branch<br />
git_branch() {<br />
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)\ /';<br />
}<br /><br />

# Clear attributes<br />
clear_attributes="\[$(tput sgr0)\]"<br /><br />

# Dracula bash prompt for regular user - "➜  ~ (master) "<br />
export PS1="${titlebar}${green}\h ${blue}\W ${cyan}\$(git_branch)${clear_attributes}"<br /><br />

# Autocorrect typos in path names when using `cd`<br />
shopt -s cdspell;<br /><br />

# Add tab completion for many Bash commands<br />
if which brew > /dev/null && [ -f "$(brew --prefix)/share/bash-completion/bash_completion" ]; then<br />
    source "$(brew --prefix)/share/bash-completion/bash_completion";<br />
elif [ -f /etc/bash_completion ]; then<br />
    source /etc/bash_completion;<br />
fi;<br /><br />

# Load other dotfiles<br />
source $HOME/.aliases_private<br />
source $HOME/.aliases<br /><br />

PATH="$HOME/.composer/vendor/bin:$PATH"<br /></code></pre>

Tallennus <kbd><kbd>ctrl</kbd> <span>+</span> <kbd>O</kbd></kbd>, nanosta poistuminen <kbd><kbd>ctrl</kbd> <span>+</span> <kbd>X</kbd></kbd>.

<p>2. Xcoden komponentit (saattaa olla jo asennettuna, mutta varmistetaan ensin):</p>

<pre class="language-bash"><code class="language-bash">xcode-select --install</code></pre>

<p>3. Homebrewn päivitykset:</p>

Jos ei ole vielä asennettu <a href="https://brew.sh/index_fi">brew.sh</a> sivuston komennon kautta, ensin asennus ja sitten päivitykset komennolla:

<pre class="language-bash"><code class="language-bash">brew update</code></pre>

<p>4. Node ja npm:</p>

<pre class="language-bash"><code class="language-bash">brew install nodejs</code></pre>

Ja testaus:

<pre class="language-bash"><code class="language-bash">npm -v && node -v</code></pre>

<p>5. Disabloidaan automaattinen salasanakysely komentorivillä:</p>

<pre class="language-bash"><code class="language-bash">sudo nano /etc/sudoers</code></pre>

Lisätään alimmaiseksi:

<pre class="language-bash"><code class="language-bash"># root and users in group wheel can run anything on any machine as any user<br />
root            ALL = (ALL) ALL<br />
%admin          ALL = (ALL) NOPASSWD: ALL</code></pre>

<p>Tallennus <kbd><kbd>ctrl</kbd> <span>+</span> <kbd>O</kbd></kbd>, nanosta poistuminen <kbd><kbd>ctrl</kbd> <span>+</span> <kbd>X</kbd></kbd>.</p>

<p>6. Composerin asennus <a href="https://getcomposer.org/download/">sivustolla listattujen</a> komentojen kautta eli seuraavasti:</p>

<pre class="language-bash"><code class="language-bash">php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"<br />
php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"<br />
php composer-setup.php<br />
php -r "unlink('composer-setup.php');"<br />
sudo mv composer.phar /usr/local/bin/composer</code></pre>

Testaus:

<pre class="language-bash"><code class="language-bash">composer --version</code></pre>

<p>7. Gulpin asentaminen globaaliksi paketiksi:</p>

<pre class="language-bash"><code class="language-bash">npm install gulp -g</code></pre>

<p>8. Capistranon asentaminen globaaliksi paketiksi:</p>

<pre class="language-bash"><code class="language-bash">sudo gem install capistrano</code></pre>

<p>9. PHPCodeSnifferin asennus WordPress Coding Standardeilla ja toiminnan testaus (ohjeet myös <a href="https://github.com/digitoimistodude/air-light#how-to-install-for-gulp" class="github">air-light</a> repossa):</p>

<pre class="language-bash"><code class="language-bash">mkdir -p ~/Projects && cd ~/Projects && git clone -b master --depth 1 https://github.com/squizlabs/PHP_CodeSniffer.git phpcs<br />
git clone -b master https://github.com/PHPCompatibility/PHPCompatibility<br />
git clone -b master --depth 1 https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards.git wpcs</code></pre>

<p>Korvaa <i>omanimi</i> omalla järjestelmän käyttäjänimellä:</p>

<pre class="language-bash"><code class="language-bash">sudo ln -s /Users/<b>omanimi</b>/Projects/phpcs/bin/phpcs /usr/local/bin/phpcs && sudo chmod +x /usr/local/bin/phpcs</code></pre>

<p>Korvaa <i>omanimi</i> omalla järjestelmän käyttäjänimellä:</p>

<pre class="language-bash"><code class="language-bash">phpcs --config-set installed_paths "/Users/<b>omanimi</b>/Projects/wpcs","/Users/<b>omanimi</b>/Projects/PHPCompatibility"</code></pre>

<p>Testaa:</p>

<pre class="language-bash"><code class="language-bash">phpcs -i</code></pre>

<p>Pitäisi näkyä:</p>

<pre class="language-bash"><code class="language-bash">The installed coding standards are PEAR, Zend, PSR2, MySource, Squiz, PSR1, PSR12, PHPCompatibility, WordPress, WordPress-Extra, WordPress-Docs and WordPress-Core</code></pre>

<p>10. Stylelintin ja eslintin asennus:</p>

<pre class="language-bash"><code class="language-bash">npm i stylelint eslint -g</code></pre>

<p>Testaus:</p>

<pre class="language-bash"><code class="language-bash">stylelint -v && eslint -v</code></pre>

<p>Jos tulee versiot, asennus on mennyt oikein läpi.</p>

<p>11. <a href="https://code.visualstudio.com/">Visual Studio Coden</a> teemat, fontit ja värit saat asettaa oman makusi mukaan, mutta jos preferenssiä ei ole, voit käyttää <a href="https://github.com/ronilaukkarinen/vscode-settings" class="github">vscode-settings</a> repon asetuksia. <a href="https://github.com/ronilaukkarinen/vscode-settings#usage">Suora linkki asentamisohjeisiin</a>.</p>

<p>12. Paikallisen kehitysympäristön asentaminen onnistuu noudattamalla <a href="https://github.com/digitoimistodude/macos-lemp-setup#installation-steps" class="github">macos-lemp-setup</a> -asennusohjeita. <b>Huom!</b> nginx, php-fpm on ajettava roottina sudo-komennon kanssa, mutta mariadb on ajettava käyttäjän alla.</p>

<p>13. Projektikehitysstackin asentaminen onnistuu noudattamalla <a href="https://github.com/digitoimistodude/dudestack#installation" class="github">dudestack</a> -asennusohjeita.</p>
<!-- /wp:paragraph -->