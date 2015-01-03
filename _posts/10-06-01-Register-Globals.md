---
title:   Registracija globalnih spremenljivk
isChild: true
anchor:  register_globals
---

## Registracija globalnih spremenljivk {#register_globals_title}

**UPOŠTEVAJTE:** Od PHP 5.4.0 je bila nastavitev `register_globals` odstranjena in je ni več možno uporabljati.
To je samo vključeno kot opozorilo za kogarkoli v procesu nadgradnje stare aplikacije.

Ko je omogočeno, `register_globals` nastavitev naredi nekaj tipov spremenljivk (vključno tiste iz
`$_POST`, `$_GET` in `$_REQUEST`) na voljo globalnemu področju vaše aplikacije. To lahko hitro vodi v
varnostne težave, saj vaša aplikacija ne more efektivno povedati, od kod podatki prihajajo.

Na primer: `$_GET['foo']` je tako na voljo preko `$foo`, kar lahko prepiše spremenljivke, ki niso bile opredeljene.
Če uporabljate PHP < 5.4.0 __se prepričajte__ da je `register_globals` izključen - __off__.

* [register_globals v PHP priročniku](http://php.net/security.globals)