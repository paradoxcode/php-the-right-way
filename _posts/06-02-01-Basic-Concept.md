---
title:   Osnovni koncept
isChild: true
anchor:  basic_concept
---

## Osnovni koncept {#basic_concept_title}

Koncept lahko demonstriramo z enostavnim in naivnim primerom.

Imamo razred `Database`, ki zahteva, da adapter komunicira s podatkovno bazo. Instanco adapterja
naredimo v konstruktorju in izdelamo zahtevno odvisnost. To naredi testiranje težko in pomeni, da je razred `Database`
zelo tesno povezan v adapter.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct()
    {
        $this->adapter = new MySqlAdapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

To kodo je mogoče refaktorirati, da uporablja injiciranje odvisnosti in zato naredi odvisnost ohlapnejšo.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct(MySqlAdapter $adapter)
    {
        $this->adapter = $adapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

Sedaj dajemo razredu `Database` njegovo odvisnost namesto, da jo naredi sam. Lahko naredimo celo metodo,
ki bi sprejela argument odvisnosti in ga nastavila na ta način, ali če bi bila lastnost `$adapter` `public`, bi ga lahko
nastavili direktno.
