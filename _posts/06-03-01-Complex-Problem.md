---
title:   Kompleksni problem
isChild: true
anchor: complex_problem
---

## Kompleksni problem {#complex_problem_title}

Če ste kdarkoli brali o injiciranju odvisnosti, potem ste verjeno videli termine *"Inversion of Control"* ali *"Dependency Inversion Principle"*.
To so kompleksni problemi, ki jih injiciranje odvisnosti rešuje.

### Inverzija kontrole

Inverzija kontrole je, kot pove, "obračanje kontrole" sistema z obdržanjem organizacijske kontrole v celoti ločene od naših objektov.
V terminih injiciranja odvisnosti to pomeni rahljanje naših odvisnosti s kontroliranjem in njihovo instantizacijo drugje v sistemu.

Že leta so PHP ogrodja dosegala inverzijo kontrole, vendar vprašanje je postalo, kateri del kontrole
obračate in kam? Na primer, MVC ogrodja bi običajno podala super objekt ali osnovni krmilnik, ki ga morajo ostali
krmilniki razširiti, da pridobijo dostop do svojih odvisnosti. To **je** inverzija kontrole, čeprav namesto rahljanja
odvisnosti, jih ta metoda enostavno premakne.

Injiciranje odvisnosti nam omogoča bolj elegantno rešiti ta problem s samo injiciranjem odvisnosti, ki jih potrebujemo, ko jih potrebujemo,
brez potrebe za kakršnekoli vkodirane odvisnosti.

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
