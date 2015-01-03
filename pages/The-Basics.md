---
layout: page
title:  Osnove
sitemap: true
---

# Osnove

## Primerjalni operatorji

Primerjalni operatorji so pogosto spregledani aspekt PHP-ja, kar lahko pelje do mnogih nepričakovanih rezultatov.
En tak problem izhaja iz striktnih primerjav (primerjava logičnih izrazov kot cela števila).

{% highlight php %}
<?php
$a = 5;   // 5 as an integer

var_dump($a == 5);       // compare value; return true
var_dump($a == '5');     // compare value (ignore type); return true
var_dump($a === 5);      // compare type/value (integer vs. integer); return true
var_dump($a === '5');    // compare type/value (integer vs. string); return false

/**
 * Strict comparisons
 */
if (strpos('testing', 'test')) {    // 'test' is found at position 0, which is interpreted as the boolean 'false'
    // code...
}

// proti

if (strpos('testing', 'test') !== false) {    // true, as strict comparison was made (0 !== false)
    // code...
}
{% endhighlight %}

* [Primerjalni operatorji](http://php.net/language.operators.comparison)
* [Primerjalna tabela](http://php.net/types.comparisons)

## Pogojni stavki

### If stavki

Pri uporabi 'if/else' stavkov znotraj funkcije ali razreda, je pogosto spregledano, da mora biti 'else' uporabljen
v vezavi, da se deklarira potencialne rezultate. Vendar če rezultat definira vrednost, ki jo vrne, 'else' ni
potreben saj bo 'return' končala funkcijo, kar naredi 'else' spornega.

{% highlight php %}
<?php
function test($a)
{
    if ($a) {
        return true;
    } else {
        return false;
    }
}

// proti

function test($a)
{
    if ($a) {
        return true;
    }
    return false;    // else is not necessary
}
{% endhighlight %}

* [If stavki](http://php.net/control-structures.if)

### Switch stavki

Switch stavki so odličen način za izogib pisanju neskončnih 'if' in 'else' stavkov, vendar je nekaj stvari, na katere je dobro biti pozoren:

- Switch stavki samo primerjajo vrednosti in ne tipa (ekvivalentno '==')
- Ponavljajo 'case' za 'case' sklopom dokler ni ujemanje najdeno. Če ni najdenega ujemanja, potem je uporabljen 'default' (če je definiran)
- Brez 'break', bodo nadaljevali implementacijo vsakega 'case' dokler ne dosežejo 'break/return'
- Znotraj funkcije uporaba 'return' blaži potrebo po 'break' saj konča funkcijo

{% highlight php %}
<?php
$answer = test(2);    // the code from both 'case 2' and 'case 3' will be implemented

function test($a)
{
    switch ($a) {
        case 1:
            // code...
            break;             // break is used to end the switch statement
        case 2:
            // code...         // with no break, comparison will continue to 'case 3'
        case 3:
            // code...
            return $result;    // within a function, 'return' will end the function
        default:
            // code...
            return $error;
    }
}
{% endhighlight %}

* [Switch stavki](http://php.net/control-structures.switch)
* [PHP switch](http://phpswitch.com/)

## Globalni imenski prostor

Ko se uporablja imenske prostore, lahko ugotovite, da so interne funkcije skrite za funkcijami, ki jih napišete. Da se to popravi,
se sklicujte na globalne funkcije z uporabo poševnice nazaj pred imenom funkcije.

{% highlight php %}
<?php
namespace phptherightway;

function fopen()
{
    $file = \fopen();    // Our function name is the same as an internal function.
                         // Execute the function from the global space by adding '\'.
}

function array()
{
    $iterator = new \ArrayIterator();    // ArrayIterator is an internal class. Using its name without a backslash
                                         // will attempt to resolve it within your namespace.
}
{% endhighlight %}

* [Globalni prostor](http://php.net/language.namespaces.global)
* [Globalna pravila](http://php.net/userlandnaming.rules)

## Nizi

### Spajanje

- Če je vaša vrstica širša preko priporočene dolžine vrstice (120 znakov), razmislite o spajanju vaše vrstice
- Za bralnost je najboljše uporabiti operatorje spajanja nad operatorji dodeljevanja
- Medtem ko ste znotraj originalnega področja spremenljivke, zamaknite kodo, ko spajanje uporabi novo vrstico


{% highlight php %}
<?php
$a  = 'Multi-line example';    // concatenating assignment operator (.=)
$a .= "\n";
$a .= 'of what not to do';

// proti

$a = 'Multi-line example'      // concatenation operator (.)
    . "\n"                     // indenting new lines
    . 'of what to do';
{% endhighlight %}

* [Operatorji nizov](http://php.net/language.operators.string)

### Tipi nizov

Nizi so serija znakov, ki bi morali biti precej enostavni. Tako povedano je na voljo več različnih tipov
nizov in ponujajo malenkost drugačno sintakso z malenkost različnimi obnašanji.

#### Enojni citati

Enojni citati so uporabljeni za označevanje "dobesednih nizov". Dobesedni nizi ne poskušajo prevajati posebnih znakov
ali spremenljivk.

Če uporabljate enojne citate, bi lahko vnesli ime spremenljivke v niz kot je: `'stome $thing'` in videli
bi točen izpis `some $thing`. Če uporabljate dvojne citate, ki bi poskušali oceniti ime spremenljivke `$thing`
in pokazati napake, če ni najdena nobena spremenljivka.

{% highlight php %}
<?php
echo 'This is my string, look at how pretty it is.';    // no need to parse a simple string

/**
 * Output:
 *
 * This is my string, look at how pretty it is.
 */
{% endhighlight %}

* [Enojni citat](http://php.net/language.types.string#language.types.string.syntax.single)

#### Dvojni citati

Dvojni citati so švicarski nož nizov. Ne bodo sami prevedli spremenljivk kot je omenjeno zgoraj, vendar vse vrste
posebnih znakov, kot je `\n` za novo vrstico, `\t` za tabulator itd.

{% highlight php %}
<?php
echo 'phptherightway is ' . $adjective . '.'     // a single quotes example that uses multiple concatenating for
    . "\n"                                       // variables and escaped string
    . 'I love learning' . $code . '!';

// proti

echo "phptherightway is $adjective.\n I love learning $code!"  // Instead of multiple concatenating, double quotes
                                                               // enables us to use a parsable string
{% endhighlight %}

Dvojni citati lahko vsebujjejo spremnljivke, to se imenuje "interpolacija".

{% highlight php %}
<?php
$juice = 'plum';
echo "I like $juice juice"; // Output: I like plum juice
{% endhighlight %}

Ko se uporablja interpolacijo, je pogosti primer, da se bo spremenljivka dotikala drugega znaka.
Tu bo prišlo do nekaj zmede, kaj je ime spremenljivke in kaj je dobesedni znak.

Da se to odpravi, se ovije spremenljivko znotraj zavitih oklepajev.

{% highlight php %}
<?php
$juice = 'plum';
echo "I drank some juice made of $juices";    // $juice cannot be parsed

// proti

$juice = 'plum';
echo "I drank some juice made of {$juice}s";    // $juice will be parsed

/**
 * Complex variables will also be parsed within curly brackets
 */

$juice = array('apple', 'orange', 'plum');
echo "I drank some juice made of {$juice[1]}s";   // $juice[1] will be parsed
{% endhighlight %}

* [Dvojni citati](http://php.net/language.types.string#language.types.string.syntax.double)

#### Nowdoc sintaksa

Nowdoc sintaksa je bila predstavljena v 5.3 in se interno obnaša na podoben način kot enojni citati, razen ko je primernejše
uporabiti več vrstične nize brez potrebe po spojevanju.

{% highlight php %}
<?php
$str = <<<'EOD'             // initialized by <<<
Example of string
spanning multiple lines
using nowdoc syntax.
$a does not parse.
EOD;                        // closing 'EOD' must be on it's own line, and to the left most point

/**
 * Output:
 *
 * Example of string
 * spanning multiple lines
 * using nowdoc syntax.
 * $a does not parse.
 */
{% endhighlight %}

* [Nowdoc sintaksa](http://php.net/language.types.string#language.types.string.syntax.nowdoc)

#### Heredoc sintaksa

Heredoc sintaksa se interno obnaša na enak način kot dvojni citati razen, da je primernejša za uporabo
več vrstičnih nizov brez potrebe po spojevanju.

{% highlight php %}
<?php
$a = 'Variables';

$str = <<<EOD               // initialized by <<<
Example of string
spanning multiple lines
using heredoc syntax.
$a are parsed.
EOD;                        // closing 'EOD' must be on it's own line, and to the left most point

/**
 * Output:
 *
 * Example of string
 * spanning multiple lines
 * using heredoc syntax.
 * Variables are parsed.
 */
{% endhighlight %}

* [Heredoc sintaksa](http://php.net/language.types.string#language.types.string.syntax.heredoc)

### Kaj je hitreje?

Naokoli obstoja mit, da enojni citati so frakcijsko hitrejši kot dvojni nizi. To v
osnovi ni res.

Če definirate enojni niz in ne poskušate združevati vrednosti ali česarkoli kompliciranega, potem bodo ali enojni ali
dvojni nizi v celoti identični. In noben ni hitrejši.

Če združujete več nizov kateregakoli tipa ali interpolirate vrednosti v dvojno citirane nize, potem so lahko rezultati
različni. Če delate z majhnim številom vrednosti, potem je združevanje do potankosti hitrejše. Z veliko vrednosti je interpolacija
do potankosti hitrejša.

Ne glede na to, kaj delate z nizi, noben tip ne bo nikoli imel opaznejšega vpliva na vašo aplikacijo.
Če poskušate prepisati kodo, da uporablja enega ali drugega, je vedno vaja v jalovosti, torej se izogibajte tem mikro-optimizacijam razen če res
razumete pomen in vpliv teh razlik.

* [Ovrženje mita izboljšav zmogljivosti enojnih citatov](http://nikic.github.io/2012/01/09/Disproving-the-Single-Quotes-Performance-Myth.html)

## Trojni operatorji

Trojni operatorji so odlična pot za zgoščeno kodo, vendar so pogosto uporabljeni s presežkom. Medtem ko so lahko
trojni operatorji zloženi/gnezdeni, je priporočljivo uporabiti enega na vrstico zaradi bralnosti.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? 'yay' : 'nay';
{% endhighlight %}

V primerjavi je tu primer, ki žrtvuje vse oblike bralnosti za zmanjšanje števila vrstic.

{% highlight php %}
<?php
echo ($a) ? ($a == 5) ? 'yay' : 'nay' : ($b == 10) ? 'excessive' : ':(';    // excess nesting, sacrificing readability
{% endhighlight %}

To 'return' a value with ternary operators use the correct syntax.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? return true : return false;    // this example will output an error

// proti

$a = 5;
return ($a == 5) ? 'yay' : 'nope';    // this example will return 'yay'
{% endhighlight %}

Pozoren je treba biti, da ne potrebujete uporabljati trojnih operatorjev za vračanje logičnih vrednosti. Primer tega bi bil.

{% highlight php %}
<?php
$a = 3;

return ($a == 3) ? true : false; // Will return true or false if $a == 3

// proti

$a = 3;

return $a == 3; // Will return true or false if $a == 3
{% endhighlight %}

To lahko rečemo tudi za vse operacije (===, !==, !=, == itd.).

#### Uporaba oklepajev s trojnimi operatorji za oblikovanje in funkcijo

Ko se uporablja trojni operator, lahko oklepaji igrajo svojo vlogo za izboljšanje bralnosti kode in tudi vključitev zvez znotraj blokov izrazov. Primer, ko ni nobene zahteve po uporabi oklepajev, je:

{% highlight php %}
<?php
$a = 3;

return ($a == 3) ? "yay" : "nope"; // return yay or nope if $a == 3

// proti

$a = 3;

return $a == 3 ? "yay" : "nope"; // return yay or nope if $a == 3
{% endhighlight %}

Oklepaji nam tudi omogočajo zmožnost izdelave zvez znotraj blokov stavkov, kjer bo blok preverjen kot celota. Kot ta primer spodaj, ki bo vrnil true če oba ($a == 3 in $b == 4) sta true in $c == 5 je tudi true.

{% highlight php %}
<?php

return ($a == 3 && $b == 4) && $c == 5;
{% endhighlight %}

Drug primer je skupek kode spodaj, ki bo vrnil true, če ($a != 3 AND $b != 4) OR $c == 5.

{% highlight php %}
<?php

return ($a != 3 && $b != 4) || $c == 5;
{% endhighlight %}

* [Trojni operatorji](http://php.net/language.operators.comparison)

## Deklaracije spremenljivk

V času, ko programerji poskušajo narediti njihovo kodo čistejšo z deklaracijo vnaprej definiranih spremenljivk z
različnimi imeni. To pomeni, da je v realnosti potrebna poraba dvojnega spomina omenjene skripte. Za primer spodaj
recimo, da primer niza teksta vsebuje podatke vrednih 1MB, s kopiranjem spremenljivke ste povečali izvajanje skripte za
2MB.

{% highlight php %}
<?php
$about = 'A very long string of text';    // uses 2MB memory
echo $about;

// proti

echo 'A very long string of text';        // uses 1MB memory
{% endhighlight %}

* [Nasveti zmogljivosti](http://web.archive.org/web/20140625191431/https://developers.google.com/speed/articles/optimizing-php)
