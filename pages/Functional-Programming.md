---
layout: page
title: Funkcijsko programiranje v PHP
---

# Funkcijsko programiranje v PHP

PHP podpira prvo razredne funkcije, kar pomeni, da je funkcija lahko prirejena spremenljivki. Tako uporabniško definirane
kot vgrajene funkcije se lahko sklicujejo na spremenljivko. Funkcije se lahko podaja kot argumente drugim funkcijam
(lastnost imenovana funkcije višjega reda) in funkcija lahko vrne drugo funkcijo.

Rekurzija, lastnost, ki dovoljuje, da funkcija kliče samo sebe, je podprta s strani jezika, vendar največ osredotočanja
PHP kode je na iteracije.

Anonimne funkcije (s podporo za zaprtja - closures) so prisotne od PHP 5.3 (2009).

PHP 5.4 je dodal zmožnost vezanja zaprtij na objektov prosto in tudi izboljšal podporo za klicajoče, tako da so
lahko uporabljeni izmenično z anonimnimi funkcijami v skoraj vseh primerih.

Najbolj pogost primer uporabe funkcij višjih redov je, ko se implementira strateški vzorec. Vgrajena `array_filter`
funkcija sprašuje tako za vnosno polje (podatki) in funkcijo (strategija ali klicajoči), katera je uporabljena kot
filtrirna funkcija na vsakem elementu polja.

{% highlight php %}
<?php
$input = array(1, 2, 3, 4, 5, 6);

// Creates a new anonymous function and assigns it to a variable
$filter_even = function($item) {
    return ($item % 2) == 0;
};

// Built-in array_filter accepts both the data and the function
$output = array_filter($input, $filter_even);

// The function doesn't need to be assigned to a variable. This is valid too:
$output = array_filter($input, function($item) {
    return ($item % 2) == 0;
});

print_r($output);
{% endhighlight %}

Zaprtje je anonimna funkcija, ki lahko dostopa do spremenljivk uvoženih iz zunanjega prostora brez uporabe kakršnihkoli
globalnih spremenljivk. Teoretično je zaprtje funkcija z nekaj zaprtimi argumenti (t.j. fiksiranimi) zaradi okolja, ko je
definirana. Zaprtja lahko delajo okrog omejitev prostora spremenljivke na čisti način.

V naslednjem primeru bomo uporabili zaprtje za definicijo funkcije, ki vrne eno filtrirno funkcijo za `array_filter` izven
družine filtrirnih funkcij.

{% highlight php %}
<?php
/**
 * Creates an anonymous filter function accepting items > $min
 *
 * Returns a single filter out of a family of "greater than n" filters
 */
function criteria_greater_than($min)
{
    return function($item) use ($min) {
        return $item > $min;
    };
}

$input = array(1, 2, 3, 4, 5, 6);

// Use array_filter on a input with a selected filter function
$output = array_filter($input, criteria_greater_than(3));

print_r($output); // items > 3
{% endhighlight %}

Vsaka filtrirna funkcija v družini sprejme samo elemente večje od nekaterih najmanjših vrednosti. Enoten filter vrnjen
od `criteria_grater_than` je zaprtje z `$min` argumentom zaprtim s strani vrednosti v prostoru (podanim kot argument ko
je klican `criteria_greater_than`).

Zgodnje vezavanje je uporabljeno privzeto z uvozom `$min` spremenljivke v izdelano funkcijo. Za prava zaprtja z zakasnjeno
vezavo bi le-ta morala biti sklic, ko se uvaža. Predstavljajte si predlogo ali knjižnico za vnosno preverjanje, kjer je
zaprtje definirano za zajemanje spremenljivk v prostoru in dostopa do njih kasneje, ko se oceni anonimna funkcija.

* [Preberite več o Anonimnih funkcijah][anonymous-functions]
* [Več podrobnosti v Closures RFC][closures-rfc]
* [Preberite o dinaminčne sklicevanju funkcij s  `call_user_func_array`][call-user-func-array]

[anonymous-functions]: http://php.net/functions.anonymous
[call-user-func-array]: http://php.net/function.call-user-func-array
[closures-rfc]: https://wiki.php.net/rfc/closures
