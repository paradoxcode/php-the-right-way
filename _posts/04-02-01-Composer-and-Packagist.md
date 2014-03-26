---
title:   Composer in Packagist
isChild: true
anchor: composer_and_packagist
---

## Composer in Packagist {#composer_and_packagist_title}

Composer je **brilijanten** upravljalnik odvisnosti za PHP. Napišite vaše projektne odvisnosti v `composer.json` datoteko in z nekaj enostavnimi ukazi bo Composer avtomatsko prenesel odvisnosti za vaš projekt in nastavil avtomatsko nalaganje (autoloading) za vas.

Na voljo je že ogromno PHP knjižnic, ki so kompatibilne s Composer-jem in pripravljene za uporabo v vašem projektu. Te "paketi" so našteti na [Packagist-u][1], uradnem repozitoriju za Composer-kompatibilne PHP knjižnice.

### Kako namestiti Composer

Composer lahko namestite lokalno (v vaš trenutni delovni direktorij; čeprav to ni več priporočljivo) ali globalno (npr. /usr/local/bin). Ob predpostavki, da želite namestiti Composer lokalno, se Composer prenese v vaš projektni vrhovni direktorij:

    curl -s https://getcomposer.org/installer | php

To namesti `composer.phar` (PHP binarni arhiv). To lahko poženete s `php` za upravljanje vaših projektnih odvisnosti.
<strong>Prosimo, upoštevajte:</strong> Če ste prenesli naloženo kodo direktno v interpreter, prosimo prvo preberite kodo na spletu, da ste prepričani, da je varna.

#### Namestitev na Windows

Za Windows uporabnike je najenostavnejši način za pričetek uporaba namestitvenega programa [ComposerSetup][6], ki izvede globalno namestitev in nastavi vašo `$PATH`, da lahko samo pokličete `composer` iz kateregakoli direktorija v vaši ukazni vrstici.

### Kako namestiti Composer (ročno)

Ročna namestitev Composer-ja je napredna tehnika, čeprav obstajajo različni razlogi, zakaj bi razvijalec raje uporabil sledečo metodo proti uporabi interaktivne namestitvene rutine. Interaktivna namestitev preveri vašo PHP namestitev za zagotovitev, da:

- je uporabljena zadostna verzija PHP-ja
- `.phar` datoteke se lahko izvaja pravilno
- so zadostne nekatere pravice direktorijev
- določene problematične razširitve niso naložene
- so nastavljene določene `php.ini` nastavitve

Ker ročna namestitev ne izvede nobenih od teh preverjanj, se morate odločiti ali je to ustrezno za vas. Tako je na voljo Composer tudi ročno:

    curl -s https://getcomposer.org/composer.phar -o $HOME/local/bin/composer
    chmod +x $HOME/local/bin/composer

Pot `$HOME/local/bin` (ali direktorij po vaši izbiri) bi moral biti v vaši potni `$PATH` spremenljivki okolja. To bo omogočilo izvajanje ukaza `composer`.

Ko v dokumentaciji naletite na ukaz, kot je npr. `php composer.phar install`, ga lahko zamenjate in poženete sledeče:

    composer install

Ta sekcija predvideva, da ste namestili Composer globalno.

### Kako definirati in namestiti odvisnosti

Composer beleži odvisnosti vašega projekta v datoteki imenovani `composer.json`. Če želite, jo lahko upravljate ročno, ali uporabite sam Composer. Ukaz `composer require` doda odvisnost projekta in če nimate `composer.json` datoteke, bo kreirana. Spodaj je primer, ki doda [Twig][2] kot odvisnost v vaš projekt.

	composer require twig/twig:~1.8

Alternativno, ukaz `composer init` vas bo vodil skozi ustvarjanje celotne datoteke `composer.json` za vaš projekt. Bodisi, ko enkrat ustvarite vašo `composer.json` datoteko lahko poveste Composer-ju, da prenese in namesti vaše odvisnosti v `vendors/` direktorij. To velja tudi za projekte, ki ste jih prenesli in že vsebujejo `composer.json` datoteko:

    composer install

V nadaljevanju dodajte naslednjo vrstico v vašo glavno PHP datoteko aplikacije. To narekuje PHP-ju, da uporabi Composer-jev avtomatski nalagalnik (autoloader) za odvisnosti vašega projekta.

{% highlight php %}
<?php
require 'vendor/autoload.php';
{% endhighlight %}

Sedaj lahko uporabite odvisnosti vašega projekta in bodo avtomatsko naložene na zahtevo.

### Posodobitev vaših odvisnosti

Composer ustvari datoteko imenovano `composer.lock`, ki shrani točno verzijo za vsak paket, ki ga je prenesel, ko ste prvič pognali ukaz `php composer.phar install`. Če delite vaš projekt z drugimi razvijalci in je datoteka `composer.lock` del vaše distribucije, bodo ob ukazu `php composer.phar install` dobili točno enake verzije kot vi. Za posodobitev vaših odvisnosti poženite ukaz `php composer.phar update`.

To je najbolj uporabno, ko definirate vaše verzije zahtev fleksibilno. Na primer zahtevana verzija ~1.8 pomeni "karkoli novejše od 1.8.0, vendar manj kot 2.0.x-dev". Lahko uporabite tudi nadomestni znak `*` kot pri `1.8.*`. Sedaj bo Composer ukaz `php composer.phar update` nadgradil vaše odvisnosti na najnovejše verzije, ki ustrezajo omejitvam, ki ste jih definirali.

### Obvestila posodobitev

Da dobite obvestila o novih verzijah izdaj se lahko naročite na [VersionEye][3], spletno storitev, ki nadzira vaše GitHub in BitBucket račune za `composer.json` datotekami in pošilja e-pošto z novimi izdajami paketov.

### Preverjanje vaših odvisnosti za varnostnimi težavami

[Security Advisories Checker][4] je spletni servis in orodje za ukazno vrstico (CLI), ki bo tako preučil vašo datoteko `composer.lock` kot vam tudi povedal, če potrebujete kakšne posodobitve za vaše odvisnosti.

* [Naučite se o Composer-ju][5]

[1]: http://packagist.org/
[2]: http://twig.sensiolabs.org
[3]: https://www.versioneye.com/
[4]: https://security.sensiolabs.org/
[5]: http://getcomposer.org/doc/00-intro.md
[6]: https://getcomposer.org/Composer-Setup.exe

