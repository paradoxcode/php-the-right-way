---
title:   Osnovne PHP predloge
isChild: true
anchor:  plain_php_templates
---

## Osnovne PHP predloge {#plain_php_templates_title}

Osnovne PHP predloge so enostavno predloge, ki uporabljajo prvotno PHP kodo. So naravna izbira, ker je PHP dejansko
jezik predlog sam po sebi. To enostavno pomeni, da lahko kombinirate PHP kodo znotraj druge kode, kot je HTML. To je
koristno za PHP razvijalce, saj ni nobene nove sintakse za naučiti, poznajo funkcije, ki so jim na voljo in njihovi
urejevalniki kode že imajo vgrajeno označevanje sintakse PHP in avtomatsko zaključevanje. Dalje, osnovne PHP predloge se nagibajo, da so
kakor hitre možno, saj ni potrebne nobene faze prevajanja.

Vsako moderno PHP ogrodje vključuje neko vrsto sistema predlog, večina od teh uporabljajo privzeto osnovni PHP. Zunaj
ogrodij, knjižnice kot je [Plates][plates] ali [Aura.View][aura] delujejo
z osnovnimi PHP predlogami enostavnejše s ponujanjem moderne funkcionalnosti predlog, kot je dedovanje, postavitve in
razširitve.

### Enostaven primer osnovne PHP predloge

Uporaba knjižnice [Plates][plates]:

{% highlight php %}
<?php // user_profile.php ?>

<?php $this->insert('header', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->escape($name)?></p>

<?php $this->insert('footer'i) ?>
{% endhighlight %}

### Primer osnovne PHP predloge z uporabo dedovanja

Uporaba knjižnice [Plates][plates].

{% highlight php %}
<?php // template.php ?>

<html>
<head>
    <title><?=$title?></title>
</head>
<body>

<main>
    <?=$this->section('content')?>
</main>

</body>
</html>
{% endhighlight %}

{% highlight php %}
<?php // user_profile.php ?>

<?php $this->layout('template', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->escape($name)?></p>

{% endhighlight %}


[plates]: http://platephp.com/
[aura]: https://github.com/auraphp/Aura.View