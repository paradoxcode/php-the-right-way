---
title:  Podatkovne baze
anchor: databases
---

# Podatkovne baze {#databases_title}

Mnogokrat bo vaša PHP koda uporabila podatkovno bazo za pridobivanje informacij. Na voljo imate nekaj opcij za povezavo in interakcijo
z vašo podatkovno bazo. Priporočena opcija **do PHP 5.1.0** je bila uporaba originalnih gonilnikov kot so [mysqli], [pgsql], [mssql] itd.

Originalni gonilniki so odlični, če uporabljate samo _eno_ podatkovno bazo v vaši aplikaciji, vendar če na primer uporabljate MySQL in nekaj MSSQL hkrati,
ali se potrebujete povezati na Oracle podatkovno bazo, potem ne boste mogli uporabiti istih gonilnikov. Naučiti se boste morali popolnoma nov API za vsako
podatkovno bazo &mdash; in to lahko postane neumno.


[mysqli]: http://php.net/mysqli
[pgsql]: http://php.net/pgsql
[mssql]: http://php.net/mssql