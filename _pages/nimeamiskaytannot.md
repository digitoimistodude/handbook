---
ID: 443
post_title: Nimeämiskäytännöt
author: Roni
post_excerpt: ""
layout: page
permalink: >
  https://handbook.dude.fi/wordpress-kehitys/nimeamiskaytannot
published: true
post_date: 2019-08-12 15:33:33
---
Dude käyttää tyylipuolella (SCSS) <a href="https://smacss.com/">SMACSS (Scalable and Modular Architecture for CSS)</a> ja <a href="https://css-tricks.com/styling-the-gutenberg-columns-block/">WordPressin Gutenbergiin</a> pohjautuvaa nimeämiskäytäntöä. Moduuleja, eli ulkoasussa olevia rajattuja 100% leveitä alueita (<code>&lt;section&gt;</code>) kutsutaan nimellä <code>block</code>. Näiden sisällä ensimmäistä diviä kutsutaan nimellä <code>container</code>.

<h3>Tyypillinen HTML-rakenne</h3>

<pre class="language-html"><code>&lt;section class="block block-example"&gt;
  &lt;div class="container"&gt;
    &lt;div class="cols"&gt;
      &lt;div class="col col-text"&gt;
        &lt;p class="block-title-pre" aria-describedby="block-title-something"&gt;Some pre-heading&lt;/p&gt;
        &lt;h2 class="block-title" id="block-title-something"&gt;Some heading - Lorem ipsum&lt;/h2&gt;

        &lt;p&gt;Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla vel accumsan libero. Duis non erat in odio porta venenatis. Integer nibh nulla, mollis a eleifend a, laoreet ac eros. Aliquam venenatis at mauris non pellentesque. Interdum et malesuada fames ac ante ipsum primis in faucibus. Nulla condimentum elementum leo. Etiam viverra nec lectus eu bibendum.&lt;/p&gt;

        &lt;p&gt;Aenean ac ultrices metus. Donec pretium laoreet massa accumsan sodales. Integer non facilisis ante. Duis scelerisque ex nulla. Sed sed ligula ipsum. Fusce porttitor tincidunt finibus. Duis ut convallis elit. Curabitur viverra vehicula ante, sit amet dapibus urna dignissim in. Aliquam id molestie dolor, et sollicitudin arcu.&lt;/p&gt;
      &lt;/div&gt;

      &lt;div class="col col-image col-poster"&gt;
        &lt;img src="&lt;?php echo get_theme_file_uri('/images/placeholder.png'); ?&gt;" alt="Dynamic title" /&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/section&gt;
</code></pre>

<h3>Tyypillinen CSS-rakenne</h3>

<pre class="language-scss"><code>.block.block-example {
  // Default background-color
  background-color: $color-mudgreen;

  h1,
  h2,
  p {
    color: $color-white;
  }

  .block-title-pre {
    margin: 0 0 1rem;
  }

  .block-title {
    margin-top: 0;
  }

  .cols {
    display: flex;
    color: $color-white;
  }

  .col.col-text {
    @media (min-width: $some-breakpoint) {
      width: 50%;
      margin-right: 30%;
    }
  }

  .col.col-image {
    @media (min-width: $some-breakpoint) {
      width: calc(50% - 30%);
    }

    img {
      max-width: 395px;
      width: 100%;
      height: auto;
    }
  }
}</code></pre>

<h3>Taustakehitys</h3>

PHP-kehityksessä noudatetaan virallista <a href="https://make.wordpress.org/core/handbook/best-practices/coding-standards/php/">WordPress Coding Standardsia</a>, muutamia teemakehityksen (WPCS) poikkeuksia lukuunottamatta. Poikkeukset on määritelty <a href="https://github.com/digitoimistodude/air-light/blob/master/phpcs.xml" class="github">pohjateeman phpcs.xml-tiedostossa</a> ja vielä tarkennetusti projektikohtaisesti projektin oman teeman phpcs.xml:ssä.