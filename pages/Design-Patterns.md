---
layout: page
title:  Načtrovalski vzorci
---

# Načrtovalski vzorci

Obstaja mnogo načinov za strukturiranje kode in projekta za vašo spletno aplikacijo in v to lahko vložite ogromno ali pa
malo premisleka v arhitekturo. Vendar je ponavadi dobra ideja, da se sledi pogostim vzorcem, ker bo vašo
kodo naredilo enostavnejšo za upravljanje in enostavnejšo drugim za razumevanje.

* [Arhitekturni vzorci na Wikipediji](https://en.wikipedia.org/wiki/Architectural_pattern)
* [Načrtovalski vzorci programske opreme na Wikipediji](https://en.wikipedia.org/wiki/Software_design_pattern)
* [Zbirka primerov implementacij](https://github.com/domnikl/DesignPatternsPHP)

## Tovarna

Eden najpogosteje uporabljanih načrtovalskih vzorcev je vzorec tovarne. V tem vzorcu razred enostavno naredi objekt,
ki ga želite uporabiti. Premislite o sledečem primeru vzorca tovarne:

{% highlight php %}
<?php
class Automobile
{
    private $vehicleMake;
    private $vehicleModel;

    public function __construct($make, $model)
    {
        $this->vehicleMake = $make;
        $this->vehicleModel = $model;
    }

    public function getMakeAndModel()
    {
        return $this->vehicleMake . ' ' . $this->vehicleModel;
    }
}

class AutomobileFactory
{
    public static function create($make, $model)
    {
        return new Automobile($make, $model);
    }
}

// have the factory create the Automobile object
$veyron = AutomobileFactory::create('Bugatti', 'Veyron');

print_r($veyron->getMakeAndModel()); // outputs "Bugatti Veyron"
{% endhighlight %}

Ta koda uporablja tovarno za izdelavo objekta Automobile. Na voljo sta dve možni prednosti za gradnjo vaše kode po
tej poti; prva je, da če potrebujete naknadno spremeniti, preimenovati ali zamenjati razred Automobile, lahko to storite
samo s spremembo kode v tovarni, namesto na vsakem mestu v vašem projektu, ki uporablja razred Automobile.
Druga možna prednost je, da če je izdelava objekta komplicirano opravilo, lahko vso delo opravite v tovarni namesto
ponavljanja vsakokrat, ko želite narediti novo instanco.

Uporaba tovarniškega vzorca ni vedno potrebna (ali pametna). Primer kode uporabljene tu je tako enostavna, da bi bila
tovarna enostavno dodajanje nepotrebne kompleksnosti. Vendar če izdelujete dokaj velik ali kompleksen projekt, si lahko
prihranite precej težav na poti z uporabo tovarn.

* [Tovarniški vzorec na Wikipediji](https://en.wikipedia.org/wiki/Factory_pattern)

## Enojni vzorec (singleton)

Ko se načrtuje spletne aplikacije, je pogosto smiselno konceptualno in arhitekturno dovoliti dostop do ene in
samo ene instance določenega razreda. To nam omogoči narediti enojni vzorec.

{% highlight php %}
<?php
class Singleton
{
    /**
     * Returns the *Singleton* instance of this class.
     *
     * @staticvar Singleton $instance The *Singleton* instances of this class.
     *
     * @return Singleton The *Singleton* instance.
     */
    public static function getInstance()
    {
        static $instance = null;
        if (null === $instance) {
            $instance = new static();
        }

        return $instance;
    }

    /**
     * Protected constructor to prevent creating a new instance of the
     * *Singleton* via the `new` operator from outside of this class.
     */
    protected function __construct()
    {
    }

    /**
     * Private clone method to prevent cloning of the instance of the
     * *Singleton* instance.
     *
     * @return void
     */
    private function __clone()
    {
    }

    /**
     * Private unserialize method to prevent unserializing of the *Singleton*
     * instance.
     *
     * @return void
     */
    private function __wakeup()
    {
    }
}

class SingletonChild extends Singleton
{
}

$obj = Singleton::getInstance();
var_dump($obj === Singleton::getInstance());             // bool(true)

$anotherObj = SingletonChild::getInstance();
var_dump($anotherObj === Singleton::getInstance());      // bool(false)

var_dump($anotherObj === SingletonChild::getInstance()); // bool(true)
{% endhighlight %}

Koda zgoraj implementira enojni vzorec z uporabo [*statične* spremenljivke](http://php.net/language.variables.scope#language.variables.scope.static) in statične izdelovalne metode `getInstance()`.
Upoštevajte sledeče:

* Konstruktor [`__construct`](http://php.net/language.oop5.decon#object.construct) je deklarirana kot 'protected', da prepreči novo instanco izven razreda preko operatorja `new`.
* Magična metoda [`__clone`](http://php.net/language.oop5.cloning#object.clone) je deklarirana kot 'private', da prepreči kloniranje instance razreda preko operatorja [`clone`](http://php.net/language.oop5.cloning).
* Magična metoda [`__wakeup`](http://php.net/language.oop5.magic#object.wakeup) je deklarirana kot 'private', da prepreči deserializacijo instance razreda preko globalne funkcije [`unserialize()`](http://php.net/function.unserialize).
* Nova instanca je narejena preko t.i. ["late static binding"](http://php.net/language.oop5.late-static-bindings) v statični metodi izdelave `getInstance()` s ključno besedo `static`. To omogoča podrazredenje razreda `Singleton` v primeru.

Enojni vzorec je uporaben, ko moramo zagotoviti, da imamo samo enojno instanco razreda za celoten cikel zahtevka v
spletni aplikaciji. To se običajno zgodi, ko imamo globalne objekte (kot je razred 'Configuration') ali deljeni vir
(kot je čakalna vrsta dogodkov).

Morate paziti, ko uporabljate enojni vzorec, saj po svoji naravi uvede globalno stanje v vašo aplikacijo, kar zmanjša
možnost testiranja. V večini primerov, injiciranje odvisnosti je lahko (in bi moralo) biti uporabljeno na mestu
enojnega razreda. Uporaba injiciranja odvisnosti pomeni, da ne uvajamo nepotrebnih skupkov v načrt naše aplikacije,
saj objekt, ki uporablja deljeni ali globalni vir, ne potrebuje znanja o konkretno definiranem razredu.

* [Enojni razred na Wikipediji](https://en.wikipedia.org/wiki/Singleton_pattern)

## Strategija

S strateškim vzorcem zaobjamete specifične družine algoritmov, kar dovoljuje klientnem razredu, ki je odgovoren za
instantizacijo določenega algoritma, da nima znanja aktualne implementacije. Na voljo je nekaj variacij strateškega
vzorca, najenostavnejši je izpostavljen spodaj:

Prvi odrezek kode orisuje družino algoritmov; morda želite serializirano polje, nekaj JSON ali morda
samo polje podatkov:
{% highlight php %}
<?php

interface OutputInterface
{
    public function load();
}

class SerializedArrayOutput implements OutputInterface
{
    public function load()
    {
        return serialize($arrayOfData);
    }
}

class JsonStringOutput implements OutputInterface
{
    public function load()
    {
        return json_encode($arrayOfData);
    }
}

class ArrayOutput implements OutputInterface
{
    public function load()
    {
        return $arrayOfData;
    }
}
{% endhighlight %}

Z zaobjemom zgornjega algoritma ga delate lepega in čistega v vaši kodi, da ostali razvijalci lahko enostavno
dodajo nove izhodne tipe brez vplivanja na kodo klienta.

Videli boste, kako vsak konkreten 'output' razred izvede OutputInterface - to ima dvojen namen, primarno
ponuja enostavno naročilo, katero mora biti ubogano s strani katerekoli nove konkretne izvedbe. Drugič, z
implementacijo pogostega vmesnika boste videli v naslednji sekciji, da lahko sedaj uporabite t.i. [Type Hinting](http://php.net/language.oop5.typehinting),
da zagotovite, da je klient, ki je uporabil ta vedenja, pravilnega tipa, v tem primeru 'OutputInterface'.

Naslednji odrezek kode opisuje, kako klic razreda klienta lahko uporabi enega teh algoritmon ali celo boljše nastavi
zahtevano vedenje pri izvajanju:
{% highlight php %}
<?php
class SomeClient
{
    private $output;

    public function setOutput(OutputInterface $outputType)
    {
        $this->output = $outputType;
    }

    public function loadOutput()
    {
        return $this->output->load();
    }
}
{% endhighlight %}

Razred klienta, ki kliče zgoraj ima privatno lastnost, ki mora biti nastavljena pri izvajanju in biti tipa 'OutputInterface',
ko je enkrat ta lastnost nastavljena, bo klic loadOutput() poklical metodo load() v konkretnem razredu izhodnega tipa, ki je bil
nastavljen.
{% highlight php %}
<?php
$client = new SomeClient();

// Want an array?
$client->setOutput(new ArrayOutput());
$data = $client->loadOutput();

// Want some JSON?
$client->setOutput(new JsonStringOutput());
$data = $client->loadOutput();

{% endhighlight %}

* [Streteški vzorec na Wikipediji](http://en.wikipedia.org/wiki/Strategy_pattern)

## Sprednji krmilnik

Vzorec sprednjega krmilnika je, kjer imate enojno vstopno točko za vašo spletno aplikacijo (na primer index.php), ki
ravna vse zahtevke. Ta koda je odgovorna za nalaganje vseh odvisnosti, ki obdelujejo zahtevek in pošiljajo odziv brskalniku.
Vzorec sprednjega krmilnika je lahko koristen, ker spodbuja modularno kodo in vam ponuja centralni prostor za povezavo
kode, ki bi morala biti gnana za vsak request (kot je čiščenje vnosa).

* [Vzorec sprednjega krmilnika na Wikipediji](https://en.wikipedia.org/wiki/Front_Controller_pattern)

## Model-pogled-krmilnik (MVC)

Vzorec model-pogled-krmilnik (MVC - Model-View-Controller) in njegova sorodna HMVC in MVVM vam omogočata zlom kode v logične objekte, ki
služijo zelo specifičnim razlogom. Modeli služijo kot plast podatkovnega dostopa, kjer so podatki pridobljeni in vrnjeni v obliki
uporabni skozi vašo aplikacijo. Krmilniki upravljajo zahtevek, obdelujejo podatke vrnjene iz modela in nalagajo poglede, da
pošljejo odziv. In pogledi so prikazane predloge (markup, xml itd), ki so poslani v odzivu spletnemu brskalniku.

MVC je najbolj pogost arhitekturni vzorec uporabljen v popularnih [PHP ogrodjih](https://github.com/codeguy/php-the-right-way/wiki/Frameworks).

Naučite se več o MVC in njegovih sorodnih vzorcih:

* [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller)
* [HMVC](https://en.wikipedia.org/wiki/Hierarchical_model%E2%80%93view%E2%80%93controller)
* [MVVM](https://en.wikipedia.org/wiki/Model_View_ViewModel)
