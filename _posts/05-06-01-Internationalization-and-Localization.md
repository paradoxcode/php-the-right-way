---
title:   Jezikovno in krajevno prilagajanje
isChild: true
anchor:  i18n_l10n
---

## Jezikovno prilagajanje oz. i18n (internationalisation) in krajevno prilagajanje oz. l10n (localisation) {#i18n_l10n_title}

_Opozorilo za novince: i18n in l10n sta t.i. numeronym-a, neke vrste kratice, kjer se številke uporabljajo za skrajšanje
besede - v našem primeru, internationalisation postane i18n in localisation, l10n._


Najprej moramo opredeliti ta dva podobna koncepta in druge s tem povezane stvari:

- **Jezikovno prilagajanje** pomeni organizacijo vaše kode, tako da se lahko prilagodi različnim jezikom ali regijam
brez refaktorizacije. To se običajno opravi enkrat - po možnosti v začetku projekta, drugače boste verjetno
morali narediti nekaj večjih sprememb v izvorni kodi.
- **Krajevno prilagajanje** se večinoma uporabi, ko se prilagaja vmesnik s prevajanjem vsebin, kar temelji na predhodnem delu i18n. To se običajno izvaja vsakič ko novi jezik ali regija potrebuje podporo in se posodablja, ko se dodajajo novi deli vmesnika, saj morajo biti na voljo v vseh podprtih jezikih.
- **Pluralizacija** določa pravila, ki so potrebna med različnimi jeziki za interoperabilnost nizov, ki vsebujejo številke in
števce. Na primer, v angleščini, ko imate samo en element, je to ednina, in vse, kar se razlikuje od tega, se
imenuje množina; množina je v tem jeziku označena z dodajanjem `s` nekaterim besedam, in včasih spreminja njihove dele.
V drugih jezikih, kot sta ruščina ali srbščina, obstajata poleg ednine dve obliki množine - lahko najdete tudi
jezike s skupno štirimi, petimi ali šestimi oblikami množine, kot so slovenščina, irščina ali arabščina.

## Pogosti načini za izvajanje

Najenostavnejši način za jezikovno prilaganje PHP programske opreme, je uporaba datotek polj in uporaba teh nizov v predlogah, kot je
`<h1><?=$TRANS['title_about_page']?></h1>`. To drugače ni priporočljiv način za resnejše projekte, saj predstavlja
nekatera vprašanja glede vzdrževanja - nekatera se lahko pojavijo v samem začetku, kot je pluralizacija. Torej,
ne poskušajte tega, če bo vaš projekt vseboval več kot nekaj strani.

Najbolj klasičen način in pogosta vzet kot referenca za i18n in l10n je [orodje za Unix, imenovano `gettext`][gettext]. Izvira
nazaj iz leta 1995 in je še vedno popolna izvedba za prevajanje programske opreme. Zelo enostavno ga je postaviti, medtem ko
je še vedno omogoča močna podporna orodja. Tu bomo govorili o Gettext. Poleg tega, da vam pomaga pri
ukazni vrstici, bomo predstavili oglično GUI aplikacijo, ki se lahko uporablja za enostavno posodobitev virov
datotek l10n.

### Druga orodja

Obstajajo skupne knjižnice, ki se uporabljajo za podporo Gettext in drugih implementacij i18n. Nekatere izmed njih se lažje
namestijio ali prikazujejo dodatne funkcionalnosti ali formate datotek i18n. V tem dokumentu, se bomo osredotočili na orodja, podprta
v PHP jedru, vendar tu je seznam drugih za celovitost:

- [oscarotero/Gettext][oscarotero]: Gettext podpora z vmesnikom OO; vključuje izboljšane pomožne funkcije, zmogljive
izvlečke za več formatov datotek (nekaterih od njih ukaz `gettext` izvorno ne podpira), lahko pa tudi izvaža
v druge formate pole, poleg datotek `.mo/.po`. Lahko je koristno, če morate vključiti vaše datoteke prevodov v druge dele
sistema, kot je vmesnik JavaScript.
- [symfony/translation][symfony]: podpira veliko različnih formatov, vendar priporoča uporabo bolj jedrnatih XLIFF-jev. Ne
vključuje pomožnih funkcij ali vgrajenih izvlečkov, vendar interno podpira nadomestne prostore z uporabo `strtr()`.
- [zend/i18n][zend]: podpira polja in datoteke INI, ali pa formate Gettext. Vključuje nivo predpomnenja, da vam ni
potrebno vsakič brati datotečnega sistema. Prav tako vključuje pomočnike ogleda in vhodne filtre področnih nastavitev ter preverjalnike.
Vendar nima pa izvlečka sporočil.

Druga ogrodja vključujejo tudi i18n module, vendar niso na voljo izven njihove kodne osnove:
- [Laravel] podpira osnovne datoteke polj, nima samodejnega izvlečka, vendar pa vključuje pomočnik `@lang` za datoteke predlog.
- [Yii] podpira polja, Gettext in prevode, ki temeljijo na podatkovni bazi. Vključuje izvleček sporočil. Podprt je z
[`Intl`][intl] razširitvijo, ki je na voljo od PHP 5.3, in temelji na [projektu ICU]; To omogoča Yii poganjati močnejše
zamenjave, kot so črkovanje številk, oblikovanje datumov, časovne intervale, valute in zaporedja.

Če se odločite uporabiti eno od knjižnic, ki ne ponuja izvlečkov, boste morda želeli uporabiti oblike gettext, tako
da lahko uporabite prvotni skupek orodij gettext (vključno s Poedit), kot je opisano v preostalem delu poglavja.

## Gettext

### Namestitev

Morda boste morali namestiti Gettext in s tem povezano PHP knjižnico z upraviteljem paketov, kot sta `apt-get` ali `yum`.
Po namestitvi jo omogočite z `extension=gettext.so` (Linux/Unix) ali `extension=php_gettext.dll` (Windows) v
vaši datoteki `php.ini`.

Tu bomo uporabili tudi [Poedit] za ustvarjanje datotek prevodov. Verjetno ga boste našli v upravitelju paketov vašega
sistema; na voljo je za Unix, Mac in Windows. Lahko se ga tudi [brezplačno prenese iz njihove spletne strani][poedit_download].

### Struktura

#### Vrste datotek

Obstajajo tri datoteke, ki se običajno obravnavajo pri delu z Gettext-om. Glavni med njimi so datoteke PO (Portable Object) in
MO (Machine Object), pri čemer je prva seznam berljivih "prevedenih objektov" in druga ustreza
binarni interpretaciji z gettext, ko se izvaja krajevno prilagajanje. Na voljo je tudi datoteka POT (Template), ki preprosto vsebuje
vse obstoječe ključe iz izvornih datotek in se lahko uporabi kot vodilo za ustvarjanje in posodobitev vseh datotek PO. Tiste datoteke
predlog niso obvezne: odvisno od orodja, ki ga uporabljate za l10n, lahko popolnoma primerno uporabite tudi samo datoteke PO/MO.
Vedno boste imeli en par datotek PO/MO glede na jezik in regijo, ampak le eno datoteko POT na domeno.

### Domene

Obstajajo nekateri primeri velikih projektov, kjer boste morda morali ločiti prevode, ko enake besede izražajo
različen pomen glede na kontekst. V teh primerih jih ločite v različne _domene_. To so v bistvu imenske
skupine datotek POT/PO/MO, kjer je datoteka omenjena _domena prevoda_. Majhni in srednje veliki projekti običajno
zaradi enostavnosti uporabljajo samo eno domeno; njeno ime je poljubno, vendar mi bomo uporabljali "main" za naše vzorce kode.
V [Symfony] projektih, na primer, se domene uporabljajo za ločevanje prevoda od sporočil potrjevanja.

#### Koda področnih nastavitev

Področne nastavitve so enostavno koda, ki označuje določeno različico jezika. To je opredeljeno po [ISO 639-1][639-1] in
[ISO 3166-1 alpha-2][3166-1] specifikacijah: dve mali črki za jezik, ki jima opcijsko sledi spodnja črta in dve
veliki črki, ki označujeta državo ali območno kodo. Za [redke jezike][rare], se uporabijo tri črke.

Za določene govorce je lahko del države odveč. V bistvu, nekateri jeziki imajo narečja v različnih
državah, kot sta avstrijska nemščina (`de_AT`) ali brazilska portugalščina (`pt_BR`). Drugi del se uporablja za razlikovanje
med temi narečji - ko ga ni, je to sprejeto kot "generična" ali "hibridna" verzija jezika.

### Struktura direktorijev

Za uporabo Gettext, bomo morali upoštevati posebno strukturo direktorijev. Najprej, boste morali izbrati poljubni
vrhnji direktorij za datoteke l10n v vašem izvornem repozitoriju. V njem boste imeli mapo za vsako potrebno področno nastavitev in fiksno
mapo `LC_MESSAGES`, ki bo vsebovala vse vaše PO/MO pare. Na primer:

{% highlight console %}
<project root>
 ├─ src/
 ├─ templates/
 └─ locales/
    ├─ forum.pot
    ├─ site.pot
    ├─ de/
    │  └─ LC_MESSAGES/
    │     ├─ forum.mo
    │     ├─ forum.po
    │     ├─ site.mo
    │     └─ site.po
    ├─ es_ES/
    │  └─ LC_MESSAGES/
    │     └─ ...
    ├─ fr/
    │  └─ ...
    ├─ pt_BR/
    │  └─ ...
    └─ pt_PT/
       └─ ...
{% endhighlight %}

### Oblike množin

Kot smo povedali v uvodu, imajo lahko različni jeziki različna pravila množine. Vendar gettext nam pomaga
tudi pri tem. Pri ustvarjanju nove datoteke `.po`, boste moralid določiti [pravila množine][plural] za ta
jezik in prevedeni deli, ki so odvisni od množine, bodo imeli drugačne oblike za vsako od teh pravil. Ko
kličete Gettext v kodi, boste morali določiti število povezano s stavkom in to bo uporabilo pravilno
obliko - tudi pri uporabi menjave niza, če je potrebno.

Pravila množine vključujejo število množin, ki so na voljo, in logični test z `n`, ki bi opredelil, v katero pravilo
spada določeno število (začne se z 0). Na primer:

- Japonščina: `nplurals=1; plural=0` - samo eno pravilo
- Angleščina: `nplurals=2; plural=(n != 1);` - dve pravili, prvo, če je N ena in v drugem primeru drugo
- Brazilska portugalščina: `nplurals=2; plural=(n > 1);` - dve pravili, drugo, če je N večji od ena, drugače prvo

Sedaj ko razumete osnovo, kako pravila množin delujejo - drugače si poglejte podrobnejše razlage
na [LingoHub vodičih][lingohub_plurals] -, morda boste želeli kopirati tiste, ki jih potrebujete iz [seznama][plural] namesto, da
jih pišete ročno.

Ko kliče Gettext, da naredi krajevno prilagajanje na stavkih s števci, mu boste morali dati
tudi povezano številko. Gettext bo določil, katero pravilo bi moralo biti v veljavi in uporabil pravilno krajevno različico.
Za vsako definirano pravilo množine boste morali dodati drugačen stavek v datoteke `.po`.

### Primer izvedbe

Po vsej tej teoriji naredimo nekaj praktičnega. Tukaj je odlomek iz datoteke `.po` - njena oblika ni pomembna.
Pomembna je celotna vsebina. Kako jo urediti, se boste enostavno naučili kasneje:

{% highlight po %}
msgid ""
msgstr ""
"Language: pt_BR\n"
"Content-Type: text/plain; charset=UTF-8\n"
"Plural-Forms: nplurals=2; plural=(n > 1);\n"

msgid "We're now translating some strings"
msgstr "Nós estamos traduzindo algumas strings agora"

msgid "Hello %1$s! Your last visit was on %2$s"
msgstr "Olá %1$s! Sua última visita foi em %2$s"

msgid "Only one unread message"
msgid_plural "%d unread messages"
msgstr[0] "Só uma mensagem não lida"
msgstr[1] "%d mensagens não lidas"
{% endhighlight %}

Prvi del deluje kot glava, ki ima `msgid` in` msgstr` prazna. Opisuje kodiranje datoteke,
oblike množine in druge manj pomembne stvari.
Drugi del prevaja enostaven niz iz angleščine v
brazilsko portugalščino in tretji počne isto, vendar zamenjuje niz iz [`sprintf`][sprintf], tako da
prevod lahko vsebuje uporabniško ime in datum obiska.
Zadnji del je primer oblik množin in prikazuje
verzijo ednine in množine kot `msgid` v angleščini in njene ustrezne prevode kot `msgstr` 0 in 1
(sledi številka pravila množine). Zamenjani niz je tudi uporabljen, da je število razvidno
neposredno v stavku, s pomočjo `%d`. Oblike množine imajo vedno dva `msgid` (ednino in množino), tako da ni
priporočljivo uporabljati kompleksnega jezika za vir prevoda.

### Razprava glede ključev l10n

As you might have noticed, we're using as source ID the actual sentence in English. That `msgid` is the same used
throughout all your `.po` files, meaning other languages will have the same format and the same `msgid` fields but
translated `msgstr` lines.

Talking about translation keys, there are two main "schools" here:

1. _`msgid` as a real sentence_.  
    The main advantages are:
    - if there are pieces of the software untranslated in any given language, the key displayed will still maintain some
    meaning. Example: if you happen to translate by heart from English to Spanish but need help to translate to French,
    you might publish the new page with missing French sentences, and parts of the website would be displayed in English
    instead;
    - it's much easier for the translator to understand what's going on and make a proper translation based on the
    `msgid`;
    - it gives you "free" l10n for one language - the source one;
    - The only disadvantage: if you need to change the actual text, you would need to replace the same `msgid`
    across several language files.

2. _`msgid` as a unique, structured key_.  
It would describe the sentence role in the application in a structured way, including the template or part where the
string is located instead of its content.
    - it's a great way to have the code organized, separating the text content from the template logic.
    - however, that could bring problems to the translator that would miss the context. A source language file would be
    needed as a basis for other translations. Example: the developer would ideally have an `en.po` file, that
    translators would read to understand what to write in `fr.po` for instance.
    - missing translations would display meaningless keys on screen (`top_menu.welcome` instead of `Hello there, User!`
    on the said untranslated French page). That's good it as would force translation to be complete before publishing -
    but bad as translation issues would be really awful in the interface. Some libraries, though, include an option to
    specify a given language as "fallback", having a similar behavior as the other approach.

The [Gettext manual][manual] favors the first approach as, in general, it's easier for translators and users in
case of trouble. That's how we will be working here as well. However, the [Symfony documentation][symfony-keys] favors
keyword-based translation, to allow for independent changes of all translations without affecting templates as well.

### Vsakdanja uporaba

V pogosto uporabljani aplikaciji, bi uporabili nekatere funkcije Gettext za pisanje statičnih tekstov na vaših straneh. Te stavki
bi se potem pojavili v datotekah `.po`, se prevedli, in se prevedli v datoteke `.mo`. Nato jih Gettext uporabi pri upodabljanju
dejanskega vmesnika. Glede na to, povežimo skupaj, kar smo doslej razpravljali, v primer korak za korakom:

#### 1. Primer datoteke predloge, ki vključuje nekaj različnih klicev Gettext

{% highlight php %}
<?php include 'i18n_setup.php' ?>
<div id="header">
    <h1><?=sprintf(gettext('Welcome, %s!'), $name)?></h1>
    <!-- code indented this way only for legibility -->
    <?php if ($unread): ?>
        <h2><?=sprintf(
            ngettext('Only one unread message',
                     '%d unread messages',
                     $unread),
            $unread)?>
        </h2>
    <?php endif ?>
</div>

<h1><?=gettext('Introduction')?></h1>
<p><?=gettext('We\'re now translating some strings')?></p>
{% endhighlight %}

- [`gettext()`][func] enostavno prevede `msgid` v njegov pripadajoči `msgstr` za dani jezik. Na voljo je tudi
bližnjica funkcije `_()`, ki deluje na enak način;
- [`ngettext()`][n_func] naredi enako, vendar s pravili množine;
- na voljo sta tudi [`dgettext()`][d_func] in [`dngettext()`][dn_func], ki vam omogočata prepisati domeno za posamezen klic. Več o nastavitvah domene v naslednjem primeru.

#### 2. Primer namestitvene datoteke (`i18n_setup.php` kot je uporabljeno zgoraj), izbira pravilnih področnih nastavitev ter nastavitev Gettext-a

```php
<?php
/**
 * Verifies if the given $locale is supported in the project
 * @param string $locale
 * @return bool
 */
function valid($locale) {
   return in_array($locale, ['en_US', 'en', 'pt_BR', 'pt', 'es_ES', 'es');
}

//setting the source/default locale, for informational purposes
$lang = 'en_US';

if (isset($_GET['lang']) && valid($_GET['lang'])) {
    // the locale can be changed through the query-string
    $lang = $_GET['lang'];    //you should sanitize this!
    setcookie('lang', $lang); //it's stored in a cookie so it can be reused
} elseif (isset($_COOKIE['lang']) && valid($_COOKIE['lang'])) {
    // if the cookie is present instead, let's just keep it
    $lang = $_COOKIE['lang']; //you should sanitize this!
} elseif (isset($_SERVER['HTTP_ACCEPT_LANGUAGE'])) {
    // default: look for the languages the browser says the user accepts
    $langs = explode(',', $_SERVER['HTTP_ACCEPT_LANGUAGE']);
    array_walk($langs, function (&$lang) { $lang = strtr(strtok($lang, ';'), ['-' => '_']); });
    foreach ($langs as $browser_lang) {
        if (valid($browser_lang)) {
            $lang = $browser_lang;
            break;
        }
    }
}

// here we define the global system locale given the found language
putenv("LANG=$lang");

// this might be useful for date functions (LC_TIME) or money formatting (LC_MONETARY), for instance
setlocale(LC_ALL, $lang);

// this will make Gettext look for ../locales/<lang>/LC_MESSAGES/main.mo
bindtextdomain('main', '../locales');

// indicates in what encoding the file should be read
bind_textdomain_codeset('main', 'UTF-8');

// if your application has additional domains, as cited before, you should bind them here as well
bindtextdomain('forum', '../locales');
bind_textdomain_codeset('forum', 'UTF-8');

// here we indicate the default domain the gettext() calls will respond to
textdomain('main');

// this would look for the string in forum.mo instead of main.mo
// echo dgettext('forum', 'Welcome back!');
?>
```

#### 3. Priprava prevodov

To make matters easier - and one of the powerful advantages Gettext has over custom framework i18n packages - is its
custom file type. "Oh man, that's quite hard to understand and edit by hand, a simple array would be easier!" Make no
mistake, applications like [Poedit] are here to help - _a lot_. You can get the program from
[their website][poedit_download], it's free and available for all platforms. It's a pretty easy tool to get used to,
and a very powerful one at the same time - using all powerful features Gettext has available.

In the first run, you should select "File > New Catalog" from the menu. There you'll have a small screen where we will
set the terrain so everything else runs smoothly. You'll be able to find those settings later through
"Catalog > Properties":

- Project name and version, Translation Team and email address: useful information that goes in the `.po` file header;
- Language: here you should use that format we mentioned before, such as `en_US` or `pt_BR`;
- Charsets: UTF-8, preferably;
- Source charset: set here the charset used by your PHP files - probably UTF-8 as well, right?
- plural forms: here go those rules we mentioned before - there's a link in there with samples as well;
- Source paths: here you must include all folders from the project where `gettext()` (and siblings) will happen - this
is usually your templates folder(s)
- Source keywords: this last part is filled by default, but you might need to alter it later - and is one of the
powerful points of Gettext. The underlying software knows how the `gettext()` calls look like in several programming
languages, but you might as well create your own translation forms. This will be discussed later in the "Tips" section.

After setting those points you'll be prompted to save the file - using that directory structure we mentioned as well,
and then it will run a scan through your source files to find the localization calls. They'll be fed empty into the
translation table, and you'll start typing in the localized versions of those strings. Save it and a `.mo` file will be
(re)compiled into the same folder and ta-dah: your project is internationalized.

#### 4. Prevajanje nizov

As you may have noticed before, there are two main types of localized strings: simple ones and the ones with plural
forms. The first ones have simply two boxes: source and localized string. The source string can't be modified as
Gettext/Poedit do not include the powers to alter your source files - you should change the source itself and rescan
the files. Tip: you may right-click a translation line and it will hint you with the source files and lines where that
string is being used.  
On the other hand, plural form strings include two boxes to show the two source strings, and tabs so you can configure
the different final forms.

Whenever you change your sources and need to update the translations, just hit Refresh and Poedit will rescan the code,
removing non-existent entries, merging the ones that changed and adding new ones. It may also try to guess some
translations, based on other ones you did. Those guesses and the changed entries will receive a "Fuzzy" marker,
indicating it needs review, being highlighted in the list. It's also useful if you have a translation team and someone
tries to write something they're not sure about: just mark Fuzzy and someone else will review later.

Finally, it's advised to leave "View > Untranslated entries first" marked, as it will help you _a lot_ to not forget
any entry. From that menu, you can also open parts of the UI that allow you to leave contextual information for
translators if needed.

### Nasveti in triki

#### Možne težave pri predpomnenju

Če poganjate PHP kot modul za Apache (`mod_php`), se boste morda soočili s težavami predpomnenja datotek `.mo`. To
se zgodi prvič, ko se preberejo, ter, ko jih osvežite, boste morda morali znova zagnati strežnik. Na nginx in PHP5
ponavadi traja le nekaj osvežitev strani za osvežitev predpomnilnika prevodov. Na PHP7 je to redko potrebno.

#### Dodatne pomožne funkcije

As preferred by many people, it's easier to use `_()` instead of `gettext()`. Many custom i18n libraries from
frameworks use something similar to `t()` as well, to make translated code shorter. However, that's the only function
that sports a shortcut. You might want to add in your project some others, such as `__()` or `_n()` for `ngettext()`,
or maybe a fancy `_r()` that would join `gettext()` and `sprintf()` calls. Other libraries, such as
[oscarotero's Gettext][oscarotero] also provide helper functions like these.

In those cases, you'll need to instruct the Gettext utility on how to extract the strings from those new functions.
Don't be afraid, it's very easy. It's just a field in the `.po` file, or a Settings screen on Poedit. In the editor,
that option is inside "Catalog > Properties > Source keywords". You need to include there the specifications of those
new functions, following [a specific format][func_format]:

- if you create something like `t()` that simply returns the translation for a string, you can specify it as `t`.
Gettext will know the only function argument is the string to be translated;
- if the function has more than one argument, you can specify in which one the first string is - and if needed, the
plural form as well. For instance, if we call our function like this: `__('one user', '%d users', $number)`, the
specification would be `__:1,2`, meaning the first form is the first argument, and the second form is the second
argument. If your number comes as the first argument instead, the spec would be `__:2,3`, indicating the first form is
the second argument, and so on.

After including those new rules in the `.po` file, a new scan will bring in your new strings just as easy as before.

### Viri

* [Wikipedia: i18n and l10n](https://en.wikipedia.org/wiki/Internationalization_and_localization)
* [Wikipedia: Gettext](https://en.wikipedia.org/wiki/Gettext)
* [LingoHub: PHP internationalization with gettext tutorial][lingohub]
* [PHP Manual: Gettext](http://php.net/manual/en/book.gettext.php)
* [Gettext Manual][manual]

[Poedit]: https://poedit.net
[poedit_download]: https://poedit.net/download
[lingohub]: https://lingohub.com/blog/2013/07/php-internationalization-with-gettext-tutorial/
[lingohub_plurals]: https://lingohub.com/blog/2013/07/php-internationalization-with-gettext-tutorial/#Plurals
[plural]: http://docs.translatehouse.org/projects/localization-guide/en/latest/l10n/pluralforms.html
[gettext]: https://en.wikipedia.org/wiki/Gettext
[manual]: http://www.gnu.org/software/gettext/manual/gettext.html
[639-1]: https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
[3166-1]: http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2
[rare]: http://www.gnu.org/software/gettext/manual/gettext.html#Rare-Language-Codes
[func_format]: https://www.gnu.org/software/gettext/manual/gettext.html#Language-specific-options
[oscarotero]: https://github.com/oscarotero/Gettext
[symfony]: https://symfony.com/doc/current/components/translation.html
[zend]: https://docs.zendframework.com/zend-i18n/translation
[laravel]: https://laravel.com/docs/master/localization
[yii]: http://www.yiiframework.com/doc-2.0/guide-tutorial-i18n.html
[intl]: http://br2.php.net/manual/en/intro.intl.php
[ICU project]: http://www.icu-project.org
[symfony-keys]: https://symfony.com/doc/current/components/translation/usage.html#creating-translations

[sprintf]: http://php.net/manual/en/function.sprintf.php
[func]: http://php.net/manual/en/function.gettext.php
[n_func]: http://php.net/manual/en/function.ngettext.php
[d_func]: http://php.net/manual/en/function.dgettext.php
[dn_func]: http://php.net/manual/en/function.dngettext.php
