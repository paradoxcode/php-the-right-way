---
title:   Poročanje o napakah
isChild: true
---

## Poročanje o napakah {#error_reporting_title}

Beleženje napak je lahko uporabno v tem, da najdete problematične točke v vaši aplikaciji, vendar lahko tudi razkrije
informacije o strukturi aplikacije zunanjemu svetu. Za efektivno zaščito vaše aplikacije pred težavami, ki jih lahko
povzroči izpis teh sporočil, morate nastaviti vaš razvojni strežnik drugače od produkcijske različice (v živo).

### Razvoj

Za prikaz vsake možne napake med <strong>razvojem</strong>, nastavite sledeče v vaši `php.ini` datoteki:

    display_errors = On
    display_startup_errors = On
    error_reporting = -1
    log_errors = On

> Podajanje vrednosti `-1` bo prikazalo vsako možno napako, tudi če so novi nivoji ali konstante dodani v prihodnjih PHP verzijah. `E_ALL` konstanta se tudi obnaša na tak način od PHP 5.4. - [php.net](http://php.net/manual/function.error-reporting.php)

`E_STRICT` konstanta nivoja napak je bila predstavljena v 5.3.0 in ni
del `E_ALL`, čeprav je postala del `E_ALL` v 5.4.0. Kaj to pomeni?
V smislu poročanja vsake možne napake v verziji 5.3 pomeni, da morate
uporabiti ali `-1` ali `E_ALL | E_STRICT`.

**Poročanje vsake možne napake po PHP verzijah**

* &lt; 5.3 `-1` or `E_ALL`
* &nbsp; 5.3 `-1` or `E_ALL | E_STRICT`
* &gt; 5.3 `-1` or `E_ALL`

### Produkcija

Da skrijete napake v vašem <strong>produkcijskem</strong> okolju, nastavite vašo `php.ini` datoteko kot:

    display_errors = Off
    display_startup_errors = Off
    error_reporting = E_ALL
    log_errors = On

S temi nastavitvami v produkciji, bodo napake še vedno zabeležene v dnevnike napak za spletni strežnik, vendar ne bodo
prikazane uporabniku. Za več informacij na teh nastavitvah, si oglejte PHP priročnik:

* [error_reporting](http://php.net/manual/errorfunc.configuration.php#ini.error-reporting)
* [display_errors](http://php.net/manual/errorfunc.configuration.php#ini.display-errors)
* [display_startup_errors](http://php.net/manual/errorfunc.configuration.php#ini.display-startup-errors)
* [log_errors](http://php.net/manual/errorfunc.configuration.php#ini.log-errors)
