---
isChild: true
---

## Imenski prostori - Namespaces {#namespaces_title}

Kot zgoraj omenjeno, ima PHP skupnost veliko razijalcev, ki ustvarijo ogromno kode. To pomeni, da določena PHP koda knjižnice lahko uporabi enako ime razreda kot druga knjižnica. Ko sta obe knjižnici uporabljeni v istem imenskem prostoru, lahko sovpadajo in povzročajo težave.

_Imenski prostori_ rešujejo ta problem. Kot je opisano v PHP referenčnem priročniku, lahko primerjamo imenske prostore z direktoriji operacijskega sistema, ki _poimenujejo prostor_ datotek; dve datoteki z enakim imenom lahko obstajata v različnih direktorijih. Enako lahko tudi dva PHP razreda z enakim imenom obstajata v različnih PHP imenskih prostorih. Tako enostavno.

Pomembno je, da vašo kodo prostorsko poimenujete, da je lahko uporabljena s strani drugih razvijalcev brez strahu pred sovpadanjem z drugimi knjižnicami.

Ena izmed priporočenih poti za uporabo imenskih prostorov je povdarjena v [PSR-0][psr0], ki cilja ponujati standardizirano koncencijo za datoteke, razrede in imenske prostore, da omogoča plug-in-play kodo.

* [Preberite o imenskih prostorih][namespaces]
* [Preberite o PSR-0][psr0]

[namespaces]: http://php.net/manual/en/language.namespaces.php
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
