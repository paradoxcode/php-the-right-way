---
isChild: true
title:   Razširitev MySQL
anchor:  mysql_extension
---

## Razširitev MySQL {#mysql_extension_title}

Razširitev [mysql] za PHP je izjemno stara in je bila nadomeščena z dvema drugima razširitvima:

- [mysqli]
- [pdo]

Ne samo, da se je razvoj na [mysql] ustavil dolgo nazaj, razširitev je [opuščena od PHP 5.5.0][mysql_deprecated]
in je **[uradno odstranjena v PHP 7.0][mysql_removed]**.

Da si prihranite čas s poglabljanjem v vaše nastavitve `php.ini`, da vidite, katere module uporabljate, je ena opcija za iskanje `mysql_*`
v vašem priljubljenem urejevalniku. Če se pojavi katerakoli izmed funkcij, kot je `mysql_connect` in `mysql_query`, potem je
v uporabi `mysql`.

Tudi če še ne uporabljate PHP 7.0, izpustitev te nadgradnje kakor hitro je mogoče, bo vodilo k še večjim
težavam, ko boste prišli do nadgradnje PHP 7.0. Najboljša opcija je zamenjati uporabo mysql z [mysqli] ali [PDO] v
vaši aplikacijah znotraj vašega razvojnega razporeda, tako da se vam ne bo kasneje mudilo.

**Če nadgrajujete iz [mysql] k [mysqli], bodite pozorni o lenobnih vodičih nadgradnje, ki enostavno predlagajo najti in zamenjati `mysql_*` z `mysqli_*`. Ne samo, da je to prevelika posplošitev, pozablja tudi prednosti, ki jih mysqli ponuja, kot je vezava parametrov, ki je ponujena tudi v [PDO][pdo].**

* [PHP: Izbira API-ja za MySQL][mysql_api]
* [PDO Tutorial for MySQL Developers][pdo4mysql_devs]


[mysql]: http://php.net/mysql
[mysql_deprecated]: http://php.net/migration55.deprecated
[mysql_removed]: http://php.net/manual/en/migration70.removed-exts-sapis.php
[mysqli]: http://php.net/mysqli
[PDO]: http://php.net/pdo
[mysql_api]: http://php.net/mysqlinfo.api.choosing
[pdo4mysql_devs]: http://wiki.hashphp.org/PDO_Tutorial_for_MySQL_Developers
