---
title:   Vodič kodnega stila
isChild: false
anchor:  code_style_guide
---

# Vodič kodnega stila {#code_style_guide_title}

PHP skupnost je velika in raznolika ter sestavljena iz številnih knjižnic, ogrodij in komponent. Za PHP razvijalce je
običajno, da izbirajo med mnogimi od le teh in jih kombinirajo v določenem projektu. Pomembno je, da se PHP koda oprijema
(kolikor je le mogoče) skupnega stila kodiranja, saj omogoča za razvijalce enostavnejše mešanje in ujemanje različnih
knjižnic za njihove projekte.

[Framework Interop Group][fig] so predlagali in odobrili serijo stilskih priporočil. Vsa niso vezana na kodne stile, vendar
tista ki so, so [PSR-0][psr0], [PSR-1][psr1], [PSR-2][psr2] in [PSR-4][psr4]. Ta priporočila so samo
skupek pravil, ki jih določeni projekti, kot so Drupal, Zend, Symfony, CakePHP, phpBB, AWS SDK, FuelPHP, Lithium itd.
pričenjajo privzemati. Lahko jih uporabite v vaših projektih, ali nadaljujete z uporabo vaših osebnih stilov.

Idealno bi morali pisati PHP kodo, ki se oprijema znanih standardov. To je lahko kakršnakoli kombinacija PSR-jev, ali
enega izmed kodnih standardov izdelanih s strani PEAR ali Zend. To pomeni, da ostali razvijalci lahko enostavno berejo
in delajo z vašo kodo ter aplikacije, ki implementirajo komponente, imajo lahko konsistentnost celo, ko se uporablja veliko
tretje osebne kode.

* [Preberite o PSR-0][psr0]
* [Preberite o PSR-1][psr1]
* [Preberite o PSR-2][psr2]
* [Preberite o PSR-4][psr4]
* [Preberite o PEAR kodnih standardih][pear-cs]
* [Preberite o Symfony kodnih standardih][symfony-cs]

Lahko uporabite [PHP_CodeSniffer][phpcs], da preverite kodo proti katerimkoli izmed teh priporočil in vtičnike za tekstovne
urejevalnike, kot je [Sublime Text][st-cs], ki nudi odziv v realnem času.

Postavitev kode lahko popravite avtomatično z uporabo enega izmed sledečih orodij:

- Eno je [PHP Coding Standards Fixer][phpcsfixer], ki ima zelo dobro testirano osnovo kode.
- Ter lahko se uporabi tudi orodje [PHP Code Beautifier and Fixer][phpcbf], ki je vključeno v PHP_CodeSniffer, da ustrezno prilagodite vašo kodo.

In PHP_CodeSniffer lahko poženete ročno v terminalu:

    phpcs -sw --standard=PSR2 file.php

Prikazal bo napake in opisal, kako jih popraviti.
Lahko je tudi v pomoč pri vključevanju tega ukaza v git hook.
Na ta način se vej, ki vsebujejo kršitve izbranega standards, ne more vnesti v repozitorij dokler se teh
kršitev ne odpravi.

Če imate PHP_CodeSniffer, lahko sporočene težave postavitve kode avtomatsko popravite s
[PHP Code Beautifier and Fixer][phpcbf].

    phpcbf -w --standard=PSR2 file.php

Druga opcija je uporaba orodja [PHP Coding Standards Fixer][phpcsfixer].
Prikazal bo, katere vrste napak je imela struktura kode pred popravki.

    php-cs-fixer fix -v --level=psr2 file.php

Angleščina je priporočljiva za vsa imena simbolov in infrastruktur kode. Komentarji so lahko napisani v kateremkoli jeziku,
ki ga lahko enostavno preberejo vse trenutne in bodoče strani, ki bodo delale s kodo.


[fig]: http://www.php-fig.org/
[psr0]: http://www.php-fig.org/psr/psr-0/
[psr1]: http://www.php-fig.org/psr/psr-1/
[psr2]: http://www.php-fig.org/psr/psr-2/
[psr4]: http://www.php-fig.org/psr/psr-4/
[pear-cs]: http://pear.php.net/manual/en/standards.php
[symfony-cs]: http://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[phpcbf]: https://github.com/squizlabs/PHP_CodeSniffer/wiki/Fixing-Errors-Automatically
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/
