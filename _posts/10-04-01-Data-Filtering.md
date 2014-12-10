---
title:   Filtriranje podatkov
isChild: true
anchor: data_filtering
---

## Filtriranje podatkov {#data_filtering_title}

Nikoli, nikoli ne zaupajte tujemu vnosu predstavljenemu vaši PHP kodi. Vedno počistite in preverite
tuj vnos, preden ga uporabljate v kodi. Funkciji `filter_var` in `filter_input` lahko počistita tekst
in preverita obliko teksta (npr. e-poštni naslov).

Tuj vnos je lahko karkoli: `$_GET` in `$_POST` podatki obrazcev, nekatere vrednosti v `$_SERVER`
superglobalni spremenljivki in telo (body) HTTP zahtevka preko `fopen('php://input', 'r')`. Dobro je vedeti,
da tuj vnos ni omejen na poslane podatke iz obrazca s strani uporabnika. Naložene in prenesene datoteke, vrednosti
sej, podatki piškotkov in podatki s tretjih strani spletnih servisev so tudi tuji vnosi.

Medtem ko se tuje podatke lahko shrani, kombinira in do njih dostopa kasneje, gre še vedno za tuj vnos. Vsakič,
ko procesirate, izpisujete, spojite ali vključite podatke v vašo kodo, se vprašajte, če so bili podatki ustrezno
filtrirani in jim lahko zaupate.

Podatki so lahko _filtrirani_ različno na osnovi njihovega namena. Na primer, ko je nefiltriran tuj vnos podan
v izpis HTML strani, lahko izvede HTML in JavaScript na vaši strani! To je poznano kot Cross-Site Scripting (XSS)
in je lahko zelo nevaren napad. En način, da se izognete XSS, je čiščenje vseh uporabnikovih generiranih podatkov,
preden jih izpišete v vašo stran, z odstranitvijo HTML značke s funkcijo `strip_tags` ali čiščenje znakov s posebnim
pomenom (escaping) v njihove ustrezne HTML entitete s funkcijama `htmlentites` ali `htmlspecialchars`.

Drug primer je podajanje opcij, ki se bodo izvedle v komandni vrstici. To je lahko izjemno nevarno
(in je ponavadi slaba ideja), vendar lahko uporabite vgrajeno funkcijo `escapeshellarg` za čiščenje
izvedenih ukaznih argumentov.

Zadnji primer je sprejemanje tujega vnosa za ugotovitev, katero datoteko naložiti iz datotečnega sistema. To je
lahko izkoriščeno s spremembo imena datoteke v pot datoteke. Odstraniti morate "/", "../", [null bajte][6], ali ostale
znake iz poti datoteke, da ne uspe naložiti skritih, nejavnih ali občutljivih datotek.

* [Naučite se o filtriranju podatkov][1]
* [Naučite se o `filter_var`][4]
* [Naučite se o `filter_input`][5]
* [Naučite se o ravnanju z null bajti][6]

### Čiščenje

Čiščenje odstrani (ali spremeni - escaping) nedovoljene ali nevarne znake iz tujega vnosa.

Na primer, morali bi počistiti tuj vnos preden vključujete vnos v HTML ali ga vnašate
v izvorno SQL poizvedbo. Ko uporabljate vezanje parametrov s [PDO](#databases), bo
vnos počistilo za vas.

Včasih je potrebno dovoliti nekatere varne HTML značke v vnosu, ko se ga vključuje v HTML stran.
To je zelo težko izvesti in mnogi se tega izogibajo z uporabo ostalih bolj omejenih oblikovanj kot
sta Markdown ali BBCode, čeprav s tem namenom obstajajo čistilne knjižnice kot je [HTML Purifier][html-purifier].

[Poglejte si čistilne filtre][2]

### Preverjanje

Preverjanje zagotavlja, da je tuj vnos to, kar pričakujete. Na primer, lahko boste želeli preveriti
e-poštni naslov, telefonsko številko ali starost pri procesiranju registracijske oddaje.

[Poglejte si filtre preverjanja][3]

[1]: http://php.net/book.filter
[2]: http://php.net/filter.filters.sanitize
[3]: http://php.net/filter.filters.validate
[4]: http://php.net/function.filter-var
[5]: http://php.net/function.filter-input
[6]: http://php.net/security.filesystem.nullbytes
[html-purifier]: http://htmlpurifier.org/
