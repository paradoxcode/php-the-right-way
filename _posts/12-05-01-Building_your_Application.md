---
title:   Gradnja in postavitev vaše aplikacije
isChild: true
anchor: building_and_deploying_your_application
---

## Gradnja in postavitev vaše aplikacije {#building_and_deploying_your_application_title}

Če ugotovite, da delate ročne spremembe podatkovne baze ali poganjate vaše teste ročno, preden posodabljate vaše datoteke
(ročno), ponovno premislite! Z vsakim dodatnim ročnim opravilom potrebnim za postavitev nove verzije vaše aplikacije,
se možnosti za potencialno usodno napako povečajo. Ali če imate opravka z enostavno posodobitvijo, podrobnim procesom gradnje
ali celo strategijo zvezne integracije, je [avtomatizacija gradnje](http://en.wikipedia.org/wiki/Build_automation) vaš
prijatelj.

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

[Phing](http://www.phing.info/) je najenostavnejša pot za začetek z avtomatizirano postavitvijo v PHP svetu. S Phing-om
lahko kontrolirate vaše pakiranje, postavitev ali proces testiranja znotraj enostavne XML postavitvene datoteke. Phing
(ki je osnovan na [Apache Ant](http://ant.apache.org/) ponuja bogat nabor opravil, ki se jih ponavadi potrebuje za namestitev
ali posodobitev spletne aplikacije in je lahko razširjen z dodatnimi opravili po meri, napisanimi v PHP.

[Capistrano](https://github.com/capistrano/capistrano/wiki) je sistem za *vmesne do napredne programerje*, da lahko izvajajo
komande v strukturirani, ponovljivi poti na eni ali več oddaljenih naprav. Je pred-nastavljen za postavitev Ruby on Rails aplikacij,
čeprav ljudje z njim **uspešno postavljajo PHP sisteme**. Uspešna uporaba Capistrana zavisi na delovnem znanju Ruby-ja in Rake-a.

Dave Gardner-jeva objava na blogu [PHP Deployment with Capistrano](http://www.davegardner.me.uk/blog/2012/02/13/php-deployment-with-capistrano/)
je dobra začetna točka za PHP razvijalce, ki jih zanima Capistrano.

[Chef](http://www.opscode.com/chef/) je bolj postavitveno ogrodje, je zelo močno na Ruby-ju osnovano sistemsko integrirano ogrodje,
ki ne samo postavi vaše aplikacije, vendar lahko zgradi vaše celotno strežniško ogrodje ali virtualne naprave.

Chef viri za PHP razvijalce:

* [Blog serija iz treh delov o postavitvi LAMP aplikacije s Chef, Vagrant, in EC2](http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/)
* [Chef recepti, ki namestijo in nastavijo PHP 5.3 in PEAR paketni upravljalni sistem](https://github.com/opscode-cookbooks/php)

Nadaljnje branje:

* [Avtomatizacija vašega projekta z Apache Ant](http://net.tutsplus.com/tutorials/other/automate-your-projects-with-apache-ant/)
* [Maven](http://maven.apache.org/), ogrodje za gradnjo osnovan na Ant in [kako ga uporabljati s PHP](http://www.php-maven.org/)

### Zvezna integracija

> Continuous Integration is a software development practice where members of a team integrate their work frequently, 
> usually each person integrates at least daily — leading to multiple integrations per day. Many teams find that this 
> approach leads to significantly reduced integration problems and allows a team to develop cohesive software more 
> rapidly.

*-- Martin Fowler*

Obstaja več različnih poti za implementacijo zvezne integracije za PHP. Pred kratkim je [Travis CI](https://travis-ci.org/)
naredil odlično delo zvezne integracije, zaradi česar je realnost tudi za manjše projekte. Travis CI je gostovan servis zvezne
integracije za odprto kodno skupnost. Integriran je z GitHub-om in ponuja prvo razredno podporo za mnoge jezike, tudi PHP.

Nadaljnje branje:

* [Zvezna integracija z Jenkins](http://jenkins-ci.org/)
* [Zvezna integracija s PHPCI](http://www.phptesting.org/)
* [Zvezna integracija s Teamcity](http://www.jetbrains.com/teamcity/)
