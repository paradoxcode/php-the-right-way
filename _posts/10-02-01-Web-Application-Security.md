---
title:   Varnost spletnih aplikacij
isChild: true
anchor:  web_application_security
---

## Varnost spletnih aplikacij {#web_application_security_title}

Za vsakega PHP razvijalca je pomembno, da se nauči [osnov varnosti spletnih aplikacij][4], ki se lahko razčlenijo na peščico širokih tem:

1. Ločevanje kode in podatkov.
   * Ko se podatki izvršujejo kot koda, dobite vrivanje SQL, XSS-napad, vključevanje lokalnih/oddaljenih datotek itd.
   * Ko je koda izpisana kot podatek, dobite uhajanje informacij, (razkritje izvorne kode, ali v primeru C programov,
     dovolj informacij za zaobiti [ASLR][5]).
2. Logika aplikacije.
   * Manjkajoče overjanje ali kontrola avtorizacije.
   * Validacija vnosa.
3. Operativno okolje.
   * PHP verzije.
   * Tretje osebne knjižnice.
   * Operacijski sistem.
4. Slabosti kriptografije.
   * [Šibka naključna števila][6].
   * [Izbrani šifrirni napadi][7].
   * [Uhajanje informacij o stranskih kanalih][8].

Obstajajo slabi ljudje pripravljeni in voljni izkoristiti vašo spletno aplikacijo. Pomembno je, da
naredite ustrezne varnostne ukrepe za izboljšanje varnosti vaše spletne aplikacije. Na srečo so dobri
ljudje pri [The Open Web Application Security Project][1] (OWASP) prevedli zgoščen seznam znanih varnostnih težav
in metod, da se lahko zaščitite pred napadalci. To je obvezno branje za varnostno ozaveščenega razvijalca. Drug dober vodič
za varnost spletnih PHP aplikacij je tudi [Survive The Deep End: PHP Security][3] avtorja Padraic Brady.

* [Preberite OWASP varnostni vodič][2]


[1]: https://www.owasp.org/
[2]: https://www.owasp.org/index.php/Guide_Table_of_Contents
[3]: http://phpsecurity.readthedocs.org/en/latest/index.html
[4]: https://paragonie.com/blog/2015/08/gentle-introduction-application-security
[5]: http://searchsecurity.techtarget.com/definition/address-space-layout-randomization-ASLR
[6]: https://paragonie.com/blog/2016/01/on-design-and-implementation-stealth-backdoor-for-web-applications
[7]: https://paragonie.com/blog/2015/05/using-encryption-and-authentication-correctly
[8]: http://blog.ircmaxell.com/2014/11/its-all-about-time.html
