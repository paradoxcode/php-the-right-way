---
layout: page
title: Načtrovalski vzorci
---

# Načrtovalski vzorci

Obstaja mnogo načinov za strukturiranje kode in projekta za vašo spletno aplikacijo in v to lahko vložite ogromno ali pa
malo premisleka kot ga želite v arhitekturo. Vendar je ponavadi dobra ideja, da se sledi pogostim vzorcem, ker bo vašo
kodo naredilo enostavnejšo za upravljanje in enostavnejšo drugim za razumevanje.

* [Arhitekturni vzorci na Wikipediji](https://en.wikipedia.org/wiki/Architectural_pattern)
* [Načrtovalski vzorci programske opreme na Wikipediji](https://en.wikipedia.org/wiki/Software_design_pattern)

## Tovarna

Eden najpogosteje uporabljanih načrtovalskih vzorcev je vzorec tovarne. V tem vzorcu razred enostavno naredi objekt,
ki ga želite uporabiti. Premislite o sledečem primeru vzorca tovarne:

{% highlight php %}
<?php
class Automobile
{
    private $vehicle_make;
    private $vehicle_model;

    public function __construct($make, $model)
    {
        $this->vehicle_make = $make;
        $this->vehicle_model = $model;
    }

    public function get_make_and_model()
    {
        return $this->vehicle_make . ' ' . $this->vehicle_model;
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

print_r($veyron->get_make_and_model()); // outputs "Bugatti Veyron"
{% endhighlight %}

Ta koda uporablja tovarno za izdelavo objekta Automobile. Na voljo sta dve možni prednosti za gradnjo vaše kode po
tej poti. Prva je, da če potrebujete naknadno spremeniti, preimenovati ali zamenjati razred Automobile, lahko to storite
in morali boste samo spremeniti kodo v tovarni, namesto na vsakem mestu v vašem projektu, ki uporablja razred Automobile.
Druga možna prednost je, da če je izdelava objekta komplicirano opravilo, lahko vso delo opravite v tovarni, namesto
ponavljanja vsakokrat, ko želite narediti novo instanco.

Uporaba tovarniškega vzorca ni vedno potrebna (ali pametna). Primer kode uporabljene tu je tako enostavna, da bi bila
tovarna enostavno dodajanje nepotrebne kompleksnosti. Vendar če izdelujete dokaj velik ali kompleksen projekt, si lahko
prihranite precej težav na poti z uporabo tovarn.

* [Tovarniški vzorec na Wikipediji](https://en.wikipedia.org/wiki/Factory_pattern)

## Singleton

When designing web applications, it often makes sense conceptually and architecturally to allow access to one and
only one instance of a particular class. The singleton pattern enables us to do this.

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

The code above implements the singleton pattern using a [*static* variable](http://php.net/language.variables.scope#language.variables.scope.static) and the static creation method `getInstance()`.
Note the following:

* The constructor [`__construct`](http://php.net/language.oop5.decon#object.construct) is declared as protected to prevent creating a new instance outside of the class via the `new` operator.
* The magic method [`__clone`](http://php.net/language.oop5.cloning#object.clone) is declared as private to prevent cloning of an instance of the class via the [`clone`](http://php.net/language.oop5.cloning) operator.
* The magic method [`__wakeup`](http://php.net/language.oop5.magic#object.wakeup) is declared as private to prevent unserializing of an instance of the class via the global function [`unserialize()`](http://php.net/function.unserialize).
* A new instance is created via [late static binding](http://php.net/language.oop5.late-static-bindings) in the static creation method `getInstance()` with the keyword `static`. This allows the subclassing of the class `Singleton` in the example.

The singleton pattern is useful when we need to make sure we only have a single instance of a class for the entire
request lifecycle in a web application. This typically occurs when we have global objects (such as a Configuration
class) or a shared resource (such as an event queue).

You should be wary when using the singleton pattern, as by its very nature it introduces global state into your
application, reducing testability. In most cases, dependency injection can (and should) be used in place of a
singleton class. Using dependency injection means that we do not introduce unnecessary coupling into the design of our
application, as the object using the shared or global resource requires no knowledge of a concretely defined class.

* [Singleton pattern on Wikipedia](https://en.wikipedia.org/wiki/Singleton_pattern)

## Streategija

With the strategy pattern you encapsulate specific families of algorithms allowing the client class responsible for 
instantiating a particular algorithm to have no knowledge of the actual implementation.
There are several variations on the strategy pattern, the simplest of which is outlined below:

This first code snippet outlines a family of algorithms; you may want a serialized array, some JSON or maybe 
just an array of data:
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

By encapsulating the above algorithms you are making it nice and clear in your code that other developers can easily 
add new output types without affecting the client code.

You will see how each concrete 'output' class implements an OutputInterface - this serves two purposes, primarily it
provides a simple contract which must be obeyed by any new concrete implementations. Secondly by implementing a common
interface you will see in the next section that you can now utilise [Type Hinting](http://php.net/manual/en/language.oop5.typehinting.php) to ensure that the client which is utilising these behaviours is of the correct type in
this case 'OutputInterface'.

The next snippet of code outlines how a calling client class might use one of these algorithms and even better set the
behaviour required at runtime:
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

The calling client class above has a private property which must be set at runtime and be of type 'OutputInterface'
once this property is set a call to loadOutput() will call the load() method in the concrete class of the output type
that has been set.
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

* [Strategy pattern on Wikipedia](http://en.wikipedia.org/wiki/Strategy_pattern)

## Front Controller

The front controller pattern is where you have a single entrance point for you web application (e.g. index.php) that
handles all of the requests. This code is responsible for loading all of the dependencies, processing the request and
sending the response to the browser. The front controller pattern can be beneficial because it encourages modular code
and gives you a central place to hook in code that should be run for every request (such as input sanitization).

* [Front Controller pattern on Wikipedia](https://en.wikipedia.org/wiki/Front_Controller_pattern)

## Model-View-Controller

The model-view-controller (MVC) pattern and its relatives HMVC and MVVM let you break up code into logical objects that
serve very specific purposes. Models serve as a data access layer where data is fetched and returned in formats usable
throughout your application. Controllers handle the request, process the data returned from models and load views to
send in the response. And views are display templates (markup, xml, etc) that are sent in the response to the web
browser.

MVC is the most common architectural pattern used in the popular [PHP frameworks](https://github.com/codeguy/php-the-right-way/wiki/Frameworks).

Learn more about MVC and its relatives:

* [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller)
* [HMVC](https://en.wikipedia.org/wiki/Hierarchical_model%E2%80%93view%E2%80%93controller)
* [MVVM](https://en.wikipedia.org/wiki/Model_View_ViewModel)
