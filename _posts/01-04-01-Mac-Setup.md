---
title:   Mac namestitev
isChild: true
anchor: mac_setup
---

## Namestitev v Mac okolju  {#mac_setup_title}

OS X sicer že vsebuje PHP, vendar ima običajno nekoliko starejšo verzijo za zadnjo stabilno. Mountain Lion vsebuje
PHP 5.3.10, Mavericks ima 5.4.17 in Yosemite ima 5.5.9, vendar z izzidom PHP 5.6 to pogostokrat ni dovolj.

Obstoja veliko načinov za namestitev PHP na OS X.

### Namestitev PHP preko Homebrew

[Homebrew](http://brew.sh/) je močan paketni urejevalnik za OS X, ki vam lahko pomaga namestiti PHP in
različne razširitve enostavno. [Homebrew PHP] je repozitorij, ki vsebuje PHP povezane 'formulae' za Homebrew,
in vam bo omogočil namestiti PHP.

Na tej točki, lahko namestite `php53`, `php54`, `php55` ali `php56` z uporabo ukaza `brew install`
in preklapljanje med njimi s spreminjanjem vaše spremenljivke `PATH`.

### Namestitev PHP preko phpbrew

[phpbrew] je orodje za namestitev in upravljanje različnih PHP verzij. To je lahko res uporabno, če dve
različni aplikaciji/projekta zahtevata različni verziji PHP in ne uporabljate virtualne naprave.

### Prevajanje iz izvorne kode

Druga opcija. ki vam da kontrolo nad verzijo PHP-ja, ki ga nameščate, je [da ga sami prevedete][mac-compile].
V tem primeru zagotovite, da imate nameščen ali Xcode ali Apple-ov nadomestek ["Command Line Tools for XCode"],
ki ga je moč prenesti iz Apple Developer Centra.

### All-in-One Installers

Rešitve napisane zgoraj v glavnem upravljajo sam PHP in ne podpirajo stvari kot je Apache, Nginx ali SQL server. "Vse-v-enem" rešitve kot je [MAMP][mamp-downloads] in [XAMPP][xampp] bodo namestile ostale dele programske opreme za vas in jo skupaj povezale, vendar enostavnost namestitve pride z pomanjkanjem fleksibilnosti.

[Homebrew]: http://brew.sh/
[Homebrew PHP]: https://github.com/Homebrew/homebrew-php#installation
[mac-compile]: http://php.net/manual/install.macosx.compile
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
["Command Line Tools for XCode"]: https://developer.apple.com/downloads
[mamp-downloads]: http://www.mamp.info/en/downloads/
[phpbrew]: https://github.com/phpbrew/phpbrew
[xampp]: http://www.apachefriends.org/en/xampp.html
