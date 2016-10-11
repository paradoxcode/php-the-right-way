---
title:   Predpomnilnik ukazne kode
isChild: true
anchor:  opcode_cache
---

## Predpomnilnik ukazne kode {#opcode_cache_title}

Ko se PHP datoteka izvede, mora biti naprej prevesti v [ukazno kodo - opcodes](http://php.net/manual/en/internals2.opcodes.php) (navodila strojnega jezika za CPU). Če je izvorna koda nespremenjena, bo ukazna koda enaka, tako da ta korak sestavljanja postane odvečen vir za CPU.

Predpomnilnik ukazne kode (opcode cache) preprečuje odvečno sestavljanje s shranjevanjem ukazne kode v spomin in jo ponovno uporabi pri zaporednih klicih. Običajno se najprej preveri podpis ali čas spremembe datoteke, če je prišlo do kakšnih sprememb.

Verjetno je, da bo predpomnilnik ukazne kode naredil opazno izboljšanje hitrosti vaše aplikacije. Od PHP 5.5 je na voljo vgrajeni [Zend OPCache][opcache-book]. Odvisno od vašega PHP paketa/distribucije je običajno privzeto vključen - preverite [opcache.enable](http://php.net/manual/en/opcache.configuration.php#ini.opcache.enable) in izpis `phpinfo()`, da se prepričate. Za prejšnje verzije je na voljo PECL razširitev.

Preberite več o predpomnilnikih ukazne kode:

* [Zend OPcache][opcache-book] (vgrajen od PHP 5.5)
* Zend OPcache (prej znan kot Zend Optimizer+) je sedaj [odprto koden][Zend Optimizer+]
* [APC] (PHP 5.4 in prejšnji)
* [XCache]
* [WinCache] (razširitev za MS Windows Server)
* [seznam pohitritev PHP na Wikipediji][PHP_accelerators]


[opcache-book]: http://php.net/book.opcache
[APC]: http://php.net/book.apc
[XCache]: http://xcache.lighttpd.net/
[Zend Optimizer+]: https://github.com/zendtech/ZendOptimizerPlus
[WinCache]: http://www.iis.net/download/wincacheforphp
[PHP_accelerators]: http://en.wikipedia.org/wiki/List_of_PHP_accelerators
