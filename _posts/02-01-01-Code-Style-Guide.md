---
title:   Vodič kodnega stila
isChild: false
anchor: code_style_guide
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
* [Preberite o Zend kodnih standardih][zend-cs]
* [Preberite o Symfony kodnih standardih][symfony-cs]

Lahko uporabite [PHP_CodeSniffer][phpcs], da preverite kodo proti katerimkoli izmed teh priporočil in vtičnike za tekstovne
urejevalnike, kot je [Sublime Text 2][st-cs], ki nudi realnočasovni odziv.

Postavitev kode lahko popravite avtomatsko z uporabo enega izmed dveh orodij. Eno je Fabien Potencier-jev
[popravljalnik PHP kodnih standardov][phpcsfixer], ki ima zelo dobro testirano kodno bazo. Je večji in in počasnejši, vendar zelo stabilen
in uporabljen v nekaterih večjih projektih kot sta Magento in Symfony. Druga opcija je [php.tools][phptools], ki je popularen
s strani vtičnika urejevalnika [sublime-phpfmt][sublime-phpfmt]. Medtem ko je novejši, ima narejene odlične izboljšave v zmogljivosti,
kar pomeni bolj tekoče realno časovno urejanje v urejevalniku.

Angleščina je priporočljiva za vsa imena simbolov in infrastruktur kode. Komentarji so lahko napisani v kateremkoli jeziku,
ki ga lahko enostavno preberejo vse trenutne in bodoče strani, ki bodo delale s kodo.


[fig]: http://www.php-fig.org/
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[psr2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
[pear-cs]: http://pear.php.net/manual/en/standards.php
[zend-cs]: http://framework.zend.com/wiki/display/ZFDEV2/Coding+Standards
[symfony-cs]: http://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/
[phptools]: https://github.com/dericofilho/php.tools
[sublime-phpfmt]: https://github.com/dericofilho/sublime-phpfmt