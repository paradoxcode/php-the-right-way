---
title:   CLI - vmesnik komandne vrstice
isChild: true
---

## CLI - vmesnik komandne vrstice {#command_line_interface_title}

PHP je bil v osnovi narejen za ustvarjanje spletnih aplikacij, vendar je tudi uporaben za skriptiranje programov vmesnika komandne vrstice (CLI - command line interface). PHP programi za ukazno vrstico vam lahko pomagajo avtomatizirati pogoste naloge, kot so testiranje, nalaganje in administriranje aplikacije.

CLI PHP programi so zmogljivi, ker lahko uporabite kodo vaše aplikacije direktno brez potrebe po ustvarjanju in zavarovanju spletnega GUI-ja zanjo. Bodite samo prepričani, da ne date vaše PHP CLI skripte v vaš javni spletni direktorij!

Poskusite pognati PHP iz komandne vrstice:

{% highlight bash %}
> php -i
{% endhighlight %}

Opcija `-i` bo izpisala vašo PHP konfiguracijo tako kot funkcija [`phpinfo`][phpinfo].

Opcija `-a` ponuja interaktivno lupino, podobno kot Ruby-jev IRB ali Pythonova interaktivna lupina. Na voljo je še mnogo ostalih uporabnih [opcij ukazne vrstice][cli-options].

Napišimo preprost "Hello, $name" CLI program. Da ga preizkusite, ustvarite datoteko poimenovano `hello.php`, tako kot je prikazano spodaj.

{% highlight php %}
<?php
if ($argc != 2) {
    echo "Usage: php hello.php [name].\n";
    exit(1);
}
$name = $argv[1];
echo "Hello, $name\n";
{% endhighlight %}

PHP priredi dve posebni spremenljivki, ki temeljita na podanih argumentih pri pogonu vaše skripte. [`$argc`][argc] je celo številska spremenljivka, ki vsebuje argument *count*, in [`$argv`][argv] je spremenljivka tipa polje, ki vsebuje *vrednost* vsakega argumenta. Prvi argument je vedno ime vaše PHP skriptne datoteke, v tem primeru `hello.php`.

Izraz `exit()` je uporabljen s številko različno od nič, da omogoči lupini vedeti, da je ukaz spodletel. Pogosto uporabljene exit kode je moč najti [tu][exit-codes].

Za pogon naše skripte zgoraj iz komandne vrstice:

{% highlight bash %}
> php hello.php
Usage: php hello.php [name]
> php hello.php world
Hello, world
{% endhighlight %}


 * [Naučite se o poganjanju PHP-ja iz ukazne vrstice][php-cli]
 * [Naučite se o nastavitvi Windows okolja za poganjanje PHP-ja iz ukazne vrstice][php-cli-windows]

[phpinfo]: http://php.net/manual/en/function.phpinfo.php
[cli-options]: http://www.php.net/manual/en/features.commandline.options.php
[argc]: http://php.net/manual/en/reserved.variables.argc.php
[argv]: http://php.net/manual/en/reserved.variables.argv.php
[php-cli]: http://php.net/manual/en/features.commandline.php
[php-cli-windows]: http://www.php.net/manual/en/install.windows.commandline.php
[exit-codes]: http://www.gsp.com/cgi-bin/man.cgi?section=3&topic=sysexits
