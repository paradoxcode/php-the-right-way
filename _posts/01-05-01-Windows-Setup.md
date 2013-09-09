---
isChild: true
---

## Namestitev v Windows okolju {#windows_setup_title}

PHP za Windows je na voljo na več načinov. Lahko [prenesete binarne datoteke][php-downloads] in do pred kratkim ste lahko uporabili '.msi' 
namestitveni program. Namestitveni program ni več podprt in na voljo od PHP 5.3.0.

Za učenje in lokalni razvoj lahko uporabite vgrajeni spletni strežnik s PHP 5.4+, tako da vam ni treba skrbeti za njegovo konfiguracijo. Če 
želite "vse v enem", ki vključuje celoten spletni strežnik in tudi MySQL, potem orodja kot je [] [Web Platform Installer][wpi], 
[Zend Server CE][zsce], [XAMPP][xampp] in [WAMP][wamp] pripomorejo k hitri namestitvi na Windows razvojno okolje. Tako bodo orodja 
malenkost drugačna od produkcijskih, zato bodite previdni na razlike v razvojnih okoljih, če delate na Windows-u in nalagate na Linux.

Če potrebujete zagnati vaš produkcijski sistem na Windows, potem vam bo IIS7 zagotovil najbolj stabilno in najboljše izvajanje. Lahko uporabite 
[phpmanager][phpmanager] (GUI vtičnik za IIS7), ki enostavno skonfigurira in upravlja PHP. IIS7 vsebuje že vgrajen FastCGI in pripravljen 
na uporabo, tako da potrebujete samo skonfigurirati PHP kot hendler. Za podporo in dodatne vire je na voljo [namensko področje na iis.net][php-iis] za 
PHP.

[php-downloads]: http://windows.php.net
[phpmanager]: http://phpmanager.codeplex.com/
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[zsce]: http://www.zend.com/en/products/server-ce/
[xampp]: http://www.apachefriends.org/en/xampp.html
[wamp]: http://www.wampserver.com/
[php-iis]: http://php.iis.net/
