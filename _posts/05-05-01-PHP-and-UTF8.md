---
title: Delo z UTF-8
isChild: true
anchor: php_and_utf8
---

## Delo z UTF-8 {#php_and_utf8_title}

_To sekcijo je prvotno napisal [Alex Cabal](https://alexcabal.com/) na
[PHP Best Practices](https://phpbestpractices.org/#utf-8) in je uporabljena kot osnova za naš lasten UTF-8 nasvet_.

### Tu ni ene vrstice. Bodite previdni, pozorni na podrobnosti in skladni.

Trenutno PHP ne podpira Unicode na nižjem nivoju. Obstajajo načini za zagotovitev, da so UTF-8 nizi v redu procesirani,
vendar ni enostavno in zahteva posvečanje na skoraj vseh nivojih spletne aplikacije, od HTML do SQL do PHP. Ciljali
bomo na kratek, praktičen povzetek.

### UTF-8 na PHP nivoju

Osnovne operacije nizov, kot sta združevanje dveh nizov in dodeljevanje nizov spremenljivkam, ne potrebujejo ničesar,
posebnega za UTF-8. Vendar večina funkcij nizov, kot sta `strpos()` in `strlen()`, ne potrebujeta posebnih premislekov. Te
funkcije imajo pogosto `mb_*` nadomestke: na primer `mb_strpos()` in `mb_strlen()`. Ti `mb_*` nizi so na voljo
za vas preko [razširitve multibyte niza] in so posebej načrtovane za operiranje na Unicode nizih.

Uporabljati morate `mb_*` funkcije kadarkoli izvajate operacije na Unicode nizih. Na primer, če uporabljate `substr()` na
UTF-8 nizu, je precejšnja verjetnost, da bo rezultat vključeval popačene polovične znake. Pravilna funkcija za uporabo
bi bila večbajtni nadomestek, `mb_substr()`.

Težji del si je zapomniti uporabo `mb_*` funkcij v vseh primerih. Če samo enkrat pozabite, bo vaš Unicode niz
zelo verjetno popačen med naslednjim procesiranjem.

Ne vse funkcije nizov imajo `mb_*` nadomestek. Če določene ni na voljo, za kar želite narediti, potem lahko nimate
sreče.

Uporabljati bi morali `mb_internal_encoding()` funkcijo na vrhu vsake PHP skripte, ki jo napišete (ali na
vrhu vaše globalne include skripte), in `mb_http_output()` funkcijo ravno za njo, če vaša skripta izpisuje
brskalniku. Izrecno definiranje kodiranja vašega niza v vsaki skripti vam bo prihranilo veliko glavobolov tekom
poti.

Dodatno mnogo PHP funkcij, ki operirajo na nizih imajo opcijske parametre, ki vam omogočajo specifikacijo kodiranja
znakov. Vedno bi morali eksplicitno navesti UTF-8, ko imate možnost. Na primer, `htmlentites()` ima
opcijo za kodiranje znakov in bi morali vedno določiti UTF-8, če imate opravka s takimi nizi. Bodite pozorni, da
od PHP 5.4.0 je UTF-8 privzeto kodiranje za `htmlentities()` in  `htmlspecialchars()`.

Končno, če gradite distribuirano aplikacijo in ne morete biti prepričani, da bo razširitev `mbstring`
omogočena, potem premislite o uporabi [patchwork/utf8] Composer paketa. Ta
bo uporabil `mbstring`, če je na voljo in se vrnil na ne UTF-8 funkcije, če ni.

[razširitve multybyte niza]: http://php.net/manual/en/book.mbstring.php
[patchwork/utf8]: https://packagist.org/packages/patchwork/utf8

### UTF-8 na nivoju podatkovne baze

Če vaša PHP skripta dostopa do MySQL-a, obstaja verjetnost, da so vaši nizi shranjeni kot ne-UTF-8 nizi v podatkovni bazi,
tudi če sledite vsem varnostnim ukrepom zgoraj.

Da zagotovite, da gredo vaši nizi iz PHP-ja v MySQL kot UTF-8, zagotovite, da so vaša podatkovna baza in tabele vse nastavljene
na `utf8mb4` set znakov in kolacijo in da uporabljate `utf8mb4` sete znakov v nizu povezave PDO. Glejte
primer kode spodaj. To je _kritično pomembno_.

Pomnite, da morate uporabiti `utf8mb4` set znakov za celotno UTF-8 podporo in ne `utf8` seta znakov! Glejte
nadaljnje branje spodaj zakaj.

### UTF-8 na nivoju brskalnika

Uporabite `mb_http_output()` funkcijo za zagotovitev, da vaša PHP skripta izpisuje UTF-8 nize v vaš brskalnik.
Brskalniku bo nato povedano s strani odziva HTTP, da ta stran bi morala biti smatrana kot UTF-8. Zgodovinski pristop za to je bil vključit [charset `<meta>` značko](http://htmlpurifier.org/docs/enduser-utf8.html) v značko `<head>` vaše strani. Ta pristop je povsem veljaven, vendar nastavitev charset-a v `Content-Type` glavi je dejansko [veliko hitrejši](https://developers.google.com/speed/docs/best-practices/rendering#SpecifyCharsetEarly).

{% highlight php %}
<?php
// Tell PHP that we're using UTF-8 strings until the end of the script
mb_internal_encoding('UTF-8');
 
// Tell PHP that we'll be outputting UTF-8 to the browser
mb_http_output('UTF-8');
 
// Our UTF-8 test string
$string = 'Êl síla erin lû e-govaned vîn.';
 
// Transform the string in some way with a multibyte function
// Note how we cut the string at a non-Ascii character for demonstration purposes
$string = mb_substr($string, 0, 15);
 
// Connect to a database to store the transformed string
// See the PDO example in this document for more information
// Note the `set names utf8mb4` commmand!
$link = new \PDO(   
                    'mysql:host=your-hostname;dbname=your-db;charset=utf8mb4',
                    'your-username',
                    'your-password',
                    array(
                        \PDO::ATTR_ERRMODE => \PDO::ERRMODE_EXCEPTION,
                        \PDO::ATTR_PERSISTENT => false
                    )
                );
 
// Store our transformed string as UTF-8 in our database
// Your DB and tables are in the utf8mb4 character set and collation, right?
$handle = $link->prepare('insert into ElvishSentences (Id, Body) values (?, ?)');
$handle->bindValue(1, 1, PDO::PARAM_INT);
$handle->bindValue(2, $string);
$handle->execute();
 
// Retrieve the string we just stored to prove it was stored correctly
$handle = $link->prepare('select * from ElvishSentences where Id = ?');
$handle->bindValue(1, 1, PDO::PARAM_INT);
$handle->execute();
 
// Store the result into an object that we'll output later in our HTML
$result = $handle->fetchAll(\PDO::FETCH_OBJ);

header('Content-Type: text/html; charset=UTF-8');
?><!doctype html>
<html>
    <head>
        <title>UTF-8 test page</title>
    </head>
    <body>
        <?php
        foreach($result as $row){
            print($row->Body);  // This should correctly output our transformed UTF-8 string to the browser
        }
        ?>
    </body>
</html>
{% endhighlight %}

### Nadaljnje branje

* [PHP priročnik: operacije nizov](http://php.net/manual/en/language.operators.string.php)
* [PHP priročnik: funkcije nizov](http://php.net/manual/en/ref.strings.php)
    * [`strpos()`](http://php.net/manual/en/function.strpos.php)
    * [`strlen()`](http://php.net/manual/en/function.strlen.php)
    * [`substr()`](http://php.net/manual/en/function.substr.php)
* [PHP priročnik: večbajtne funkcije nizov](http://php.net/manual/en/ref.mbstring.php)
    * [`mb_strpos()`](http://php.net/manual/en/function.mb-strpos.php)
    * [`mb_strlen()`](http://php.net/manual/en/function.mb-strlen.php)
    * [`mb_substr()`](http://php.net/manual/en/function.mb-substr.php)
    * [`mb_internal_encoding()`](http://php.net/manual/en/function.mb-internal-encoding.php)
    * [`mb_http_output()`](http://php.net/manual/en/function.mb-http-output.php)
    * [`htmlentities()`](http://php.net/manual/en/function.htmlentities.php)
    * [`htmlspecialchars()`](http://www.php.net/manual/en/function.htmlspecialchars.php)
* [PHP UTF-8 plonkec](http://blog.loftdigital.com/blog/php-utf-8-cheatsheet)
* [Stack Overflow: Kateri faktorji narejo PHP nekompatibilnega z Unicode?](http://stackoverflow.com/questions/571694/what-factors-make-php-unicode-incompatible)
* [Stack Overflow: Najboljše prakse v PHP in MySQL z mednarodnimi nizi](http://stackoverflow.com/questions/140728/best-practices-in-php-and-mysql-with-international-strings)
* [Kako podpirati celtni Unicode v MySQL podatkovnih bazah](http://mathiasbynens.be/notes/mysql-utf8mb4)
* [Prinašanje Unicode v PHP s prenosnim UTF-8](http://www.sitepoint.com/bringing-unicode-to-php-with-portable-utf8/)
