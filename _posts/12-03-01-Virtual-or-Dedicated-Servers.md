---
title:   Virtualni ali namenski strežniki
isChild: true
anchor: virtual_or_dedicated_servers
---

## Virtualni ali namenski strežniki {#virtual_or_dedicated_servers_title}

Če se počutite domače s sistemsko administracijo, ali ste zainteresirani za učenje, virtualni ali namenski strežniki ponujajo celotno kontrolo vašega aplikacijskega produkcijskega okolja.

### nginx in PHP-FPM

PHP preko PHP-jevega vgrajenega FastCGI procesnega upravljalnika (FPM), gre res lepo skupaj z [nginx](http://nginx.org) strežnikom, ki je lahek, dobro zmogljiv spletni strežnik. Uporabi manj
spomina kot Apache in boljše ravna s trenutni zahtevki. To je še posebej pomembno na virtualnih strežnikih, ki nimajo na voljo veliko spomina.

* [Preberite več o nginx](http://nginx.org)
* [Preberite več o PHP-FPM](http://php.net/install.fpm)
* [Preberite več o varni nastavitvi nginx in PHP-FPM](https://nealpoole.com/blog/2011/04/setting-up-php-fastcgi-and-nginx-dont-trust-the-tutorials-check-your-configuration/)

### Apache in PHP

PHP in Apache imata za sabo dolgo zgodovino. Apache je divje nastavljiv in ima na voljo mnogo [modulov](http://httpd.apache.org/docs/2.4/mod/) za razširitev funkcionalnosti. Je popularna izbira
za skupne strežnike in enostavna namestitev za PHP ogrodja in odprtokodne aplikacije kot je WordPress. Na žalost Apache privzeto uporabi več virov kot nginx in ne more ravnati z mnogimi uporabniki
istočasno.

Apache ima nekaj možnih nastavitev za poganjanje PHP. Najbolj pogosta in enostavna za namestitev je [prefork MPM](httpd://httpd.apache.org/docs/2.4/mod/prefork.html) z mod_php5. Medtem ko ni
najbolj spominsko učinkovit, je pa najbolj enostaven za delo in uporabo. To je verjetno najboljša izbira, če se ne želite poglabljati preveč globoko v aspekte strežniške administracije. Upoštevajte,
da če uporabljate mod_php5, morate uporabiti prefork MPM.

Alternativno, če želite stisniti več zmogljivosti in stabilnosti iz Apache-ja, potem morate izkoristiti enak FPM sistem kot nginx in pognati [worker MPM](http://httpd.apache.org/docs/2.4/mod/worker.html) ali [event MPM](http://httpd.apache.org/docs/2.4/mod/event.html) z mod_fastcgi ali mod_fcgid. Ta nastavitev bo bistveno bolj spominsko učinkovita in bolj hitra, vendar je potrebno več dela za vzpostavitev.

* [Preberite več o Apache](http://httpd.apache.org/)
* [Preberite več o Multi-Processing modulih](http://httpd.apache.org/docs/2.4/mod/mpm_common.html)
* [Preberite več o mod_fastcgi](http://www.fastcgi.com/mod_fastcgi/docs/mod_fastcgi.html)
* [Preberite več o mod_fcgid](http://httpd.apache.org/mod_fcgid/)
