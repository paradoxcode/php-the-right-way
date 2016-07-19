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


### Orodja za namestitev

Orodja za namestitev lahko opišemo kot zbirko skript, ki opravljajo pogosta opravila namestitve programske opreme. Orodje za namesitev ni del vaše aplikacije, vendar deluje na vaši aplikaciji od 'zunaj'.

Na voljo je ogromno odprtokodnih orodij, ki so na voljo za pomoč pri avtomatizirani gradnji in namestitvi. Nekatera so napisana v PHP,
nekatera ne. To vas ne bi smelo ovirati pri njihovi uporabi, če so bolj primerna za določeno nalogo. Tu je nekaj primerov:

[Phing] lahko krmili vaše procese pakiranja, postavitve ali testiranja iz XML postavitvene datoteke. Phing (ki je osnovan na [Apache Ant]) ponuja bogat nabor opravil, ki so ponavadi potrebna za namestitev ali posodobitev spletne aplikacije, in se ga lahko razširi z dodatnimi opravili po meri, napisanimi v PHP. Je stabilno in močno orodje, ki je na voljo že dolgo časa, vendar se ga lahko dojema za nekoliko staromodno zaradi načina obravnave konfiguracije (XML datoteke).

[Capistrano] je sistem za *programerje z nadaljevalnim do naprednim znanjem*, da lahko izvajajo ukaze na strukturiran, ponovljiv način na eni ali več oddaljenih naprav. Je prednastavljen za namestitev aplikacij Ruby on Rails, čeprav z njim lahko uspešno nameščate PHP sisteme. Uspešna uporaba Capistrana zavisi na praktičnem znanju Ruby-ja in Rake-a. Dave Gardner-jeva objava na blogu [PHP Deployment with Capistrano][phpdeploy_capistrano] je dobro izhodišče za PHP razvijalce, ki jih zanima Capistrano.

[Rocketeer] je dobil inspiracijo in filozofijo iz ogrodja Laravel. Cilj je hitrost, elegantnost in enostavna uporaba s smiselnimi privzetimi nastavitvami. Vsebuje več strežnikov, več razvojnih stopenj, atomske namestitve in vzporedno izvedene namestitve. Vse v orodju se lahko zamenja ali razširi med delovanjem in vse je napisano v PHP.

[Deployer] je orodje za namestitev napisano v PHP, je enostavno in funkcionalno. Opravila poganja vzporedno, opravlja atomske namestitve in obdrži konsistentnost med strežniki. Na voljo so recepti pogostih opravil za Symfony, Laravel, Zend Framework in Yii. Younes Rafie-jev članek [Easy Deployment of PHP Applications with Deployer][phpdeploy_deployer] je odličen vodič za namestiev vaše aplikacije s tem orodjem.

[Magallanes] je drugo orodje napisano v PHP z enostavno konfiguracijo v YAML datotekah. Podpira več strežnikov in okolij, atomske namestitve in ima vgrajena opravila, ki jih lahko uporabite pri pogostih orodjih in ogrodjih.

#### Nadaljnje branje

* [Avtomatizirajte vaše projekte z Apache Ant][apache_ant_tutorial]
* [Espertne namestitve PHP][expert_php_deployments] - brezplačna knjiga o namestitvi s Capistrano, Phing in Vagrant.
* [Namestitev PHP aplikacij][deploying_php_applications] - plačljiva knjiga z najboljšimi praksami in orodji za namestitve PHP.

### Strežniške provizije

Upravljanje in konfiguracija strežnikov je lahko zastrašujoče opravilo pri večih strežnikih. Na voljo so orodja za ravnanje s tem, tako da lahko avtomatizirate vašo infrastrukturo in zagotovite, da imate pravilno nastavljene strežnike. Pogosto se integrirajo z večjimi ponudniki oblačnega gostovanja (Amazon Web Services, Heroku, DigitalOcean itd.) za upravljanje instanc, kar naredi skaliranje aplikacije veliko enostavnejše.

[Ansible] je orodje, ki upravlja vašo infrastrukturo preko YAML datotek. Je enostaven za začeti in lahko upravlja kompleksne in večje apllikacije. Na voljo je API za upravljanje oblačnih instanc in lahko jih upravlja preko dinamičnega inventarja z uporabo določenih orodij.

[Puppet] je orodje, ki ima svoj lasten jezik in vrste datotek za upravljanje strežnikov in konfiguracij. Lahko se ga uporabi v namestitvi master/klient ali pa se ga uporablja v "master-less" načinu. V načinu master/klient, bodo klienti raziskali osrednje master-je za novo konfiguracijo po nastavljenih intervalih in se posodobili, če je potrebno. V načinu master-less, lahko pošljete spremembe vašim vozliščem.

[Chef] je močno, na Ruby-ju osnovano, sistemsko ogrodje za integracijo, s katerim lahko zgradite vaše celotno strežniško okolje ali virtualne naprave. Dobro se integrira z Amazon Web Services preko njihove storitve imenovane OpsWorks.

#### Nadaljnje branje:

* [Vodič Ansible][an_ansible_tutorial]
* [Ansible za DevOps][ansible_for_devops] - plačljiva knjiga z vsem o Ansible
* [Ansible za AWS][ansible_for_aws] - plačljiva knjiga o integraciji Ansible in Amazon Web Services
* [Blog serija iz treh delov o postavitvi LAMP aplikacije s Chef, Vagrant, in EC2][chef_vagrant_and_ec2]
* [Chef recepti, ki namestijo in nastavijo PHP in PEAR paketni upravljalni sistem][Chef_cookbook]
* [Chef serija video vodičev][Chef_tutorial]

### Zvezna integracija

> Continuous Integration is a software development practice where members of a team integrate their work frequently,
> usually each person integrates at least daily — leading to multiple integrations per day. Many teams find that this
> approach leads to significantly reduced integration problems and allows a team to develop cohesive software more
> rapidly.

*-- Martin Fowler*

Obstaja več različnih poti za implementacijo zvezne integracije za PHP. [Travis CI] je
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
[phpdeploy_deployer]: http://www.sitepoint.com/deploying-php-applications-with-deployer/
[Chef]: https://www.chef.io/
[chef_vagrant_and_ec2]: http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/
[Chef_cookbook]: https://github.com/chef-cookbooks/php
[Chef_tutorial]: https://www.youtube.com/playlist?list=PL11cZfNdwNyPnZA9D1MbVqldGuOWqbumZ
[apache_ant_tutorial]: http://net.tutsplus.com/tutorials/other/automate-your-projects-with-apache-ant/
[Travis CI]: https://travis-ci.org/
[Jenkins]: http://jenkins-ci.org/
[PHPCI]: http://www.phptesting.org/
[Teamcity]: http://www.jetbrains.com/teamcity/
[Deployer]: https://github.com/deployphp/deployer
[Rocketeer]: http://rocketeer.autopergamene.eu/
[Magallanes]: http://magephp.com/
[expert_php_deployments]: http://viccherubini.com/assets/Expert-PHP-Deployments.pdf
[deploying_php_applications]: http://www.deployingphpapplications.com
[Ansible]: https://www.ansible.com/
[Puppet]: https://puppet.com/
[ansible_for_devops]: https://leanpub.com/ansible-for-devops
[ansible_for_aws]: https://leanpub.com/ansible-for-aws
[an_ansible_tutorial]: https://serversforhackers.com/an-ansible-tutorial
