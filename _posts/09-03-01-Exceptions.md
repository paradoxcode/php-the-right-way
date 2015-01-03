---
title:   Izjeme
isChild: true
anchor:  exceptions
---

## Izjeme {#exceptions_title}

Izjeme (Exceptions) so standardni deli najbolj popularnih programskih jezikov, vendar so pogosto spregledani s strani PHP programerjev.
Jeziki kot je Ruby so izjemno zapolnjeni z izjemami, tako da kadarkoli gre kaj narobe, kot npr. okvara zahtevka HTTP, ali
okvara pri poizvedbi podatkovne baze, ali celo ko slikovnega stredstva ni mogoče najti, Ruby (ali uporabljeni gemi) bodo izpisali
izjemo na zaslon, kar pomeni, da takoj veste, kje se nahaja napaka.

PHP sam po sebi ima precej pomanjkanja glede tega in klic `file_get_contents()` vam bo ponavadi vrnil `FALSE` in opozorilo.
Mnoga starejša ogrodja, kot je na primer CodeIgniter, bodo vrnila samo false vrednost, zapis sporočila v dnevnik in mogoče
vam omogočila uporabo metode, kot je `$this->upload->get_error()`, da lahko vidite, kaj je šlo narobe. Problem tu je, da
morate iskati napako in preverjati dokumentacijo, za katero napako metode gre za določen razred, namesto da se to naredi
izjemno očitno.

Naslednji problem je, ko razredi avtomatsko vržejo napako na zaslon in zapustijo proces. Ko naredite to, ustavite drugega
razvijalca, da bi lahko dinamično ravnal s to napako. Izjeme bi morale biti zagnane, da opozorijo razvijalca pred napako.
Nato le-ta lahko izbere, kako bo ravnal v tem primeru. Primer:

{% highlight php %}
<?php
$email = new Fuel\Email;
$email->subject('My Subject');
$email->body('How the heck are you?');
$email->to('guy@example.com', 'Some Guy');

try
{
    $email->send();
}
catch(Fuel\Email\ValidationFailedException $e)
{
    // The validation failed
}
catch(Fuel\Email\SendingFailedException $e)
{
    // The driver could not send the email
}
finally
{
    // Use this to let user know email was sent
}
{% endhighlight %}

### SPL izjeme

Generični `Exception` razred ponuja zelo malo konteksta razhroščevanja za razvijalca, čeprav za odpravo tega je
mogoče narediti specializiran `Exception` tip s pomočjo pod-razreda generičnega `Exception` razreda:

{% highlight php %}
<?php
class ValidationException extends Exception {}
{% endhighlight %}

To pomeni, da lahko dodate več catch blokov in upravljate z različnimi izjemami različno. To lahko vodi v
ustvarjanje <em>veliko</em> izjem po meri, nekaterim med njimi se lahko izognete z uporabo SPL izjem, ki so na voljo
v [SPL razširitvi][splext]. 

Če na primer uporabite `__call()` magično metodo in je nato zahtevana napačna metoda, se namesto zagona standardne izjeme
`Exception`, ki je nejasna, ali ustvarjanja izjeme po meri samo za to, lahko samo zaženete `throw new BadMethodCallException;`.

* [Preberite o izjemah][exceptions]
* [Preberite o SPL izjemah][splexe]
* [Gnezdenje izjem v PHP][nesting-exceptions-in-php]
* [Najboljše prakse izjem v PHP 5.3][exception-best-practices53]

[exceptions]: http://php.net/language.exceptions
[splexe]: http://php.net/spl.exceptions
[splext]: /#standardna_php_knjižnica
[exception-best-practices53]: http://ralphschindler.com/2010/09/15/exception-best-practices-in-php-5-3
[nesting-exceptions-in-php]: http://www.brandonsavage.net/exceptional-php-nesting-exceptions-in-php/
