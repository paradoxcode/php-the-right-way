---
title:   Composer in Packagist
isChild: true
anchor:  composer_and_packagist
---

## Composer in Packagist {#composer_and_packagist_title}

Composer je priporočeni upravljalnik odvisnosti za PHP. Napišite vaše projektne odvisnosti v `composer.json` datoteko in z nekaj enostavnimi ukazi bo Composer avtomatsko prenesel odvisnosti za vaš projekt in nastavil avtomatsko nalaganje (autoloading) za vas. Composer je analogno NPM v svetu Node.js ali Bundler v Ruby svetu.

Na voljo je obilica PHP knjižnic, ki so kompatibilne s Composer-jem in pripravljene za uporabo v vašem projektu. Ti
"paketi" so našteti na [Packagist]-u, uradnem repozitoriju za Composer-kompatibilne PHP knjižnice.

### Kako namestiti Composer

Najbolj varen način za namestitev Composer-ja je [slediti uradnim navodilom](https://getcomposer.org/download/).
To preveri, da namestitveni program ni pokvarjen ali ponarejen.
Namestitveni program namesti binarno skripto `composer.phar` v _vaš trenutni delovni direktorij_.

Composer priporočamo namestiti *globalno* (npr. v `/usr/local/bin`). Da to naredite, poženite sledeči ukaz:

{% highlight console %}
mv composer.phar /usr/local/bin/composer
{% endhighlight %}

**Opomba:** Če zgornje ni uspešno zaradi pravic, poženite ponovno s `sudo`.

Da poženete lokalno nameščen Composer, bi uporabili `php composer.phar`, globalno pa je enostavno `composer`.

#### Namestitev na Windows

Za Windows uporabnike je najenostavnejši način za pričetek uporaba namestitvenega programa [ComposerSetup], ki
izvede globalno namestitev in nastavi vašo `$PATH`, da lahko samo pokličete `composer` iz kateregakoli
direktorija v vaši ukazni vrstici.

### Kako definirati in namestiti odvisnosti

Composer beleži odvisnosti vašega projekta v datoteki imenovani `composer.json`. Če želite, jo lahko upravljate
ročno, ali uporabite sam Composer. Ukaz `composer require` doda odvisnost projekta
in če nimate `composer.json` datoteke, bo kreirana. Spodaj je primer, ki doda [Twig]
kot odvisnost v vaš projekt.

{% highlight console %}
composer require twig/twig:^2.0
{% endhighlight %}

Alternativno, ukaz `composer init` vas bo vodil skozi ustvarjanje celotne datoteke `composer.json`
za vaš projekt. Bodisi, ko enkrat ustvarite vašo `composer.json` datoteko lahko poveste Composer-ju,
da prenese in namesti vaše odvisnosti v `vendor/` direktorij. To velja tudi za projekte,
ki ste jih prenesli in že vsebujejo `composer.json` datoteko:

{% highlight console %}
composer install
{% endhighlight %}

V nadaljevanju dodajte naslednjo vrstico v vašo glavno PHP datoteko aplikacije. To narekuje PHP-ju, da uporabi Composer-jev
avtomatski nalagalnik (autoloader) za odvisnosti vašega projekta.

{% highlight php %}
<?php
require 'vendor/autoload.php';
{% endhighlight %}

Sedaj lahko uporabite odvisnosti vašega projekta in bodo avtomatsko naložene na zahtevo.

### Posodobitev vaših odvisnosti

Composer ustvari datoteko imenovano `composer.lock`, ki shrani točno verzijo za vsak paket, ki ga je
prenesel, ko ste prvič pognali ukaz `composer install`. Če delite vaš projekt z drugimi, zagotovite, da je datoteka `composer.lock`
vključena, tako da bodo ob ukazu `composer install` dobili enake verzije kot vi. Za posodobitev vaših odvisnosti poženite ukaz `composer update`. Ne uporabljajte `composer update`, ko nalagate aplikacijo na strežnik. Takrat poženite samo `composer install`, drugače boste lahko imeli drugačne verzije paketov v produkciji.

To je najbolj uporabno, ko definirate vaše verzije zahtev fleksibilno. Na primer zahtevana verzija
`~1.8` pomeni "karkoli novejše od `1.8.0`, vendar manj kot `2.0.x-dev`". Lahko uporabite tudi
nadomestni znak `*` kot pri `1.8.*`. Sedaj bo Composer ukaz `php composer.phar update` nadgradil vse vaše
odvisnosti na najnovejše verzije, ki ustrezajo omejitvam, ki ste jih definirali.

### Obvestila posodobitev

Da dobite obvestila o novih verzijah izdaj se lahko naročite na [libraries.io], spletno storitev,
ki nadzira odvisnosti in pošilja e-pošto z novimi izdajami paketov.

### Preverjanje vaših odvisnosti za varnostnimi težavami

[Security Advisories Checker] je spletni servis in orodje za ukazno vrstico (CLI), ki bo tako preučil vašo datoteko `composer.lock`
kot vam tudi povedal, če potrebujete kakšne posodobitve za vaše odvisnosti.

### Upravljanje globalnih odvisnosti s Composer-jem

Composer lahko tudi upravlja globalne odvisnosti in njihove zagonske datoteke. Uporaba je enostavna, vse kar morate
narediti je, da dodate predpono `global` vašim ukazom. Če na primer želite namestiti PHPUnit in ga imeti
na voljo globalno, poženite sledeči ukaz:

{% highlight console %}
composer global require phpunit/phpunit
{% endhighlight %}

To bo ustvarilo mapo `~/.composer`, kjer bodo domovale vaše globalne odvisnosti. Da imate nameščene
paketne zagonske datoteke in na voljo kjerkoli, bi potem dodali `~/.composer/vendor/bin` k vaši
spremenljivki `$PATH`.

* [Naučite se o Composer-ju]


[Packagist]: https://packagist.org/
[Twig]: https://twig.symfony.com/
[libraries.io]: https://libraries.io/
[Security Advisories Checker]: https://security.symfony.com/
[Naučite se o Composer-ju]: https://getcomposer.org/doc/00-intro.md
[ComposerSetup]: https://getcomposer.org/Composer-Setup.exe
