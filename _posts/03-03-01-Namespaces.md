---
title:   Imenski prostori
isChild: true
anchor: namespaces
---

## Imenski prostori - Namespaces {#namespaces_title}

Kot zgoraj omenjeno, ima PHP skupnost veliko razvijalcev, ki ustvarijo ogromno kode. To pomeni, da
določena PHP koda knjižnice lahko uporabi enako ime razreda kot druga knjižnica. Ko sta obe knjižnici uporabljeni
v istem imenskem prostoru, lahko sovpadajo in povzročajo težave.

_Imenski prostori_ rešujejo ta problem. Kot je opisano v PHP referenčnem priročniku, lahko primerjamo imenske prostore
z direktoriji operacijskega sistema, ki _poimenujejo prostor_ datotek; dve datoteki z enakim imenom lahko obstajata v
različnih direktorijih. Enako lahko tudi dva PHP razreda z enakim imenom obstajata v različnih PHP
imenskih prostorih. Tako enostavno je.

Pomembno je, da vašo kodo prostorsko poimenujete, da je lahko uporabljena s strani drugih razvijalcev brez strahu
pred sovpadanjem z drugimi knjižnicami.

Ena izmed priporočenih poti za uporabo imenskih prostorov je poudarjena v [PSR-0][psr0], ki cilja ponujati standardizirano konvencijo za datoteke,
razrede in imenske prostore, da omogoča plug-in-play kodo.

V decembru 2013 je PHP-FIG ustvaril nov standard za avtomatsko nalaganje: [PSR-4][psr4], ki bo nekega dne
verjetno zamenjal PSR-0. Trenutno sta oba še vedno v uporabi, saj PSR-4 potrebuje PHP 5.3 in mnogi samo PHP 5.2
projekti imajo trenutno implementiran PSR-0. Če nameravate uporabiti standard za avtomatsko nalaganje za novo aplikacijo ali
paket potem vsekakor želite preveriti PSR-4.

* [Preberite o imenskih prostorih][namespaces]
* [Preberite o PSR-0][psr0]
* [Preberite o PSR-4][psr4]

[namespaces]: http://php.net/language.namespaces
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
