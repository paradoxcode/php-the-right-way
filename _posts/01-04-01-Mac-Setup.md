---
title:   Mac namestitev
isChild: true
anchor:  mac_setup
---

## Namestitev v Mac okolju {#mac_setup_title}

OS X sicer že vsebuje PHP, vendar ima običajno nekoliko starejšo verzijo za zadnjo stabilno. Mavericks vsebuje PHP 5.4.17,
Yosemite 5.5.9, El Capitan 5.5.29 in Sierra 5.6.24, vendar z izzidom PHP 7.0 to pogostokrat ne zadostuje.

Obstoja veliko načinov za namestitev PHP na OS X.

### Namestitev PHP preko Homebrew

[Homebrew] je močan paketni urejevalnik za OS X, ki vam lahko pomaga namestiti PHP in različne razširitve enostavno.
[Homebrew PHP] je repozitorij, ki vsebuje PHP povezane 'formulae' za Homebrew, in vam bo omogočil
namestiti PHP.

Na tej točki, lahko namestite `php53`, `php54`, `php55`, `php56` ali `php70` z uporabo ukaza `brew install`
in preklapljanje med njimi s spreminjanjem vaše spremenljivke `PATH`. Druga možnost je uporaba [brew-php-switcher][brew-php-switcher],
ki bo preklopil avtomatsko za vas.

### Namestitev PHP preko Macports

Projekt [MacPorts] je pobuda odprto kodne skupnosti načrtovati
sistem enostaven za uporabo, za prevajanje, nameščanje in nadgradnjo bodisi
ukazne vrstice, X11 ali Aqua osnovane odprto kodne programske opreme na OS X operacijskem
sistemu.

MacPorts podpira vnaprej prevedene zagonske datoteke, tako da vam ni potrebno prevajati vsake
odvisnosti iz izvornih tarball datotek, reši vam življenje tudi če
nimate kakršnegakoli paketa nameščenega na vašem sistemu.

Za sedaj lahko namestite `php54`, `php55`, `php56` ali `php70` z uporabo ukaza `port install` na primer:

    sudo port install php56
    sudo port install php70

Lahko poženete ukaz `select`, da preklopite vaš aktiven php:

    sudo port select --set php php70

### Namestitev PHP preko phpbrew

[phpbrew] je orodje za namestitev in upravljanje različnih PHP verzij. To je lahko res uporabno, če dve različni
aplikaciji/projekta zahtevata različni verziji PHP in ne uporabljate virtualne naprave.

### Namestitev PHP preko Liip-ovega zagonskega namestitvenega programa

Druga popularna opcija je [php-osx.liip.ch], ki ponuja eno vrstične namestitvene metode za verzije 5.3 do 7.0.
Ne prepisuje php zagonskih datotek nameščenih s strani Apple-a, vendar namesti vse na ločeno lokacijo (/usr/local/php5).

### Prevajanje iz izvorne kode

Druga opcija. ki vam da kontrolo nad verzijo PHP-ja, ki ga nameščate, je [da ga sami prevedete][mac-compile].
V tem primeru zagotovite, da imate nameščen ali [Xcode][xcode-gcc-substitution] ali Apple-ov nadomestek
["Command Line Tools for XCode"], ki ga je moč prenesti iz Apple Developer Centra.

### All-in-One Installers

Rešitve napisane zgoraj v glavnem upravljajo sam PHP in ne podpirajo stvari kot je Apache, Nginx ali SQL server.
"Vse-v-enem" rešitve kot je [MAMP][mamp-downloads] in [XAMPP][xampp] bodo namestile ostale dele programske opreme za
vas in jo skupaj povezale, vendar enostavnost namestitve pride z pomanjkanjem fleksibilnosti.


[Homebrew]: http://brew.sh/
[Homebrew PHP]: https://github.com/Homebrew/homebrew-php#installation
[MacPorts]: https://www.macports.org/install.php
[phpbrew]: https://github.com/phpbrew/phpbrew
[mac-compile]: http://php.net/manual/install.macosx.compile
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
["Command Line Tools for XCode"]: https://developer.apple.com/downloads
[mamp-downloads]: http://www.mamp.info/en/downloads/
[xampp]: http://www.apachefriends.org/en/xampp.html
[brew-php-switcher]: https://github.com/philcook/brew-php-switcher
