---
title: Podatkovne baze
anchor: databases
---

# Podatkovne baze {#databases_title}

Mnogokrat bo vaša PHP koda uporabila podatkovno bazo za pridobivanje informacij. Na voljo imate nekaj opcij za povezavo in interakcijo
z vašo podatkovno bazo. Priporočena opcija **do PHP 5.1.0** je bila uporaba originalnih gonilnikov kot so [mysqli], [pgsql], [mssql] itd.

Originalni gonilniki so odlični, če uporabljate samo _eno_ podatkovno bazo v vaši aplikaciji, vendar če na primer uporabljate MySQL in nekaj MSSQL hkrati,
ali se potrebujete povezati na Oracle podatkovno bazo, potem ne boste mogli uporabiti istih gonilnikov. Naučiti se boste morali popolnoma nov API za vsako
podatkovno bazo &mdash; in to lahko postane neumno.

## MySQL extension

Razširitev [mysql] za PHP ni več v aktivnem razvoju in je [uradno opuščena od PHP 5.5.0], kar pomeni, da bo
odstranjena znotraj nekaj naslednjih izdaj. Če uporabljate katerekoli funkcije, ki se začnejo z `mysql_*`
kot sta `mysql_connect()` in `mysql_query()` v vaših aplikacijah, potem le te enostavno ne bodo na voljo v kasnejših verzijah PHP. To pomeni, da se boste v srečali s prepisovanjem, torej je najboljša opcija zamenjava mysql uporabe
z [mysqli] ali [PDO] v vaših aplikacijah znotraj vašega razvojnega časovnega načrta, tako da se vam ne bo mudilo kasneje. **Če pričenjate od začetka potem vsekakor ne
uporabite [mysql] razširitve: uporabite [MySQLi razširitev][mysqli], ali uporabite [PDO].**

* [PHP: Izbira API-ja za MySQL](http://php.net/manual/en/mysqlinfo.api.choosing.php)
* [PDO Tutorial for MySQL Developers](http://wiki.hashphp.org/PDO_Tutorial_for_MySQL_Developers)

## PDO razširitev

[PDO] je abstraktna knjižnica povezovanja podatkovne baze &mdash; vgrajen v PHP od 5.1.0 &mdash;, ki ponuja enoten vmesnik za komunikacijo z
mnogimi različnimi podatkovnimi bazami. Na primer lahko uporabite v osnovi identično kodo za vmesnik z MySQL ali SQLite:

{% highlight php %}
// PDO + MySQL
$pdo = new PDO('mysql:host=example.com;dbname=database', 'user', 'password');
$statement = $pdo->query("SELECT some\_field FROM some\_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);

// PDO + SQLite
$pdo = new PDO('sqlite:/path/db/foo.sqlite');
$statement = $pdo->query("SELECT some\_field FROM some\_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);
{% endhighlight %}

PDO ne bo prevajal vaših SQL poizvedb ali emuliral manjkajočih lastnosti. Je izključno za povezovanje
večih tipov podatkovnih baz z istim API-jem.

Bolj pomembno, `PDO` vam dovoljuje varno vstavljanje tujih vhodov (npr. ID-ji) v vaše SQL poizvedbe brez skrbi pred podatkovno baznimi SQL vstavljenimi napadi.
To je mogoče z uporabo PDO stavkov in vezanih parametrov.

Predpostavimo, da PHP skripa dobi numeričen ID, kot parameter poizvedbe. Ta ID bi moral biti uporabljen za pridobitev zapisa iz baze. To je `napačen`
način:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$pdo->query("SELECT name FROM users WHERE id = " . $_GET['id']); // <-- NO!
{% endhighlight %}

To je grozna koda. Vstavljate izvorni parameter poizvedbe v SQL poizvedbo. Tako dopustite možen izjemno hiter napad z uporabo prakse imenovane [SQL injiciranje](http://wiki.hashphp.org/Validation).
Samo predstavljajte si, če bi napadalec poslal sledeči iznajdljivi `id` parameter s klicom preko URL-ja kot je
`http://domain.com/?id=1%3BDELETE+FROM+users`. To bo nastavil `$_GET['id']` spremenljivko na `1;DELETE FROM users`
kar bo izbrisalo vse vaše uporabnike! Namesto tega bi morali očistiti ID vnos z uporabo PDO veznih parametrov.

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
$stmt->bindParam(':id', $_GET['id'], PDO::PARAM_INT); // <-- Automatically sanitized by PDO
$stmt->execute();
{% endhighlight %}

To je pravilna koda. Uporablja vezni parameter na PDO stavku. To počisti tuj vnosni ID preden se ga predstavi podatkovni bazi, kar
preprečuje potencialne SQL vstavljene napade.

* [Izvedite več o PDO]

Morate se tudi zavedati, da povezave podatkovne baze uporabljajo vire in se je že pogosto zgodilo, da so bili vsi viri
zasedeni, če povezave niso bile implicitno zaprte, čeprav je to bolj običajno v drugih jezikih. Z uporabo PDO, lahko
implicitno zaprete vaše povezave z uničenjem objekta in zagotovite, da so vse preostale reference nanj izbrisane,
t.j. nastavljene na NULL. Če ne naredite tega eksplicitno, bo PHP avtomatsko zaprl povezavo, ko se skripta konča - 
razen seveda, če uporabljate trajne povezave.

* [Izvedite več o PDO povezavah]

[Izvedite več o PDO]: http://www.php.net/manual/en/book.pdo.php
[Izvedite več o PDO povezavah]: http://php.net/manual/en/pdo.connections.php
[uradno opuščena od PHP 5.5.0]: http://php.net/manual/en/migration55.deprecated.php
[SQL injiciranje]: http://wiki.hashphp.org/Validation

[pdo]: http://php.net/pdo
[mysql]: http://php.net/mysql
[mysqli]: http://php.net/mysqli
[pgsql]: http://php.net/pgsql
[mssql]: http://php.net/mssql
