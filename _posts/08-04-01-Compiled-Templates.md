---
title:   Prevedene predloge
isChild: true
anchor:  compiled_templates
---

## Prevedene predloge {#compiled_templates_title}

Medtem ko se je PHP razvil v zrel, objektno orientiran jezik, se [ni veliko izboljšal][article_templating_engines] kot
jezik predlog. Prevedene predloge, kot so [Twig], [Brainy], ali [Smarty]*, zapolnjujejo to praznino s ponujanjem nove sintakse, ki je
bila sestavljena posebej za predloge. Od avtomatskega čiščenja, do dedovanja in poenostavljenih krmilnih struktur, so
prevedene predloge načrtovane za enostavnejše pisanje, čistejše branje in varnejše za uporabo. Prevedene predloge so lahko celo
deljene med različnimi jeziki, [Mustache] je dober primer tega. Ker morajo biti te predloge prevedene,
prihaja do manjšega udarca na zmogljivost, vendar je ta zelo minimalen, ko je uporabljeno ustrezno predpomnjenje.

**Medtem ko Smarty ponuja avtomatsko čiščenje, ta lastnosti NI omogočena privzeto.*

### Enostaven primer prevedene predloge

Uporaba knjižnice [Twig].

{% highlight html+jinja %}
{% raw %}
{% include 'header.html' with {'title': 'User Profile'} %}

<h1>User Profile</h1>
<p>Hello, {{ name }}</p>

{% include 'footer.html' %}
{% endraw %}
{% endhighlight %}

### Primer prevedenih predlog z uporabo dedovanja

Uporaba knjižnice [Twig].

{% highlight html+jinja %}
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

{% highlight html+jinja %}
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


[article_templating_engines]: http://fabien.potencier.org/article/34/templating-engines-in-php
[Twig]: http://twig.sensiolabs.org/
[Brainy]: https://github.com/box/brainy
[Smarty]: http://www.smarty.net/
[Mustache]: http://mustache.github.io/
