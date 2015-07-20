---
title:   Predpomnilnik ukazne kode
isChild: true
anchor:  opcode_cache
---

## Predpomnilnik ukazne kode {#opcode_cache_title}

Ko se PHP datoteka izvede, se pod pokrovom najprej prevede v ukazno kodo - opcode in samo takrat se ukazna koda izvede.
Če PHP datoteka ni modificirana, bo ukazna koda vedno enaka. To pomeni, da je korak prevajanja zapravljanje CPU virov.

Tu je pomemben pa predpomnilnik ukazne kode. Preprečuje dodatna prevajanja s shranitvijo ukazne kode v spomin in jo ponovno uporabi pri zaporednih klicih.
Vzpostavitev predpomnilnika ukazne kode je stvar nekaj minut in vaša aplikacija bo znatno pohitrena. Res ni razloga, da ga ne bi uporabili.

Od PHP 5.5 je na voljo vgrajeni predpomnilnik ukazne kode imenovan [OPcache][opcache-book]. Ta je na voljo tudi
za prejšnje različice.

Preberite več o predpomnilnikih ukazne kode:

* [OPcache][opcache-book] (vgrajen od PHP 5.5)
* [APC] (PHP 5.4 in prejšnji)
* [XCache]
* [Zend Optimizer+] (del Zend Server paketa)
* [WinCache] (razširitev za MS Windows Server)
* [seznam pohitritev PHP na Wikipediji][PHP_accelerators]


[opcache-book]: http://php.net/book.opcache
[APC]: http://php.net/book.apc
[XCache]: http://xcache.lighttpd.net/
[Zend Optimizer+]: http://www.zend.com/en/products/zend_server
[WinCache]: http://www.iis.net/download/wincacheforphp
[PHP_accelerators]: http://en.wikipedia.org/wiki/List_of_PHP_accelerators
