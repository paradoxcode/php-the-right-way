---
title:   Testno gnani razvoj
isChild: true
anchor:  test_driven_development
---

## Testno gnani razvoj {#test_driven_development_title}

Vir [Wikipedia](http://en.wikipedia.org/wiki/Test-driven_development):

> Test-driven development (TDD) is a software development process that relies on the repetition of a very short development cycle: first the developer writes a failing automated test case that defines a desired improvement or new function, then produces code to pass that test and finally refactors the new code to acceptable standards. Kent Beck, who is credited with having developed or 'rediscovered' the technique, stated in 2003 that TDD encourages simple designs and inspires confidence

Obstaja več različnih tipov testiranja, ki ga lahko izvedete za vašo aplikacijo.

### Testiranje enot

Testiranje enot (Unit Testing) je programerski pristop, da se zagotovi funkcijam, razredom in metodam, da delujejo kot
pričakovano od trenutka, ko jih zgradite skozi celotno pot razvojnega cikla. S preverjanjem
vrednosti, ki vstopajo in izstopajo, različnih funkcij in metod lahko zagotovite, da notranja logika
deluje pravilno. Z uporabo injiciranja odvisnosti in gradnjo modelnih razredov in nastavkov lahko preverite, da so odvisnosti
pravilno uporabljene za še boljšo pokritost testiranja.

Ko izdelate razred ali funkcijo, bi morali narediti test enote za vsako obnašanje, ki ga mora imeti. Na zelo osnovnem nivoju bi se
morali prepričati, da pride do napake, ko pošljete napačne argumente, in se prepričati, da deluje, če pošljete pravilne.
To bo pomagalo, da ko naredite spremembe temu razredu ali funkciji kasneje v razvojnem ciklu,
bo stara funkcionalnost še vedno delovala kot pričakovano. Edina alternativa temu bi bila `var_dump()`
v test.php, kar ni nikoli v redu za gradnjo aplikacije - male ali velike.

Drug primer uporabe za teste enot je prispevanje odprti kodi. Če lahko napišete test, ki pokaže nedelujočo
funkcionalnost (t.j. napako), potemo jo popravite in pokažite, da gre test skozi, saj bodo popravki tako veliko bolj
sprejeti. Če poganjate projekt, ki sprejema poteg zahtevkov, potem bi morali predlagati to kot zahtevo.

[PHPUnit](http://phpunit.de) je defakto testno ogrodje za pisanje testov enot za PHP aplikacije, vendar je na voljo tudi precej alternativ:

* [atoum](https://github.com/atoum/atoum)
* [Enhance PHP](https://github.com/Enhance-PHP/Enhance-PHP)
* [PUnit](http://punit.smf.me.uk/)
* [SimpleTest](http://simpletest.org)

### Integracijsko testiranje

Vir [Wikipedia](http://en.wikipedia.org/wiki/Integration_testing):

> Integration testing (sometimes called Integration and Testing, abbreviated "I&T") is the phase in software testing in which individual software modules are combined and tested as a group. It occurs after unit testing and before validation testing. Integration testing takes as its input modules that have been unit tested, groups them in larger aggregates, applies tests defined in an integration test plan to those aggregates, and delivers as its output the integrated system ready for system testing.

Mnogo enakih orodij, ki so lahko uporabljena za testiranje enot, je lahko uporabljenih za integracijsko testiranje,
saj so uporabljeni mnogi enaki principi.

### Testiranje funkcionalnosti

Včasih je poznano tudi kot testiranje sprejemljivosti, testiranje funkcionalnosti sestoji iz uporabe orodij za
izdelavo avtomatskih testov, ki dejansko uporabljajo vašo aplikacijo namesto samo preverjanja, da se individualne
enote kode obnašajo pravilno in da lahko individualne enote pravilno komunicirajo med seboj. Ta orodja običajno
delujejo z uporabo pravih podatkov in simulirajo dejanske uporabnike aplikacije.

#### Orodja za testiranje funkcionalnosti

* [Selenium](http://seleniumhq.com)
* [Mink](http://mink.behat.org)
* [Codeception](http://codeception.com) je celotno testno ogrodje, ki vključuje sprejeta testna orodja
* [Storyplayer](http://datasift.github.io/storyplayer) je celotno testno ogrodje, ki vključuje podporo za izdelavo in uničenje testnih okolij na zahtevo