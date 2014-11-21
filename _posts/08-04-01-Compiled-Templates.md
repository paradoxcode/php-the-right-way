---
title: Prevedene predloge
isChild: true
anchor: compiled_templates
---

## Prevedene predloge {#compiled_templates}

Medtem ko se je PHP razvil v zrel, objektno orientiran jezik, se
[ni veliko izboljšal](http://fabien.potencier.org/article/34/templating-engines-in-php) kot jezik predlog.
Prevedene predloge, kot so [Twig](http://twig.sensiolabs.org/) ali [Smarty](http://www.smarty.net/)*, zapolnjujejo to praznino s
ponujanjem nove sintakse, ki je bila sestavljena posebej za predloge. Od avtomatskega čiščenja, do dedovanja in
poenostavljenih krmilnih struktur, so prevedene predloge načrtovane za enostavnejše pisanje, čistejše branje in varnejše za uporabo.
Prevedene predloge so lahko celo deljene med različnimi jeziki, [Mustache](http://mustache.github.io/) je dober
primer tega. Ker morajo biti te predloge prevedene, prihaja do manjšega udarca na uspešnost, vendar je ta zelo minimalen,
ko je uporabljeno ustrezno predpomnenje.

**Medtem ko Smarty ponuja avtomatsko čiščenje, ta lastnosti NI omogočena privzeto.*

### Enostaven primer prevedene predloge

Uporaba knjižnice [Twig](http://twig.sensiolabs.org/).
{% highlight text %}
{% raw %}
{% include 'header.html' with {'title': 'User Profile'} %}

<h1>User Profile</h1>
<p>Hello, {{ name }}</p>

{% include 'footer.html' %}
{% endraw %}
{% endhighlight %}

### Primer prevedenih predlog z uporabo dedovanja

Uporaba knjižnice [Twig](http://twig.sensiolabs.org/).

{% highlight text %}
{% raw %}
// template.html

<html>
<head>
    <title>{% block title %}{% endblock %}</title>
</head>
<body>

<main>
    {% block content %}{% endblock %}
</main>

</body>
</html>
{% endraw %}
{% endhighlight %}

{% highlight text %}
{% raw %}
// user_profile.html

{% extends "template.html" %}

{% block title %}User Profile{% endblock %}
{% block content %}
    <h1>User Profile</h1>
    <p>Hello, {{ name }}</p>
{% endblock %}
{% endraw %}
{% endhighlight %}
