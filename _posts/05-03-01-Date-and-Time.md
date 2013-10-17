---
title:   Datum in čas
isChild: true
---

## Datum in čas {#date_and_time_title}

PHP ima razred DateTime, ki pomaga, ko berete, pišete, primerjate ali računate z datumi in časi. V PHP-ju je na voljo
mnogo funkcij, ki se nanašajo na datum in čas poleg DateTime razreda, vendar le-ta ponuja ličen objektno orientiran
vmesnik za večino najpogostejših primerov uporabe. Omogoča ravnanje s časovnimi območji, vendar to je izven te kratke predstavitve.

Za pričetek dela z DateTime, pretvorimo izvorni niz datuma in časa v objekt s tovarniško metodo `createFromFormat()`,
ali pa uporabimo `new \DateTime`, da dobimo trenutno datum in čas. Uporabite metodo `format()` za pretvorbo DateTime nazaj
v niz za izpis.
{% highlight php %}
<?php
$raw = '22. 11. 1968';
$start = \DateTime::createFromFormat('d. m. Y', $raw);

echo 'Start date: ' . $start->format('m/d/Y') . "\n";
{% endhighlight %}

Računanje z DateTime je možno s pomočjo razreda DateInterval. DateTime ima metode, kot so `add()` in `sub()`, ki
sprejmejo DateInterval kot argument. Ne pišite kode, ki pričakuje enako število sekund v vsakem dnevu, saj bosta tako
poletni čas in spreminjanje časovnih območij pokvarila to predpostavko. Namesto tega uporabite intervale datumov. Za izračun
sprememb datuma uporabite metodo `diff()`. Vrnila bo nov DateInterval, ki je izjemno enostaven za prikaz.
{% highlight php %}
<?php
// create a copy of $start and add one month and 6 days
$end = clone $start;
$end->add(new \DateInterval('P1M6D'));

$diff = $end->diff($start);
echo 'Difference: ' . $diff->format('%m month, %d days (total: %a days)') . "\n";
// Difference: 1 month, 6 days (total: 37 days)
{% endhighlight %}

Na DateTime objektih lahko uporabite standardne primerjave:
{% highlight php %}
<?php
if ($start < $end) {
    echo "Start is before end!\n";
}
{% endhighlight %}

Zadnji primer demonstrira razred DatePeriod. Uporabljen je za iteracijo nad ponavljajočimi se dogodki. Vzame lahko dva
DateTime objekta, začetek in konec ter interval za katerega vrne vse vmesne dogodke.
{% highlight php %}
<?php
// output all thursdays between $start and $end
$periodInterval = \DateInterval::createFromDateString('first thursday');
$periodIterator = new \DatePeriod($start, $periodInterval, $end, \DatePeriod::EXCLUDE_START_DATE);
foreach ($periodIterator as $date) {
    // output each date in the period
    echo $date->format('m/d/Y') . ' ';
}
{% endhighlight %}

* [Preberite o DateTime][datetime]
* [Preberite o oblikovanju datuma][dateformat] (sprejete opcije niza oblikovanja datuma)

[datetime]: http://www.php.net/manual/book.datetime.php
[dateformat]: http://www.php.net/manual/function.date.php
