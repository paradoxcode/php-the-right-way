---
title:   Windows namestitev
isChild: true
anchor:  windows_setup
---

## Namestitev v Windows okolju {#windows_setup_title}

Prenesete lahko zagonske datoteke iz [windows.php.net/downloads][php-downloads]. Po razširitvi datotek PHP-ja je priporočljivo nastaviti [PATH][windows-path] na vrhovni direktorij vašega PHP direktorija (kjer se nahaja php.exe), da lahko izvršite PHP iz kjerkoli.

Za učenje in lokalni razvoj lahko uporabite vgrajeni spletni strežnik s PHP 5.4+, tako da vam ni treba skrbeti
za njegovo konfiguracijo. Če želite "vse v enem", ki vključuje celoten spletni strežnik in tudi MySQL, potem orodja, kot
so [Web Platform Installer][wpi], [XAMPP][xampp], [EasyPHP][easyphp], [OpenServer][openserver] in [WAMP][wamp],
pripomorejo k hitri namestitvi na Windows razvojno okolje. Tako bodo orodja malenkost drugačna od
produkcijskih, zato bodite previdni na razlike v razvojnih okoljih, če delate na Windows-u in nalagate na Linux.

Če potrebujete zagnati vaš produkcijski sistem na Windows, potem vam bo IIS7 zagotovil najbolj stabilno in najboljše izvajanje. Lahko
uporabite [phpmanager][phpmanager] (GUI vtičnik za IIS7), ki enostavno skonfigurira in upravlja PHP. IIS7 vsebuje
že vgrajen FastCGI in je pripravljen na uporabo, tako da potrebujete samo skonfigurirati PHP kot hendler. Za podporo in dodatne vire
je na voljo [namensko področje na iis.net][php-iis] za PHP.

V splošnem poganjanje vaše aplikacije v različnih okoljih v razvoju ali produkciji lahko vodi do čudnih hroščev, ko naložite
v živo. Če razvijate na Windows in nalagate na Linux (ali na karkoli, ki ni Windows), potem bi morali razmisliti o uporabi [virtualne naprave](/#virtualization_title).

Chris Tankersley ima zelo uporabno blog objavo, katera orodja uporablja za [PHP razvoj z uporabo Windows-a][windows-tools].

[easyphp]: http://www.easyphp.org/
[phpmanager]: http://phpmanager.codeplex.com/
[openserver]: http://open-server.ru/
[wamp]: http://www.wampserver.com/en/
[php-downloads]: http://windows.php.net/download/
[php-iis]: http://php.iis.net/
[windows-path]: http://www.windows-commandline.com/set-path-command-line/
[windows-tools]: http://ctankersley.com/2016/11/13/developing-on-windows-2016/
[wpi]: https://www.microsoft.com/web/downloads/platform.aspx
[xampp]: https://www.apachefriends.org/en/xampp.html
