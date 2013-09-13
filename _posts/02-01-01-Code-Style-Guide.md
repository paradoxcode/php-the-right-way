---
title:   Vodič kodnega stila
isChild: false
---

# Vodič kodnega stila  {#code_style_guide_title}

PHP skupnost je velika in raznolika, sestavljena iz številnih knjižnic, ogrodij in komponent. Za PHP razvijalce je 
običajno, da izbirajo med mnogimi od le teh in jih kombinirajo v določenem projektu. Pomembno je, da se PHP koda oprijema 
(kolikor je le mogoče) skupnemu stilu kodiranja, saj omogoča za razvijalce enostavnejše mešanje in ujemanje različnih 
knjižnic za njihove projekte.

[Framework Interop Group][fig] so predlagali in odobrili serijo stilov priporočil, znanih kot [PSR-0][psr0], 
[PSR-1][psr1] in [PSR-2][psr2]. Naj vas nenavadna imena ne zmedejo, ta priporočila so samo 
skupek pravil, ki jih določeni projekti, kot so Drupal, Zend, Symfony, CakePHP, phpBB, AWS SDK, FuelPHP, Lithium itd. 
pričenjajo prevzemati. Lahko jih uporabite v vaših projektih ali nadaljujete z uporabo vaših osebnih stilov.

Idealno bi morali pisati PHP kodo, ki se oprijema znanih standardov. To je lahko kakršnakoli kombinacija PSR-jev, ali 
enega izmed kodnih standardov izdelanih s strani PEAR ali Zend. To pomeni, da ostali razvijalci lahko enostavno berejo 
in delajo z vašo kodo ter aplikacije, ki implementirajo komponente, imajo lahko konsistentnost celo, ko se uporablja veliko
tretje osebne kode.

* [Preberite o PSR-0][psr0]
* [Preberite o PSR-1][psr1]
* [Preberite o PSR-2][psr2]
* [Preberite o PEAR kodnih standardih][pear-cs]
* [Preberite o Zend kodnih standardih][zend-cs]

Lahko uporabite [PHP_CodeSniffer][phpcs], da preverite kodo proti katerimkoli izmed teh priporočil in vtičnike za tekstovne 
urejevalnike kot je [Sublime Text 2][st-cs], ki nudi realnočasovni odziv. 

Uporabite Fabien Potencier-jev [popravljalnik PHP kodnih standardov][phpcsfixer] za avtomatsko spreminjanje vaše kodne sintakse, 
da je usklajena s temi standardi in vam tako pomaga pred popravljanjem vsakega problema ročno.

Angleščina je priporočljiva za vsa imena simbolov in infrastruktur kode. Komentarji so lahko napisani v kateremkoli jeziku, 
ki ga lahko enostavno preberejo vse trenutne in bodoče strani, ki bodo delali s kodo.

[fig]: http://www.php-fig.org/
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[psr2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[pear-cs]: http://pear.php.net/manual/en/standards.php
[zend-cs]: http://framework.zend.com/wiki/display/ZFDEV2/Coding+Standards
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/
