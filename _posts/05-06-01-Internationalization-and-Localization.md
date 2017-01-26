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

Kot ste morda opazili, uporabljamo za izvorni ID dejanski stavek v angleščini. Tisti `msgid` je enak, kot je uporabljen
v vseh datotekah `.po`, kar pomeni, da bodo drugi jeziki imeli enako obliko in enaka `msgid` polja, vendar
prevedene vrstice `msgstr`.

Za ključe prevodov obstajata dva glavna načina:

1. _`msgid` kot celoten stavek_.
    Glavne prednosti so:
    - Če obstajajo neprevedeni deli programske opreme za katerikoli jezik, bo prikazani ključ še vedno ohranil nekaj
    pomena. Primer: prevajanje iz angleščine v španščino vendar potrebujete pomoč pri prevajanju v francoščino,
    boste morda objavili novo stran z manjkajočimi francoskimi prevodi. V tem primeru bodo deli spletne strani prikazani
    v angleščini;
    - Je veliko enostavnejše prevajalcu razumeti, kaj se dogaja in podati ustrezni prevod, ki temelji na
     `msgid`;
     - Privzeto je l10n za enega od jezikov tako že podan;
     - Edina slabost: če želite spremeniti dejansko besedilo, bo potrebno zamenjati ta `msgid`
     v več jezikovnih datotekah.

2. _`msgid` kot unikaten, strukturiran ključ_.
Namesto stavka se tu uporbi strukturiran način, vključno s predlogi ali deli, kjer
se določen niz nahaja.
    - To je odličen način imeti kodo organizirano in ločiti besedilo vsebine od logike predloge.
    - Vseeno to lahko prinese težave prevajalcu, če spregleda kontekst. Izvorna jezikovna datoteka je
    potrebna kot osnova za druge prevode. Primer: razvijalec bi v najboljšem primeru imel datoteko `en.po`, ki
    jo prevajalci uporabijo za prevajanje v datoteki npr. `fr.po`.
    - Manjkajoči prevodi prikažejo nesmiselne ključe (`top_menu.welcome` namesto `Pozdravljeni, uporabnik!`
    na omenjeni neprevedeni francoski strani). To je do določene mere prednost, saj motivira prevajalca za popolno objavo.
    Slabost pa je, da težave pri prevodih izgledajo res grdo v vmesniku. Nekatere knjižnice imajo tudi možnost, da
    opredelijio določen jezik kot "nadomestni" in se uporabi v primeru manjkajočega prevoda.

[Gettext navodila][manual] dajejo prednost prvemu pristopu, kot splošnemu, saj je lažji prevajalcem in uporabnikom
v primeru težav. Tako bomo delali tudi v sledečih primerih. Drugače [Symfony dokumentacija][symfony-keys] daje
prednost ključnim besedam, kar omogoča neodvisne spremembe vseh prevodov, ne da bi to vplivalo na predloge.

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

Da naredimo zadeve enostavnejše - ena izmed večjih prednosti Gettext-a pred i18n paketi ogrodij je njegov
tip datoteke po meri. "Oh človek, to je zelo težko razumeti in ročno urejati. Enostavno polje nizov je enostavnejše!" Ne naredite
napake, aplikacije, kot je [Poedit] so tu v pomoč - _veliko_. Program lahko dobite
iz [njihove spletne strani][poedit_download], je brezplačen in na voljo za vse platforme. Je zelo enostavno orodje za privaditi,
in hkrati zelo močno - uporaba vse zmogljivih funkcij, ki jih ima Gettext na voljo.

V prvem zagonu morate iz menija izbrati "File > New Catalog". Tam bo majhen zaslon, kjer bomo
določili podatke, da bo vse ostalo gladko teklo. Te nastavitve boste lahko našli pozneje prek
"Catalog > Properties":

- Ime in različica projekta, ekipa prevajalcev in e-poštni naslov: koristne informacije, ki gredo v `.po` glavo datoteke;
- Jezik: tu morate uporabiti obliko, ki smojo že omenili, npr. `en_US` ali `pt_BR`;
- Nabor znakov: po možnosti UTF-8;
- Izvorni nabor znakov: tu nastavite nabor znakov za vaše PHP datoteke - verjetno tudi UTF-8;
- Oblike množin: pravila množin, ki smo jih omenili zgoraj - na voljo je tudi povezava s primeri;
- Izvorne poti: tu morate vključiti vse mape iz projekta, kjer se uporabljajo `gettext()` (in pripadajoče) - to
je običajno mapa predloge
- Izvorne ključne besede: ta zadnji del je izpolnjen privzeto, vendar ga boste morda morali spremeniti kasneje. Je eden izmed
močnih točk Gettext. Osnovni program ve, kako `gettext()` klici izgledajo v večih programskih
jezikih, vendar lahko tudi ustvarite svoje prevajalske obrazce. O tem bomo govorili kasneje v poglavju "Nasveti".

Po nastavitvi teh točk boste pozvani, da shranite datoteko - z uporabo datotečne strukture, ki smo jo omenili zgoraj,
nato pa se bo izvedlo skeniranje izvornih datotek, da se najde klice krajevnega prilagajanja. V tabelo za prevajanje bodo podani
prazni in začeli boste lahko vpisovati krajevne različice teh nizov. Shranite jih in datoteka `.mo` bo
ponovno prevedena v istem direktoriju. Tako je vaš projekt sedaj internacionaliziran.

#### 4. Prevajanje nizov

Kot ste morda prej opazili, obstajata dve glavni vrsti krajevno prilagojenih nizev: enostavni in tisti z oblikami
množine. Prvi imajo le dve okenci: vir in lokaliziran niz. Izvornega niza ni mogoče spreminjati, saj
Gettext/Poedit ne vključujeta funkcionalnosti spreminjanja izvornih datotek - spremeniti morate vir sam in znova preveriti
datoteke. Nasvet: desni klik vrstice prevoda bo prikazal namig o izvorni datoteki in vrsticah, kjer je ta niz uporabljen.
Druga vrsta nizev, nizi z oblikami množine, vključujejo dve okenci za prikaz dveh izvornih nizev in zavihkov, tako da lahko
nastavite različne končne oblike.
Po drugi strani, plural form nizi vključuje dve škatli za prikaz dveh vir strune, in zavihke tako lahko nastavite
različne končne oblike.

Vsakič, ko spremenite vaše vire in morate posodobiti prevode, samo kliknite Refresh in Poedit bo znova preveril kodo,
odstranil neobstoječe vnose, združil tiste, ki so se spremenili in dodal nove. Prav tako lahko poskusi uganiti nekaj
prevodov, ki temeljijo na drugih, ki ste jih vnesli. Ta ugibanja in spremenjeni vnosi bodo prejeli "Fuzzy" oznako,
kar označuje, da jih je potrebno pregledati, pri čemer so poudarjeni v seznamu. Prav tako je uporabno, če imate prevajalsko ekipo in nekdo
skuša napisati nekaj kar niso prepričani: Samo označite Fuzzy in nekdo drug bo to pregledal kasneje.

Priporočljivo je pustiti "View > Untranslated entries first" označeno, saj vam bo _zelo_ pomagalo, da ne pozabite
kakšnega vpisa. Iz tega menija lahko tudi odprete dele uporabniškega vmesnika, ki vam omogočajo pustiti vsebinske informacije za
prevajalce, če je potrebno.

### Nasveti in triki

#### Možne težave pri predpomnenju

Če poganjate PHP kot modul za Apache (`mod_php`), se boste morda soočili s težavami predpomnenja datotek `.mo`. To
se zgodi prvič, ko se preberejo, ter, ko jih osvežite, boste morda morali znova zagnati strežnik. Na nginx in PHP5
ponavadi traja le nekaj osvežitev strani za osvežitev predpomnilnika prevodov. Na PHP7 je to redko potrebno.

#### Dodatne pomožne funkcije

Veliko ljudi ima raje, lažjo uporabo `_ ()` namesto `gettext()`. Veliko knjižnic i18n po meri iz
ogrodij uporabljajo tudi nekaj podobnega `t()`, da je koda prevoda krajša. Kljub temu pa je to edina funkcija
za bližnjico. Morda boste želeli dodati v vaš projekt še nekatere druge, kot so `__()` ali `_n()` za `ngettext()`,
ali morda lično `_r()`, kar združi klica `gettext()` in `sprintf()`. Druge knjižnice, kot je
[oscarotero's Gettext][oscarotero] ponujajo tudi pomožne funkcije, kot so te.

V teh primerih boste morali navesti Gettext pripomočku, kako izvleči nize iz teh novih funkcij.
Ne bojte se, to je zelo enostavno. To je samo polje v datoteki `.po`, ali nastavitev zaslona na Poedit. V urejevalniku
je ta možnost znotraj "Catalog > Properties > Source keywords". Vključiti pa morate specifikacije tistih
novih funkcij, ki sledijo [določeni obliki][func_format]:

- Če ste ustvarili nekaj podobnega `t()`, ki preprosto vrne prevod za niz, jo lahko določite kot `t`.
Gettext bo vedel, da je edini argument funkcije niz, ki ga je potrebno prevesti;
- Če ima funkcija več kot en argument, lahko določite, v katerem je prvi niz - in, če je potrebno, tudi
množinska obliko. Na primer, če našo funkcijo imenujemo takole: `__('one user', '%d users', $number)`, je
specifikacija `__:1,2`, kar pomeni prva oblika je prvi argument, druga oblika je drug
argument. Če je vaša številka prvi argument, bo speficikacija `__:2,3`, kar označuje, da je prva oblika
drugi argument, in tako naprej.

Po vključitvi teh novih pravil v datoteko `.po`, se bo pričelo novo skeniranje v vaših nizih, prav tako enostavno kot prej.

### Viri

* [Wikipedia: i18n in l10n](https://en.wikipedia.org/wiki/Internationalization_and_localization)
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
