---
ID: 401
post_title: Made by Dude -badge
author: Roni
post_excerpt: ""
layout: page
permalink: >
  http://handbook.dude.fi/made-by-dude-badge
published: true
post_date: 2019-04-03 14:30:30
---
Sivujen tekijästä ilmoittaa <b>Made by Dude</b> -badge, joka lisätään asiakkaan suostumuksesta sivuston Footer-osioon. Tämä sivu sisältää badgen käyttöönottoon vaadittavat universaalit snippetit, joita ei ole sisällytetty <a href="https://github.com/digitoimistodude/air-light" class="github">starter-teemaamme</a> mukaan.

<strong>footer.php:</strong>

<pre class="language-html"><code>&lt;p class="made-by-dude"&gt;&lt;a href="https://www.dude.fi" data-tooltip="Sivut toteuttanut"&gt;&lt;svg xmlns="http://www.w3.org/2000/svg" width="35" height="9" fill="#fff" viewBox="0 0 10000 2602"&gt;&lt;path d="M0 1283.5V2567h379.3c361.6 0 417.8-.4 471.2-3 297.1-14.7 539.8-79.9 736.3-197.7 137.3-82.3 249.7-188.7 335.8-317.9 27.5-41.2 44.5-70.8 68.3-118.4 75.2-151.1 119.6-326.1 133.6-527.5 3.1-45.2 3.7-61.5 4.2-123 .7-76.5-.6-115.2-5.7-177-26.5-317.7-137.8-572.7-333.3-763.2C1612.5 166.7 1379.5 59.9 1091 19.1c-57.4-8.2-103.1-12.4-186.5-17.3C890 1 763.8.6 442.3.3L0-.1v1283.6zm905.5-835.6c46.1 3.5 75.3 7 108.5 12.7 121.1 20.8 225.1 65.8 305.5 132.3 94.5 78.2 161.8 187.5 201.4 327.4 19.4 68.3 32.3 144.5 38.6 227.2 5.6 73.8 5.9 162.8.9 236-14.5 212.8-72.3 379.7-172.7 499.5-113.3 135.1-280.3 211.6-501.7 229.9-44.8 3.7-63.6 4.1-204.2 4.1H544V445.9l173.3.4c119 .3 177.9.8 188.2 1.6zm1738.8 411.8c.2 661.6.6 863.3 1.5 874.8 5.3 65.2 9.5 98.9 17.8 143.5 26.2 139.6 80.9 265.1 160.8 368.5 23.3 30.3 39.9 48.9 70 79.1 34.1 34 55.7 52.8 91.1 79.2 176.1 131.3 410 197.2 700.5 197.2 191.2 0 359.2-28.7 505.5-86.5 176.1-69.4 314.3-177.5 408.6-319.5 80.4-120.9 128.4-259.5 144.4-416 5.3-52.7 4.9 18.4 5.2-918.3L4750 0h-542v795.2c0 771.6-.2 820.4-3 860.8-11.6 165.1-54.9 285.6-131 364.3-71.6 74.1-177.2 114.9-320.5 123.7-21.8 1.3-85.9 1.4-108 0-167.6-10.1-282.2-60.2-353.7-154.6-58.6-77.4-92.7-186.9-102.8-330.4-2.8-39.9-3-92.7-3-863.8V0h-542l.3 859.7zM5271 1283.5V2567h379.3c360.8 0 418.1-.4 470.7-3 235.2-11.7 434.6-54.5 606.4-130.2 23.5-10.3 75.6-36.1 96.6-47.9 169-94.1 300.8-220.6 396.8-380.5 102.2-170.3 160.5-375.7 175.6-618.9 3-47.8 3.9-86.9 3.3-147.5-.6-58.1-1.1-71.3-4.2-116.5-24.1-341.6-147.3-615.5-364.7-811.2C6822.4 123.8 6546.2 22 6194 3c-50.1-2.7-97.9-3-501.2-3H5271v1283.5zM6155 447c29.4 1.3 55.4 3.4 81.9 6.6 284.5 33.8 467.9 183.1 549.2 447.2 32.5 105.5 48.9 230.8 48.9 372.2-.1 147.3-18.3 276.4-54.5 385.5-29.4 88.3-70.4 163.5-124.3 227.5-14 16.6-52.5 54.9-68.7 68.4-119.2 99.1-274.1 151.7-476 161.6-12.1.6-78.8 1-158.7 1H5815V446h158.8c90.8 0 168.3.5 181.2 1zm1756-172.5V544h2089V5H7911v269.5zm0 1010V1554h2089v-539H7911v269.5zm0 1013V2567h2089v-539H7911v269.5z"/&gt;&lt;/svg&gt;&lt;/a&gt;&lt;/p&gt;</code></pre>

<strong>sass/extra/_made-by-dude.scss:</strong>

<pre class="language-scss"><code>.made-by-dude {
  position: absolute;
  right: 2rem;

  svg {
    opacity: .5;
    transition: opacity .55s;
  }

  &:hover svg {
    opacity: 1;
  }
}

[data-tooltip] {
  position: relative;
  cursor: pointer;
}

[data-tooltip]:after {
  opacity: 0;
  pointer-events: none;
  transition: all .18s ease-out .18s;
  font-family: sans-serif !important;
  font-weight: normal !important;
  font-style: normal !important;
  text-shadow: none !important;
  font-size: 12px !important;
  background: rgba(17, 17, 17, .9);
  border-radius: 4px;
  color: #fff;
  content: attr(data-tooltip);
  padding: 5px;
  position: absolute;
  z-index: 10;
  bottom: 100%;
  left: 50%;
  margin-bottom: 11px;
  transform: translate(-50%, 10px);
  transform-origin: top;
  width: 105px;
  text-align: center;
}

[data-tooltip]:before {
  background: no-repeat url('data:image/svg+xml;charset=utf-8, %3Csvg%20xmlns%3D%22http://www.w3.org/2000/svg%22%20width%3D%2236px%22%20height%3D%2212px%22%3E%3Cpath%20fill%3D%22rgba(17, 17, 17, .9)%22%20transform%3D%22rotate(0)%22%20d%3D%22M2.658, .000%20C-13.615, .000%2050.938, .000%2034.662, .000%20C28.662, .000%2023.035, 12.002%2018.660, 12.002%20C14.285, 12.002%208.594, .000%202.658, .000%20Z%22/%3E%3C/svg%3E');
  background-size: 100% auto;
  width: 18px;
  height: 6px;
  opacity: 0;
  pointer-events: none;
  transition: all .18s ease-out .18s;
  content: '';
  position: absolute;
  z-index: 10;
  bottom: 100%;
  left: 50%;
  margin-bottom: 5px;
  transform: translate(-50%, 10px);
  transform-origin: top;
}

[data-tooltip]:hover:before,
[data-tooltip]:hover:after,
[data-tooltip][data-tooltip-visible]:before,
[data-tooltip][data-tooltip-visible]:after {
  opacity: 1;
  pointer-events: auto;
}

[data-tooltip]:hover:after,
[data-tooltip][data-tooltip-visible]:after {
  transform: translate(-50%, 0);
}

[data-tooltip]:hover:before,
[data-tooltip][data-tooltip-visible]:before {
  transform: translate(-50%, 0);
}</code></pre>