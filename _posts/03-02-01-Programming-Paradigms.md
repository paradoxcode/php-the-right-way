---
title:   Programske paradigme
isChild: true
---

## Programske paradigme {#programming_paradigms_title}

PHP je fleksibilen, dinamičen jezik, ki podpira celo vrsto programskih tehnik. Tekom let se je izjemno razvijal, 
še posebej z dodatkom objektno orientiranega modela v PHP 5.0 (2004), anonimne funkcije in imenski prostori (namespaces) 
v PHP 5.3 (2009) in t.i. traits v PHP 5.4 (2012).

### Objektno orientirano programiranje

PHP ima celoten nabor lastnosti objektnega programiranja, katere vključujejo podporo za razrede (classes), abstraktne razrede, 
vmesnike (interfaces), dedinjenje, konstruktorje, kloniranje, izjeme in še več.

* [Preberite o PHP objektnem programiranju][oop]
* [Preberite Traits poglavja][traits]

### Funkcijsko programiranje

PHP podpira prvo razredne funkcije, kar pomeni, da je lahko funkcija dodeljena spremenljivki. Tako uporabniško definirane ali
vgrajene funkcije se lahko sklicujejo v spremenljivki in se jih kliče dinamično. Funkcije se lahko podaja kot argumente drugim
funkcijam (lastnost višji red - higher-order funkcije) in funkcija lahko vrne tudi drugo funkcijo.

Rekurzija, lastnost, ki dovoljuje funkciji, da kliče samo sebe, je podprta v jeziku, vendar večina PHP kode se osredotoča na
iteracije.

Nove anonimne funkcije (s podporo za zapiranje - closures) so prisotne od PHP 5.3 (2009).

PHP 5.4 je dodal zmožnost za vezavo zapiranj (bind closures) obsega objekta in tudi izboljšano podporo klicajočih, tako da
so lahko uporabljene neodvisno z anonimnimi funkcijami v skoraj vseh primerih.

* Nadaljujte branje na strani [funkcijsko programiranje v PHP](/pages/Functional-Programming.html)
* [Preberite o anonimnih funkcijah][anonymous-functions]
* [Preberite o Closure razredu][closure-class]
* [Več podrobnosti v Closures RFC][closures-rfc]
* [Preberite o Callables][callables]
* [Preberte o dinamično sklicujočih funkcijah s `call_user_func_array`][call-user-func-array]

### Meta programiranje

PHP podpira vrsto oblik meta programiranja skozi mehanizme kot so Reflection API in magične metode. Na voljo je veliko
magičnih metod kot so `__get()`, `__set()`, `__clone()`, `__toString()`, `__invoke()`, itd. ki omogočajo
razvijalcem da se povežejo v obnašanje razreda. Ruby razvijalci pogosto pravijo, da v PHP-ju manjka `method_missing`, vendar je na voljo
kot `__call()` in `__callStatic()`.

* [Preberite vse o magičnih metodah][magic-methods]
* [Preberite o rekleksiji][reflection]

[namespaces]: http://php.net/manual/en/language.namespaces.php
[overloading]: http://php.net/manual/en/language.oop5.overloading.php
[oop]: http://www.php.net/manual/en/language.oop5.php
[anonymous-functions]: http://www.php.net/manual/en/functions.anonymous.php
[closure-class]: http://php.net/manual/en/class.closure.php
[callables]: http://php.net/manual/en/language.types.callable.php
[magic-methods]: http://php.net/manual/en/language.oop5.magic.php
[reflection]: http://www.php.net/manual/en/intro.reflection.php
[traits]: http://www.php.net/traits
[call-user-func-array]: http://php.net/manual/en/function.call-user-func-array.php
[closures-rfc]: https://wiki.php.net/rfc/closures
