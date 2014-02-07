---
title: Podatkovne baze
---

# Podatkovne baze {#databases_title}

Mnogokrat bo vaša PHP koda uporabila podatkovno bazo za pridobivanje informacij. Na voljo imate nekaj opcij za povezavo in interakcijo
z vašo podatkovno bazo. Priporočena opcija _do PHP 5.1.0_ je bila uporaba originalnih gonilnikov kot so [mysql][mysql], [mysqli][mysqli], [pgsql][pgsql] itd.

Originalni gonilniki so odlični, če uporabljate samo ENO podatkovno bazo v vaši aplikaciji, vendar če na primer uporabljate MySQL in nekaj MSSQL hkrati,
ali se potrebujete povezati na Oracle podatkovno bazo, potem ne boste mogli uporabiti istih gonilnikov. Naučiti se boste morali popolnoma nov API za vsako
podatkovno bazo &mdash; in to lahko postane neumno.

Kot dodatno upoštevanje glede originalnih gonilnikov, mysql razširitev za PHP ni več v aktivnem razvoju in uradni status od PHP 5.4.0 je
"dolgoročna opustitev". To pomeni, da bo odstranjen znotraj nekaj naslednjih izdaj, do PHP 5.6 (ali karkoli pride po 5.5) bo vsekakor odstranjeno.
Če uporabljate `mysql_connect()` in `mysql_query()` v vaših aplikacijah, se boste v srečali s prepisovanjem, torej je najboljša opcija zamenjava mysql uporabe
z mysqli ali PDO v vaših aplikacijah znotraj vašega razvojnega časovnega načrta, tako da se vam ne bo mudilo kasneje. _Če pričenjate od začetka potem vsekakor ne
uporabite mysql razširitve: uporabite [MySQLi razširitev][mysqli], ali uporabite PDO._

* [PHP: Izbira API-ja za MySQL](http://php.net/manual/en/mysqlinfo.api.choosing.php)

## PDO

PDO je abstraktna knjižnica povezovanja podatkovne baze &mdash; vgrajen v PHP od 5.1.0 &mdash;, ki ponuja enoten vmesnik za komunikacijo z
mnogimi različnimi podatkovnimi bazami. PDO ne bo prevajal vaših SQL poizvedb ali emuliral manjkajočih lastnosti. Je izključno za povezovanje
večih tipov podatkovnih baz z istim API-jem.

Bolj pomembno, `PDO` vam dovoljuje varno vstavljanje tujih vhodov (npr. ID-ji) v vaše SQL poizvedbe brez skrbi pred podatkovno baznimi SQL vstavljenimi napadi.
To je mogoče z uporabo PDO stavkov in vezanih parametrov.

Predpostavimo, da PHP skripa dobi numeričen ID, kot parameter poizvedbe. Ta ID bi moral biti uporabljen za pridobitev zapisa iz baze. To je `napačen`
način:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:users.db');
$pdo->query("SELECT name FROM users WHERE id = " . $_GET['id']); // <-- NO!
{% endhighlight %}

To je grozna koda. Vstavljate izvorni parameter poizvedbe v SQL poizvedbo. Tako dopustite možen izjemno hiter napad.
Samo predstavljajte si, če bi napadalec poslal sledeči iznajdljivi `id` parameter s klicom preko URL-ja kot je
`http://domain.com/?id=1%3BDELETE+FROM+users`. To bo nastavil `$_GET['id']` spremenljivko na `1;DELETE FROM users`
kar bo izbrisalo vse vaše uporabnike! Namesto tega bi morali očistiti ID vnos z uporabo PDO veznih parametrov.

{% highlight php %}
<?php
$pdo = new PDO('sqlite:users.db');
$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
$stmt->bindParam(':id', $_GET['id'], PDO::PARAM_INT); // <-- Automatically sanitized by PDO
$stmt->execute();
{% endhighlight %}

To je pravilna koda. Uporablja vezni parameter na PDO stavku. To počisti tuj vnosni ID preden se ga predstavi podatkovni bazi, kar
preprečuje potencialne SQL vstavljene napade.

* [Naučite se o PDO][1]

Morate se tudi zavedati, da povezave podatkovne baze uporabljajo vire in se je že pogosto zgodilo, da so bili vsi viri
zasedeni, če povezave niso bile implicitno zaprte, čeprav je to bolj običajno v drugih jezikih. Z uporabo PDO, lahko
implicitno zaprete vaše povezave z uničenjem objekta in zagotovite, da so vse preostale reference nanj izbrisane,
t.j. nastavljene na NULL. Če ne naredite tega eksplicitno, bo PHP avtomatsko zaprl povezavo, ko se skripta konča - 
razen seveda, če uporabljate trajne povezave.

* [Naučite se o PDO povezavah][5]

## Abstraktni nivoji

Mnoga ogrodja ponujajo svoj lasten abstraktni nivo, ki se lahko ali ne naslanja na PDO. Le-te bodo pogosto emulirala lastnosti za
en podatkovno bazni sistem, ko drugi manjka z zavitjem vaših poizvedb v PHP metodah. To omogoča dejansko abstrakcijo podatkovne baze.
To bo seveda dodalo nekaj dodatne uporabe virov, vendar če gradite prenosno aplikacijo, ki potrebuje delovati z MySQL, PostgreSQL in
SQLite potem je nekaj več uporabe virov vredno zaradi čistoče kode.

Nekaj abstraktnih nivojev je bilo že vgrajenih v PSR-0 standard imenskih prostorov, tako da je možno namestiti v katerokoli aplikacijo kot:

* [Aura SQL][6]
* [Doctrine2 DBAL][2]
* [Propel][7]
* [ZF2 Db][4]
* [ZF1 Db][3]

[1]: http://www.php.net/manual/en/book.pdo.php
[2]: http://www.doctrine-project.org/projects/dbal.html
[3]: http://framework.zend.com/manual/en/zend.db.html
[4]: http://packages.zendframework.com/docs/latest/manual/en/index.html#zend-db
[5]: http://php.net/manual/en/pdo.connections.php
[6]: https://github.com/auraphp/Aura.Sql
[7]: http://propelorm.org/Propel/

[mysql]: http://php.net/mysql
[mysqli]: http://php.net/mysqli
[pgsql]: http://php.net/pgsql
