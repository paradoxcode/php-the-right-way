---
title:   Upravljanje odvisnosti
isChild: false
anchor:  dependency_management
---

# Upravljanje odvisnosti {#dependency_management_title}

Na izbiro je ogromno PHP knjižnic, ogrodij in komponent. Vaš projekt bo najverjetneje uporabil več njih - to so t.i. projektne odvisnosti. Do pred kratkim, PHP ni imel dobrega načina za upravljanje teh projektnih odvisnosti. Tudi če ste jih upravljali ročno, ste morali še vedno skrbeti za avtomatske nalagalnike (autoloaders). Ne več.

Trenutno je za PHP na voljo več glavnih paketnih upravljalcev - Composer in PEAR. Kateri je pravi za vas? Odgovor je oba.


* Uporabite **Composer**, ko upravljate odvisnosti za posamezen projekt.
* Uporabite **PEAR**, ko upravljate odvisnosti za PHP kot celoto na vašem sistemu.

Na splošno, Composer paketi bodo na voljo samo v projektih, ki jih eksplicitno določite, dočim PEAR paket bo na voljo za vse vaše PHP projekte. Sicer PEAR zveni kot enostavnejši način na prvi pogled, so na voljo velike prednosti, ko uporabljate pristop odvisnosti projekt za projektom.