---
title:   Kompleksni problem
isChild: true
anchor:  complex_problem
---

## Kompleksni problem {#complex_problem_title}

Če ste kdarkoli brali o injiciranju odvisnosti, potem ste verjeno videli izraz
*"Inversion of Control"* ali *"Dependency Inversion Principle"*. To so
kompleksni problemi, ki jih injiciranje odvisnosti rešuje.

### Inverzija kontrole

Inverzija kontrole je, kot pove, "obračanje kontrole" sistema z obdržanjem
organizacijske kontrole v celoti ločene od naših objektov. V terminih
injiciranja odvisnosti to pomeni rahljanje naših odvisnosti s kontroliranjem in
njihovo instantizacijo drugje v sistemu.

Že leta so PHP ogrodja dosegala inverzijo kontrole, vendar vprašanje je postalo,
kateri del kontrole obračate in kam? Na primer, MVC ogrodja bi običajno podala
super objekt ali osnovni krmilnik, ki ga morajo ostali krmilniki razširiti, da
pridobijo dostop do svojih odvisnosti. To **je** inverzija kontrole, čeprav
namesto rahljanja odvisnosti, jih ta metoda enostavno premakne.

Injiciranje odvisnosti nam omogoča bolj elegantno rešiti ta problem s samo
injiciranjem odvisnosti, ki jih potrebujemo, ko jih potrebujemo, brez potrebe za
kakršnekoli vkodirane odvisnosti.

### S.O.L.I.D.

#### Single Responsibility Principle

The Single Responsibility Principle is about actors and high-level architecture. It states that “A class should have
only one reason to change.” This means that every class should _only_ have responsibility over a single part of the
functionality provided by the software. The largest benefit of this approach is that it enables improved code
_reusability_. By designing our class to do just one thing, we can use (or re-use) it in any other program without
changing it.

#### Open/Closed Principle

The Open/Closed Principle is about class design and feature extensions. It states that “Software entities (classes,
modules, functions, etc.) should be open for extension, but closed for modification.” This means that we should design
our modules, classes and functions in a way that when a new functionality is needed, we should not modify our existing
code but rather write new code that will be used by existing code. Practically speaking, this means that we should write
classes that implement and adhere to _interfaces_, then type-hint against those interfaces instead of specific classes.

The largest benefit of this approach is that we can very easily extend our code with support for something new without
having to modify existing code, meaning that we can reduce QA time, and the risk for negative impact to the application
is substantially reduced. We can deploy new code, faster, and with more confidence.

#### Liskov Substitution Principle

The Liskov Substitution Principle is about subtyping and inheritance. It states that “Child classes should never break
the parent class’ type definitions.” Or, in Robert C. Martin’s words, “Subtypes must be substitutable for their base
types.”

For example, if we have a `FileInterface` interface which defines an `embed()` method, and we have `Audio` and `Video`
classes which both implement the `FileInterface` interface, then we can expect that the usage of the `embed()` method will always
do the thing that we intend. If we later create a `PDF` class or a `Gist` class which implement the `FileInterface`
interface, we will already know and understand what the `embed()` method will do. The largest benefit of this approach
is that we have the ability to build flexible and easily-configurable programs, because when we change one object of a
type (e.g., `FileInterface`) to another we don't need to change anything else in our program.

#### Interface Segregation Principle

The Interface Segregation Principle (ISP) is about _business-logic-to-clients_ communication. It states that “No client
should be forced to depend on methods it does not use.” This means that instead of having a single monolithic interface
that all conforming classes need to implement, we should instead provide a set of smaller, concept-specific interfaces
that a conforming class implements one or more of.

For example, a `Car` or `Bus` class would be interested in a `steeringWheel()` method, but a `Motorcycle` or `Tricycle`
class would not. Conversely, a `Motorcycle` or `Tricycle` class would be interested in a `handlebars()` method, but a
`Car` or `Bus` class would not. There is no need to have all of these types of vehicles implement support for both
`steeringWheel()` as well as `handlebars()`, so we should break-apart the source interface.

### Princip inverzije odvisnosti

Princip inverzije odvisnosti (dependency Injection Principle) je "D" v S.O.L.I.D. skupku objekta orientiranih načrtovalskih principov, ki
pravijo, da bi moralo biti *"odvisno od abstrakcije. Ne zanašano na konkretizacijo."* Dano enostavno to pomeni, da naše odvisnosti bi morale biti
vmesniki/vezave ali abstraktni razredi namesto konkretne implementacije. Lahko enostavno refkatoriramo zgornji primer, da sledi temu principu.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct(AdapterInterface $adapter)
    {
        $this->adapter = $adapter;
    }
}

interface AdapterInterface {}

class MysqlAdapter implements AdapterInterface {}
{% endhighlight %}

Na voljo je nekaj koristi od razreda `Database`, ki je sedaj odvisen od vmesnika namesto od konkretizacije.

Zamislite si, da delate v ekipi in na adapterju dela kolega. V našem prvem primeru, bi morali čakati
omenjenega kolega, da konča adapter preden ga lahko ustrezno preizkusimo za naše teste enot. Sedaj, ko je odvisnost
vmesnik/vezava lahko veselo preizkusimo ta vmesnik in vemo, da bo naš kolega zgradil adapter na osnovi te vezave.

Še večja korist te metode je, da je sedaj naša koda bolj skalabilna. Če se leto dni kasneje odličimo, da se
želimo preseliti na drug tip podatkovne baze, lahko napišemo adapter, ki implementira originalni vmesnik in namesto tega to injicira,
nič več refaktoringa ne bi bilo potrebnega, saj lahko zagotovimo, da adapter sledi vezavi nastavljeni s strani vmesnika.
