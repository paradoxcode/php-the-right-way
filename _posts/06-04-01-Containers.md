---
title:   Kontejnerji
isChild: true
anchor: containers
---

## Kontejnerji {#containers_title}

Prva stvar, ki bi jo morali razumeti o kontejnerjih injiciranja odvisnosti je, da niso enaka stvar kot injiciranje
odvisnosti. Kontejner je pomožna prikladnost, ki nam pomaga implementirati injiciranje odvisnosti, vendar so lahko pogostokrat
napačno uporabljeni, da implementirajo anti-vzorec, storitveno lokacijo. Injiciranje DI (dependency injection) kontejnerja kot storitvena lokacija v naših razredih verjetno
naredi težje odvisnosti na kontejnerju kot odvisnost, ki jo zamenjujete. Tudi naredi kodo veliko bolj transparentno
in konec koncev težjo za testiranje.

Veliko modernih ogrodij ima svoje lastne kontejnerje injiciranja odvisnosti, ki vam omogočajo povezati odvisnosti skupaj skozi nastavitve.
Kaj to pomeni v praksi, je, da lahko pišete kodo aplikacije, ki je čista in ločena kot ogrodje na katerem je zgrajena.
