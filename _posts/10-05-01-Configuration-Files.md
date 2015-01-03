---
title:   Konfiguracijske datoteke
isChild: true
anchor:  configuration_files
---

## Konfiguracijske datoteke {#configuration_files_title}

Pri ustvarjanju konfiguracijskih datotek za vaše aplikacije, najboljše prakse priporočajo, da se upošteva eno izmed
naslednjih metod:

- Priporočljivo je, da shranite vaše konfiguracijske informacije, kjer ne morejo biti direktno dostopne in prebrane skozi
datotečni sistem.
- Če morate shraniti vaše konfiguracijske datoteke v vrhnji dokumentni direktorij, poimenujte datoteke s `.php` končnico. To
zagotovi, da tudi če se do skripte direktno dostopi, se ne bo izpisala kot enostaven tekst.
- Informacije v konfiguracijskih datotekah bi morale biti ustrezno zavarovane, ali preko enkripcije ali preko group/user datotečnih
sistemskih pravic.