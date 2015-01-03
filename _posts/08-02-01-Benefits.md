---
title:   Koristi
isChild: true
anchor:  templating_benefits
---

## Koristi {#templating_benefits_title}

Glavna korist uporabe predlog je jasna ločitev, ki jo naredijo med logiko predstavitve in ostalo
vašo aplikacijo. Predloge imajo izključno odgovornost prikaza vsebine oblike. Niso odgovorne za
iskanje podatkov, pridobivanje in ostala bolj kompleksna opravila. To vodi v čistejšo bolj bralno kodo, ki je posebej
priročna v okolju ekip, kjer razvijalci delajo na kodi strežniške strani (krmilniki, modeli) in oblikvalci delajo
na kodi klientne strani (oblikovanje).

Predloge tudi izboljšajo organizacijo kode predstavitve. Predloge so običajno postavljene v folder "views", vsaka
definirana znotraj ene datoteke. Ta pristop spodbuja ponovno uporabo kode, kjer so večji bloki kode razbiti v manjše
ponovno uporabne dele, pogosto imenovani partials - deli. Na primer, glava in noga vaše strani sta lahko definirani vsaka kot predloga,
ki je nato vključena pred in za vsako predlogo strani.

Končno, odvisno od knjižnice, ki jo uporabljate, predloge lahko ponujajo več varnosti z avtomatičnim čiščenjem uporabniško generirane
vsebine. Nekatere knjižnice celo ponujajo peskovnik, kjer oblikovalci predlog dobijo samo dostop do dovoljenega seznama
spremenljivk in funkcij.
