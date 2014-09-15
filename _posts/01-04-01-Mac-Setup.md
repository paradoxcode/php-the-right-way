---
title:   Mac namestitev
isChild: true
anchor: mac_setup
---

## Namestitev v Mac okolju  {#mac_setup_title}

OS&nbsp;X sicer že vsebuje PHP, vendar ima običajno nekoliko starejšo verzijo za zadnjo stabilno. Lion vsebuje 
PHP 5.3.6, Mountain Lion ima 5.3.10 in Mavericks ima 5.4.17.

Posodobitev PHP-ja na OS&nbsp;X lahko namestite preko številnih [upravljalcev paketov][mac-package-managers] za Mac-a
s priporočenim [Liip php-osx][php-osx-downloads].

Lahko ga tudi [prevedete lastnoročno][mac-compile], če to naredite, poskrbie, da imate nameščen ali Xcode ali
Apple-ov nadomestek ["Command Line Tools for Xcode"][apple-developer], ki je na voljo za prenos iz Apple Mac Developer centra.

Za popoln "vse v enem" paket, ki vsebuje PHP, Apache spletni strežnik in MySQL bazo, skupaj z ličnim kontrolnim grafičnim
vmesnikom (GUI), poskusite [MAMP][mamp-downloads] ali [XAMPP][xampp].

[mac-package-managers]: http://www.php.net/manual/en/install.macosx.packages.php
[mac-compile]: http://www.php.net/manual/en/install.macosx.compile.php
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
[apple-developer]: https://developer.apple.com/downloads
[mamp-downloads]: http://www.mamp.info/en/downloads/
[php-osx-downloads]: http://php-osx.liip.ch/
[xampp]: http://www.apachefriends.org/en/xampp.html
