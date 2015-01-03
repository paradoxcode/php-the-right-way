---
title:   Gradnja in postavitev vaše aplikacije
isChild: true
anchor:  building_and_deploying_your_application
---

## Gradnja in postavitev vaše aplikacije {#building_and_deploying_your_application_title}

Če ugotovite, da delate ročne spremembe podatkovne baze ali poganjate vaše teste ročno, preden posodabljate vaše datoteke
(ročno), ponovno premislite! Z vsakim dodatnim ročnim opravilom potrebnim za postavitev nove verzije vaše aplikacije,
se možnosti za potencialno usodno napako povečajo. Ali če imate opravka z enostavno posodobitvijo, podrobnim procesom gradnje
ali celo strategijo zvezne integracije, je [avtomatizacija gradnje][buildautomation] vaš prijatelj.

Med opravili, ki jih želite avtomatizirati so:

* Upravljanje odvisnosti
* Kompiliranje, minifikacija vaših sredstev (slike ...)
* Poganjanje testov
* Ustvarjanje dokumentacije
* Pakiranje
* Postavitev


### Orodja za avtomatizirano gradnjo

Orodja za gradnjo bi bila lahko opisana kot zbirka skript, ki ravnajo s pogostimi opravili postavitve programske opreme.
Orodje za gradnjo ni del vaše programske opreme, na vašo programsko opremo deluje od 'zunaj'.

Na voljo je ogromno odprtokodnih orodij, ki so na voljo za pomoč pri avtomatizirani gradnji. Nekatera so napisana v PHP,
nekatera ne. To vas ne bi smelo ovirati pri njihovi uporabi, če so bolj primerna za določeno nalogo. Tu je nekaj primerov:

[Phing] je najenostavnejša pot za začetek z avtomatizirano postavitvijo v PHP svetu. S Phing-om
lahko kontrolirate vaše pakiranje, postavitev ali proces testiranja znotraj enostavne XML postavitvene datoteke. Phing
(ki je osnovan na [Apache Ant] ponuja bogat nabor opravil, ki se jih ponavadi potrebuje za namestitev
ali posodobitev spletne aplikacije in je lahko razširjen z dodatnimi opravili po meri, napisanimi v PHP.

[Capistrano] je sistem za *vmesne do napredne programerje*, da lahko izvajajo
komande v strukturirani, ponovljivi poti na eni ali več oddaljenih naprav. Je pred-nastavljen za postavitev Ruby on Rails aplikacij,
čeprav ljudje z njim **uspešno postavljajo PHP sisteme**. Uspešna uporaba Capistrana zavisi na delovnem znanju Ruby-ja in Rake-a.

Dave Gardner-jeva objava na blogu [PHP Deployment with Capistrano][phpdeploy_capistrano] je dobra začetna točka za PHP
razvijalce, ki jih zanima Capistrano.

[Chef] je bolj postavitveno ogrodje, je zelo močno na Ruby-ju osnovano sistemsko integrirano ogrodje,
ki ne samo postavi vaše aplikacije, vendar lahko zgradi vaše celotno strežniško ogrodje ali virtualne naprave.

[Deployer] je razvojno orodje napisano v PHP, je enostavno in funkcionalno. Naložite vašo kodo na vse strežnike, kjer želite, podpira nalaganje preko kopiranja ali VCS-a (kot je git), ali preko rsync. Poženite vaša opravila na vseh vaših strežnikih ali uporabite naše recepte za pogosta opravila za Symfony, Laravel, Zend Framework in Yii.

#### Chef viri za PHP razvijalce:

* [Blog serija iz treh delov o postavitvi LAMP aplikacije s Chef, Vagrant, in EC2][chef_vagrant_and_ec2]
* [Chef recepti, ki namestijo in nastavijo PHP 5.3 in PEAR paketni upravljalni sistem][Chef_cookbook]
* [Chef serija video vodičev][Chef_tutorial] Opscode, izdelovalca chef-a

#### Nadaljnje branje:

* [Avtomatizacija vašega projekta z Apache Ant][apache_ant_tutorial]

### Zvezna integracija

> Continuous Integration is a software development practice where members of a team integrate their work frequently, 
> usually each person integrates at least daily — leading to multiple integrations per day. Many teams find that this 
> approach leads to significantly reduced integration problems and allows a team to develop cohesive software more 
> rapidly.

*-- Martin Fowler*

Obstaja več različnih poti za implementacijo zvezne integracije za PHP. Pred kratkim je [Travis CI]
naredil odlično delo zvezne integracije, zaradi česar je realnost tudi za manjše projekte. Travis CI je gostovan servis zvezne
integracije za odprto kodno skupnost. Integriran je z GitHub-om in ponuja prvo razredno podporo za mnoge jezike, tudi PHP.

#### Nadaljnje branje:

* [Zvezna integracija z Jenkins][Jenkins]
* [Zvezna integracija s PHPCI][PHPCI]
* [Zvezna integracija s Teamcity][Teamcity]


[buildautomation]: http://en.wikipedia.org/wiki/Build_automation
[Phing]: http://www.phing.info/
[Apache Ant]: http://ant.apache.org/
[Capistrano]: https://github.com/capistrano/capistrano/wiki
[phpdeploy_capistrano]: http://www.davegardner.me.uk/blog/2012/02/13/php-deployment-with-capistrano/
[Chef]: http://www.opscode.com/chef/
[chef_vagrant_and_ec2]: http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/
[Chef_cookbook]: https://github.com/opscode-cookbooks/php
[Chef_tutorial]: https://www.youtube.com/playlist?list=PLrmstJpucjzWKt1eWLv88ZFY4R1jW8amR
[apache_ant_tutorial]: http://net.tutsplus.com/tutorials/other/automate-your-projects-with-apache-ant/
[Travis CI]: https://travis-ci.org/
[Jenkins]: http://jenkins-ci.org/
[PHPCI]: http://www.phptesting.org/
[Teamcity]: http://www.jetbrains.com/teamcity/
[Deployer]: http://deployer.in/