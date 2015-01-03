---
title:   Vedenjsko usmerjen razvoj
isChild: true
anchor:  behavior_driven_development
---

## Vedenjsko usmerjen razvoj {#behavior_driven_development_title}

Na voljo sta dva različna tipa vedenjsko usmerjenega razvoja (BDD): SpecBDD in StoryBDD. SpecBDD se osredotoča na tehnično obnašanje kode,
medtem ko se StoryBdd osredotoča na poslovna ali lastnostna vedenja ali interakcije. PHP ima ogrodja za oba BDD tipa.

Pri StoryBDD pišete zgodbe, ki upisujejo vedenje vaše aplikacije. Te zgodbe
se nato lahko požene kot dejanske teste napram vaši aplikaciji. Uporabljeno ogrodje v PHP aplikacijah za StoryBDD
je Behat, ki je bil navdihnjen od Ruby-jevega [Cucumber](http://cukes.info) projekta in implementira Gherkin DSL
za opisovanje lastnosti vedenja.

Pri SpecBDD pišete specifikacije, ki opisujejo, kako bi se vaša dejanska koda morala vesti. Namesto testiranja
funkcije ali metode, opisujete, kako bi se funkcija ali metoda morala vesti. PHP ponuja PHPSpec ogrodje za ta namen.
To ogrodje je navdihnjeno od [Rspec projekta](http://rspec.info/) za Ruby.

### BDD Links

* [Behat](http://behat.org/), StoryBDD ogrodje za PHP, navdihnjeno od Ruby-jevega [Cucumber](http://cukes.info/) projekta;
* [PHPSpec](http://www.phpspec.net/), SpecBDD ogrodje za PHP, navdihnjeno od Ruby-jevega [RSpec](http://rspec.info/) projekta;
* [Codeception](http://codeception.com) je celotno testno ogrodje, ki uporablja BDD principe.

