---
title:   Mac namestitev
isChild: true
---

## Namestitev v Mac okolju  {#mac_setup_title}

OSX sicer že vsebuje PHP, vendar ima običajno nekoliko starejšo verzijo za zadnjo stabilno. Lion vsebuje 
PHP 5.3.6 in Mountain Lion ima 5.3.10.

Posodobitev PHP-ja na OSX lahko dobite nameščenega preko številnih [upravljalcev paketov][mac-package-managers] za Mac-a
s priporočenim [Liip php-osx][php-osx-downloads].

Druga možnost je [lastnoročno prevajanje][mac-compile], v tem primeru poskrbie, da imate nameščen ali Xcode ali
Apple-ov nadomestek ["Command Line Tools for Xcode"][apple-developer], ki je na voljo za prenos iz Apple Mac Developer centra.

Za popoln "vse v enem" paket, ki vsebuje PHP, Apache spletni strežnik in MySQL bazo, skupaj z lično kontrolnim grafičnim
vmesnikom (GUI), poskusite [MAMP][mamp-downloads] or [XAMPP][xampp].

[mac-package-managers]: http://www.php.net/manual/en/install.macosx.packages.php
[mac-compile]: http://www.php.net/manual/en/install.macosx.compile.php
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
[apple-developer]: https://developer.apple.com/downloads
[mamp-downloads]: http://www.mamp.info/en/downloads/index.html
[php-osx-downloads]: http://php-osx.liip.ch/
[xampp]: http://www.apachefriends.org/en/xampp.html
