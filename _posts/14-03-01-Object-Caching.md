---
title:   Predpomnenje objektov
isChild: true
anchor: object_caching
---

## Predpomnenje objektov {#object_caching_title}

Pride čas, ko je koristno predpomniti individualne objekte v vašo kodo, kot so podatki, ki so prepomembni,
da bi jih dobili iz ali klicali v podatkovno bazo, kjer se rezultat verjetno ne bo spremenil. Lahko uporabite programsko
opremo za predpomnenje objektov, da shrani te dele podatkov v spomin pri izjemno hitrih kasnejših klicih. Če shranite te
elemente v podatkovno shrambo, ko naredite poizvedbo zanje, potem jih potegnite direktno iz predpomnilnika za le-te zahtevke.
Dobite lahko izjemno izboljšavo v zmogljivosti kot tudi zmanjšanje obremenitve na vaše strežnike podatkovne baze.

Mnoge popularne rešitve predpomnilnikov ukazne kode, vam omogočajo tudi predpomnenje podatkov po meri. Tako, da je še večji razlog,
da jih izkoristite. APCu, XCache in WinCache vsi ponujajo API-je, da shranite podatke iz vaše PHP kode v njihov spomin predpomnilnika.

Najobičajnejši uporabljani sistemi spominsko objektnega predpomnenja sta APCu in memcached. APCu je odlična izbira za objektno
predpomnenje, vključuje enostaven API za dodajanje vaših podatkov v njihov spomin predpomnilnika in je zelo enostaven za
nastaviti in uporabiti. Ena realna omejitev APCu-ja je, da je vezan na strežnik, na katerega je nameščen. Memcached po drugi strani je
nameščen kot ločena storitev in se do nje lahko dostopa čez omrežje, kar pomeni, da lahko shranite objekte v hiper-hitro podatkovno
shrambo v centralni lokaciji in mnoge različne sisteme lahko potegnete iz nje.

Upoštevajte, da ko poganjate PHP kot (Fast-)CGI aplikacijo znotraj vašega spletnega strežnika, bo imel vsak PHP proces namesto tega svoj
predpomnilnik, to pomeni, da APCu podatki ne bodo deljeni med vašimi delovnimi procesi. V teh primerih je namesto tega dobro premisliti o uporabi
memcached predpomnilnika, saj ni vezan na PHP procese.

V omrežnih nastavitvah APCu bo običajno prekašal memcached, kar se tiče dostopne hitrosti, vendar memcached bo sposoben
hitrejšega in širšega skaliranja. Če ne pričakujete, da boste imeli mnoge strežnike za poganjanje vaše aplikacije ali ne potrebujete
dodatnih lastnosti, ki jih memcached ponuja, potem je APCu verjetno najboljša izbira za predpomnenje objektov.

Primer logike z uporabo APCu:

{% highlight php %}
<?php
// check if there is data saved as 'expensive_data' in cache
$data = apc_fetch('expensive_data');
if ($data === false) {
    // data is not in cache; save result of expensive call for later use
    apc_add('expensive_data', $data = get_expensive_data());
}

print_r($data);
{% endhighlight %}

Upoštevajte, da pred PHP 5.5, APC ponuja tako predpomnilnik objektov kot tudi predpomnilnik ukazne kode. APCu je projekt,
ki je prinesel APC-jev predpomnilnik objektov v PHP 5.5+, odkar ima PHP sedaj vgrajeni predpomnilnik ukazne kode (OPcache).

Naučite se več o popularnih sistemih predpomnilnikov objektov:

* [APCu](https://github.com/krakjoe/apcu)
* [APC Functions](http://php.net/ref.apc)
* [Memcached](http://memcached.org/)
* [Redis](http://redis.io/)
* [XCache APIs](http://xcache.lighttpd.net/wiki/XcacheApi)
* [WinCache Functions](http://php.net/ref.wincache)
