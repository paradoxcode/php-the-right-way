---
isChild: true
title: Interakcija s podatkovnimi bazami
anchor: databases_interacting
---

## Interakcija s podatkovnimi bazami

Ko se razvijalci prvič pričnejo učiti PHP, pogosto končajo z mešanjem njihovih interakcij s podatkovnimi bazami z njihovo
predstavitveno logiko, z uporabo kode, ki izgleda nekako tako:

{% highlight php %}
<ul>
<?php
foreach ($db->query('SELECT * FROM table') as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>";
}
</ul>
{% endhighlight %}

To je slaba praksa zaradi vseh vrst razlogov, v glavnem ker je težko razhroščevati, težko testirati, težko brati in izpisalo bo veliko polj, če tam ne postavite
omejitve.

Medtem ko obstoja veliko ostalih rešitev za to - odvisno od tega, če imate raje [OOP](/#object-oriented-programming) ali [funkcijsko programiranje](/#functional-programming) - mora biti nek element ločitve.

Premislite o najbolj osnovnem koraku:

{% highlight php %}
<?php
function getAllSomethings($db) {
    return $db->query('SELECT * FROM table');
}

foreach (getAllFoos() as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>"; // BAD!!
}
{% endhighlight %}

To je dober začetek. Dajte ta dva elementa v dve različni datoteki in imate nekoliko čisto ločitev.

Izdelajte razred, kamor date to metodo in imate "Model". Izdelajte enostavno `.php` datoteko, kamor date predstavitveno logiko in imate "View", kar je zelo blizu [MVC] - skupni OOP arhitekturi za večino [ogrodij](/#frameworks_title).

**foo.php**

{% highlight php %}
<?php

$db = new PDO('mysql:host=localhost;dbname=testdb;charset=utf8', 'username', 'password');

// Make your model available
include 'models/FooModel.php';

// Create an instance
$fooList = new FooModel($db);

// Show the view
include 'views/foo-list.php';
{% endhighlight %}


**models/FooModel.php**

{% highlight php %}
<?php
class Foo()
{
    protected $db;

    public function __construct(PDO $db)
    {
        $this->db = $db;
    }

    public function getAllFoos() {
        return $this->db->query('SELECT * FROM table');
    }
}
{% endhighlight %}

**views/foo-list.php**

{% highlight php %}
<? foreach ($fooList as $row): ?>
    <?= $row['field1'] ?> - <?= $row['field1'] ?>
<? endforeach ?>
{% endhighlight %}

To je v bistvu enako, kar počne večina modernih ogrodij, vse to bolj ročno. Lahko
ne boste potrebovali narediti vsega tega vsakokrat, vendar mešanje skupaj preveč predstavitvene logike in interakcij s podatkovno bazo je lahko pravi problem, če kadarkoli želite narediti [teste enot](/#unit-testing) za vašo aplikacijo.

[PHPBridge] ima odličen vir imenovan [Izdelava podatkovnega razreda - Data Class], ki pokriva precej podobno temo in je odličen
za razvijalce, ki so se ravnokar navadili na koncept interakcije s podatkovno bazo.

[MVC]: http://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488
[PHPBridge]: http://phpbridge.org/
[Izdelava podatkovnega razreda - Creating a Data Class]: http://phpbridge.org/intro-to-php/creating_a_data_class
