---
ID: 401
post_title: Made by Dude -badge
author: Roni
post_excerpt: ""
layout: page
permalink: >
  http://handbook.dude.fi/wordpress-kehitys/made-by-dude-badge
published: true
post_date: 2019-04-03 14:30:30
---
Sivujen tekijästä ilmoittaa <b>Made by Dude</b> -badge, joka lisätään asiakkaan suostumuksesta sivuston Footer-osioon. Tämä sivu sisältää badgen käyttöönottoon vaadittavat universaalit snippetit, joita ei ole sisällytetty <a class="github" href="https://github.com/digitoimistodude/air-light">starter-teemaamme</a> mukaan.

<iframe style="display: block !important; max-width: 1140px !important;" src="https://player.vimeo.com/video/464931937?background=1" width="1140" height="710" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

<iframe style="display: block !important; max-width: 1140px !important;" src="https://player.vimeo.com/video/464931911?background=1" width="1140" height="710" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

<strong>Lisää ennen footer.php-tiedoston containerin lopetustagia:</strong>
<pre class="language-html"><code>&lt;p class="dude-badge"&gt;&lt;a class="no-external-link-indicator" href="https://www.dude.fi" data-tooltip="Sivut toteuttanut" aria-label="Sivut toteuttanut Digitoimisto Dude Oy"&gt;&lt;svg aria-hidden="true" class="tip" xmlns="http://www.w3.org/2000/svg" width="36" height="12" viewBox="0 0 36 12"&gt;&lt;path class="tip-color" transform="rotate(0)" d="M2.658, .000 C-13.615, .000 50.938, .000 34.662, .000 C28.662, .000 23.035, 12.002 18.660, 12.002 C14.285, 12.002 8.594, .000 2.658, .000 Z"&gt;&lt;/path&gt;&lt;/svg&gt;&lt;svg width="85" height="17" xmlns="https://www.w3.org/2000/svg" viewBox="0 0 85 17"&gt;&lt;g fill="transparent" class="heart" fill-rule="evenodd"&gt;&lt;path d="M7.5 13.963L2.192 8.412a3.152 3.152 0 01-.59-3.634h0a3.166 3.166 0 012.312-1.7 3.133 3.133 0 012.72.882l.866.803.867-.803a3.133 3.133 0 012.718-.882 3.167 3.167 0 012.312 1.7h0a3.153 3.153 0 01-.589 3.634L7.5 13.962z" class="stroke" stroke="#03061b" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"/&gt;&lt;path class="fill" fill="#03061b" d="M50.696 8.166c0 .943-.338 2.782-2.601 2.782-2.278 0-2.618-1.84-2.618-2.782V3h-4.34v5.455c0 3.472 2.6 5.545 6.958 5.545 4.346 0 6.942-2.073 6.942-5.545V3h-4.34v5.166zM85 6.052V3H71.717v11H85v-3.052h-9.073v-1.22h7.543V7.271h-7.543V6.052zM33.14 10.948h-2.894V6.057h2.895c1.498 0 2.543 1.146 2.543 2.443 0 1.314-1.045 2.448-2.543 2.448zM34.179 3H26v11h8.178c2.832 0 5.723-2.196 5.723-5.5 0-3.324-2.891-5.5-5.723-5.5zM63.722 10.948h-2.895V6.057h2.895c1.499 0 2.543 1.146 2.543 2.443 0 1.314-1.044 2.448-2.543 2.448zM64.76 3h-8.178v11h8.178c2.832 0 5.723-2.196 5.723-5.5 0-3.324-2.891-5.5-5.723-5.5z"/&gt;&lt;/g&gt;&lt;/svg&gt;&lt;/a&gt;&lt;/p&gt;</code></pre>

<strong>Uusi tiedosto: sass/layout/_dude-badge.scss:</strong>

<pre class="language-scss"><code>// Badge variables
$badge-transition-speed: .1s;
$color-badge-logo-dark: #03061b;
$color-badge-logo-light: $color-white;
$color-badge-tooltip-text-dark: $color-white;
$color-badge-tooltip-text-light: #03061b;
$color-badge-tooltip-background-light: rgba(255, 255, 255, .8);
$color-badge-tooltip-background-dark: rgba(17, 17, 17, .9);

// Light or dark?
$color-badge-logo: $color-badge-logo-dark;
$color-badge-tooltip-text: $color-badge-tooltip-text-dark;
$color-badge-tooltip-background: $color-badge-tooltip-background-dark;

.site-footer .container {
  position: relative;
}

.dude-badge {
  text-align: center;
  margin: 0;

  @media (min-width: 480px) {
    position: absolute;
    right: 2rem;

    // Adjust based on the site
    margin-top: 0;
  }

  a:hover .heart {
    fill: $color-badge-logo;
  }

  .fill {
    fill: $color-badge-logo;
  }

  .stroke {
    stroke: $color-badge-logo;
  }
}

[data-tooltip] {
  position: relative;
  cursor: pointer;
  transform: translate(-50%, 15px);
  transition: all $badge-transition-speed ease-out $badge-transition-speed;
  transform-origin: top;
}

[data-tooltip]::after {
  opacity: 0;
  pointer-events: none;
  transition: all $badge-transition-speed ease-out $badge-transition-speed;
  font-family: sans-serif !important;
  font-weight: normal !important;
  font-style: normal !important;
  text-shadow: none !important;
  font-size: 12px !important;
  background: $color-badge-tooltip-background;
  border-radius: 4px;
  color: $color-badge-tooltip-text;
  content: attr(data-tooltip);
  padding: 5px;
  position: absolute;
  z-index: 10;
  bottom: 100%;
  left: 50%;
  margin-bottom: 11px;
  transform: translate(-50%, 10px);
  transform-origin: top;
  width: 100px;
  text-align: center;
}

[data-tooltip] .tip {
  width: 18px;
  height: 6px;
  opacity: 0;
  pointer-events: none;
  transition: all $badge-transition-speed ease-out $badge-transition-speed;
  content: '';
  position: absolute;
  z-index: 10;
  bottom: 100%;
  left: 50%;
  margin-bottom: 10px;
  transform: translate(-50%, 15px);
  transform-origin: top;

  .tip-color {
    fill: $color-badge-tooltip-background;
  }
}

[data-tooltip]:hover .tip,
[data-tooltip]:hover::after,
[data-tooltip][data-tooltip-visible] .tip,
[data-tooltip][data-tooltip-visible]::after {
  opacity: 1;
  pointer-events: auto;
}

[data-tooltip]:hover::after,
[data-tooltip][data-tooltip-visible]::after {
  transform: translate(-50%, -5px);
}

[data-tooltip]:hover .tip,
[data-tooltip][data-tooltip-visible] .tip {
  transform: translate(-50%, 0);
}</code></pre>
<strong>global.scss:</strong>
<pre class="language-scss"><code>@import '../layout/dude-badge';</code></pre>