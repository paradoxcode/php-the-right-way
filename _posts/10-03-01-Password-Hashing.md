---
title:   Zgoščevanje gesel
isChild: true
anchor:  password_hashing
---

## Zgoščevanje gesel {#password_hashing_title}

Eventuelno vsakdo zgradi PHP aplikacijo, ki uporablja uporabniško prijavo. Uporabniška imena in gesla so lahko shranjena v podatkovni bazi in potem uporabljena za potrjevanje
uporabnikov pri prijavi.

Pomembno je, da se ustrezno [_zgosti_][3] gesla, preden se jih shrani. Zgoščevanje gesel je nepovratna, enosmerna funkcija izvedena nad uporabnikovim geslom. To naredi
določeno dolg niz, ki se ga ne da enostavno povrniti. To pomeni, da lahko primerjate zgostitev z drugo, da ugotovite, če obe prihajata iz istega vira niza, vendar pa ne morete
določiti osnovnega niza. Če gesla niso zgoščena in je vaša podatkovna baza dostopna s strani neavtorizirane tretje strani, so vsi uporabniški računi ogroženi.

Gesla bi morala biti posamezno [_soljena_][5] z dodajanjem naključnega niza za vsako geslo pred zgoščevanjem. To preprečuje napade s slovarji in z uporabo "mavričnih tabel" (obratni seznam kriptografskih zgostitev za pogosta gesla).

Zgoščevanje in soljenje sta izjemnega pomena, saj uporabniki pogostokrat uporabljajo enako geslo za več storitev in kvaliteta gesla je lahko slaba.

Na srečo, dandanes PHP to naredi enostavno.

**Zgoščevanje gesel s `password_hash`**

V PHP 5.5 je bila izdana funkcija `password_hash()`. Trenutno uporablja BCrypt, najmočnejši algoritem trenutno podprt s strani PHP-ja. Bo pa tudi posodobljena v prihodnosti za podporo večih
algoritmov, kakor bo potrebno. Ustvarjena je bila knjižnica `password_compat`, ki ponuja vnaprejšnjo kompatibilnost za PHP >= 5.3.7.

Spodaj bomo zgostili niz in nato preverili zgostitev proti novemu nizu. Ker sta naša dva vira nizov različna ('secret-password' proti 'bad-password'), ta prijava ne bo uspela.

{% highlight php %}
<?php
require 'password.php';

$passwordHash = password_hash('secret-password', PASSWORD_DEFAULT);

if (password_verify('bad-password', $passwordHash)) {
    // Correct Password
} else {
    // Wrong password
}
{% endhighlight %}

`password_hash()` poskrbi za soljenje gesel. Sol je shranjena skupaj z algoritmom in "ceno" kot del zgostitve. `password_verify()` to izloči, da določi, kako preveriti geslo, tako da vam ni potrebno uporabiti ločenega polja v podatkovni bazi, da shranite vaše soli.

* [Naučite se o `password_hash()`] [1]
* [`password_compat` za PHP >= 5.3.7 && < 5.5] [2]
* [Naučite se o zgoščevanju v zvezi s kriptografijo] [3]
* [Naučite se o soleh] [5]
* [PHP `password_hash()` RFC] [4]


[1]: http://php.net/function.password-hash
[2]: https://github.com/ircmaxell/password_compat
[3]: http://en.wikipedia.org/wiki/Cryptographic_hash_function
[4]: https://wiki.php.net/rfc/password_hash
[5]: https://en.wikipedia.org/wiki/Salt_(cryptography)
