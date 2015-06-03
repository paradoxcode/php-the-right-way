---
title:   Windows namestitev
isChild: true
anchor:  windows_setup
---

## Namestitev v Windows okolju {#windows_setup_title}

Prenesete lahko zagonske datoteke iz [windows.php.net/downloads][php-downloads]. Po razširitvi datotek PHP-ja je priporočljivo nastaviti [PATH][windows-path] na vrhovni direktorij vašega PHP direktorija (kjer se nahaja php.exe), da lahko izvršite PHP iz kjerkoli.

Za učenje in lokalni razvoj lahko uporabite vgrajeni spletni strežnik s PHP 5.4+, tako da vam ni treba skrbeti
za njegovo konfiguracijo. Če želite "vse v enem", ki vključuje celoten spletni strežnik in tudi MySQL, potem orodja, kot
so [Web Platform Installer][wpi], [XAMPP][xampp], [EasyPHP][easyphp] in [WAMP][wamp],
pripomorejo k hitri namestitvi na Windows razvojno okolje. Tako bodo orodja malenkost drugačna od
produkcijskih, zato bodite previdni na razlike v razvojnih okoljih, če delate na Windows-u in nalagate na Linux.

Če potrebujete zagnati vaš produkcijski sistem na Windows, potem vam bo IIS7 zagotovil najbolj stabilno in najboljše izvajanje. Lahko
uporabite [phpmanager][phpmanager] (GUI vtičnik za IIS7), ki enostavno skonfigurira in upravlja PHP. IIS7 vsebuje
že vgrajen FastCGI in je pripravljen na uporabo, tako da potrebujete samo skonfigurirati PHP kot hendler. Za podporo in dodatne vire
je na voljo [namensko področje na iis.net][php-iis] za PHP.


[php-downloads]: http://windows.php.net/download/
[windows-path]: http://www.windows-commandline.com/set-path-command-line/
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[xampp]: http://www.apachefriends.org/en/xampp.html
[easyphp]: http://www.easyphp.org/
[wamp]: http://www.wampserver.com/en/
[phpmanager]: http://phpmanager.codeplex.com/
[php-iis]: http://php.iis.net/
