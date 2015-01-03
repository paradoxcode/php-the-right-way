---
title:   Virtualni ali namenski strežniki
isChild: true
anchor:  virtual_or_dedicated_servers
---

## Virtualni ali namenski strežniki {#virtual_or_dedicated_servers_title}

Če se počutite domače s sistemsko administracijo, ali ste zainteresirani za učenje, virtualni ali namenski strežniki ponujajo
celotno kontrolo vašega aplikacijskega produkcijskega okolja.

### nginx in PHP-FPM

PHP preko PHP-jevega vgrajenega FastCGI procesnega upravljalnika (FPM), gre res lepo skupaj z [nginx] strežnikom, ki je lahek,
dobro zmogljiv spletni strežnik. Uporabi manj spomina kot Apache in boljše ravna s trenutni zahtevki. To je
še posebej pomembno na virtualnih strežnikih, ki nimajo na voljo veliko spomina.

* [Preberite več o nginx][nginx]
* [Preberite več o PHP-FPM][phpfpm]
* [Preberite več o varni nastavitvi nginx in PHP-FPM][secure-nginx-phpfpm]

### Apache in PHP

PHP in Apache imata za sabo dolgo zgodovino. Apache je divje nastavljiv in ima na voljo mnogo
[modulov][apache-modules] za razširitev funkcionalnosti. Je popularna izbira za skupne strežnike in enostavna namestitev za PHP
ogrodja in odprtokodne aplikacije kot je WordPress. Na žalost Apache privzeto uporabi več virov kot nginx in
ne more ravnati z mnogimi uporabniki istočasno.

Apache ima nekaj možnih nastavitev za poganjanje PHP. Najbolj pogosta in enostavna za namestitev je [prefork MPM]
z mod_php5. Medtem ko ni najbolj spominsko učinkovit, je pa najbolj enostaven za delo in uporabo. To je verjetno
najboljša izbira, če se ne želite poglabljati preveč globoko v aspekte strežniške administracije. Upoštevajte, da če uporabljate
mod_php5, morate uporabiti prefork MPM.

Alternativno, če želite stisniti več zmogljivosti in stabilnosti iz Apache-ja, potem lahko izkoristite
enak FPM sistem kot nginx in pognati [worker MPM] ali [event MPM] z mod_fastcgi ali mod_fcgid. Ta nastavitev bo
bistveno bolj spominsko učinkovita in bolj hitra, vendar je potrebno več dela za vzpostavitev.

* [Preberite več o Apache][apache]
* [Preberite več o Multi-Processing modulih][apache-MPM]
* [Preberite več o mod_fastcgi][mod_fastcgi]
* [Preberite več o mod_fcgid][mod_fcgid]


[nginx]: http://nginx.org/
[phpfpm]: http://php.net/install.fpm
[secure-nginx-phpfpm]: https://nealpoole.com/blog/2011/04/setting-up-php-fastcgi-and-nginx-dont-trust-the-tutorials-check-your-configuration/
[apache-modules]: http://httpd.apache.org/docs/2.4/mod/
[prefork MPM]: http://httpd.apache.org/docs/2.4/mod/prefork.html
[worker MPM]: http://httpd.apache.org/docs/2.4/mod/worker.html
[event MPM]: http://httpd.apache.org/docs/2.4/mod/event.html
[apache]: http://httpd.apache.org/
[apache-MPM]: http://httpd.apache.org/docs/2.4/mod/mpm_common.html
[mod_fastcgi]: http://www.fastcgi.com/mod_fastcgi/docs/mod_fastcgi.html
[mod_fcgid]: http://httpd.apache.org/mod_fcgid/