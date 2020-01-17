---
title:   Mac namestitev
isChild: true
anchor:  mac_setup
---

## Namestitev v Mac okolju {#mac_setup_title}

macOS sicer že vsebuje PHP, vendar ponavadi ne vsebuje zadnje stabilne verzije. Obstaja več načinov za namestitev zadnje verzije PHP jezika na macOS.

### Namestitev PHP preko Homebrew

[Homebrew] je paketni urejevalnik za macOS, ki omogoča enostavno namestitev PHP jezika ter različnih razširitev. [Homebrew PHP] je repozitorij, ki vsebuje PHP povezane "formulae", med drugim tudi vse zadnje stabilne verzije: 7.1, 7.2, 7.3 ter 7.4. Zadnjo verzijo lahko namestite z sledečo komando:

```
brew install php@7.4
```

Če želite preklapljati med različnimi verzijami PHP-ja lahko to storite s spreminjanjem vaše spremenljivke `PATH`. Druga možnost je uporaba [brew-php-switcher][brew-php-switcher], ki bo preklopil avtomatsko za vas.

### Namestitev PHP preko Macports

Projekt [MacPorts] je pobuda odprto kodne skupnosti načrtovati
sistem enostaven za uporabo, za prevajanje, nameščanje in nadgradnjo bodisi
ukazne vrstice, X11 ali Aqua osnovane odprto kodne programske opreme na OS X operacijskem
sistemu.

MacPorts podpira vnaprej prevedene zagonske datoteke, tako da vam ni potrebno prevajati vsako
odvisnost iz izvornih tarball datotek, reši vam življenje tudi če
nimate kakršnegakoli paketa nameščenega na vašem sistemu.

Za sedaj lahko namestite `php71`, `php72`, `php73`, ali `php74` z uporabo ukaza `port install` na primer:

    sudo port install php73
    sudo port install php74

Lahko poženete ukaz `select`, da preklopite vaš aktiven PHP:

    sudo port select --set php php74

### Namestitev PHP preko phpbrew

[phpbrew] je orodje za namestitev in upravljanje različnih PHP verzij. To je lahko res uporabno, če dve različni
aplikaciji/projekta zahtevata različni verziji PHP in ne uporabljate virtualne naprave.

### Namestitev PHP preko Liip-ovega zagonskega namestitvenega programa

Druga popularna opcija je [php-osx.liip.ch], ki ponuja eno vrstične namestitvene metode za verzije 5.3 do 7.3.
Ne prepisuje PHP zagonskih datotek nameščenih s strani Apple-a, vendar namesti vse na ločeno lokacijo (/usr/local/php5).

### Prevajanje iz izvorne kode

Druga opcija. ki vam da kontrolo nad verzijo PHP-ja, ki ga nameščate, je [da ga sami prevedete][mac-compile].
V tem primeru zagotovite, da imate nameščen ali [Xcode][xcode-gcc-substitution] ali Apple-ov nadomestek
["Command Line Tools for XCode"], ki ga je moč prenesti iz Apple Developer Centra.

### All-in-One Installers

Rešitve napisane zgoraj v glavnem upravljajo sam PHP in ne podpirajo stvari kot je [Apache][apache], [Nginx][nginx] ali SQL server.
"Vse-v-enem" rešitve kot je [MAMP][mamp-downloads] in [XAMPP][xampp] bodo namestile ostale dele programske opreme za
vas in jo skupaj povezale, vendar enostavnost namestitve pride z pomanjkanjem fleksibilnosti.


[Homebrew]: https://brew.sh/
[Homebrew PHP]: https://github.com/Homebrew/homebrew-php#installation
[MacPorts]: https://www.macports.org/install.php
[phpbrew]: https://github.com/phpbrew/phpbrew
[php-osx.liip.ch]: https://php-osx.liip.ch/
[mac-compile]: https://secure.php.net/install.macosx.compile
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
["Command Line Tools for XCode"]: https://developer.apple.com/downloads
[apache]: https://httpd.apache.org/
[nginx]: https://www.nginx.com/
[mamp-downloads]: https://www.mamp.info/en/downloads/
[xampp]: https://www.apachefriends.org/index.html
[brew-php-switcher]: https://github.com/philcook/brew-php-switcher
