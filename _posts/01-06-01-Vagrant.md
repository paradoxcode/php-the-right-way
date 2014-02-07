---
isChild: true
---

## Vagrant {#vagrant_title}

Poganjanje vaše aplikacije v različnih okoljih v razvoju in produkciji lahko pripelje do nenavadnih hroščev, 
ki se pojavijo pri zagonu v živo. Je tudi mučno vzdrževati posodobljena različna razvojna okolja z enakimi 
verzijami za vse knjižnice, ki so uporabljene, ko se dela v ekipi razvijalcev. 

Če razvijate v Windows okolju in nalagate na Linux (ali karkoli drugega od Windows okolja) ali razvijate v ekipi, 
bi bilo dobro razmisliti o uporabi virtualne naprave. To zveni mučno, vendar z uporabo [Vagrant-a][vagrant], lahko 
namestite enostavno virtualno napravo samo z nekaj koraki. Te osnovne škatle se lahko potem nastavi tudi ročno, ali 
pa lahko uporabite "provisioning" (rezervacijsko) programsko opremo, kot je [Puppet][puppet] ali [Chef][chef], ki 
to naredi za vas. Rezerviranje osnovne škatle je odličen način za zagotovitev, da je več škatel nameščenih v identični 
obliki in odstrani potrebo po vzdrževanju komplicirane namestitve seznama komand. Lahko tudi odstranite vašo osnovno 
škatlo in jo ponovno kreirate brez mnogih ročnih korakov, kar omogoča enostavno novo namestitev.

Vagrant naredi skupne mape, ki se uporabljajo za deljenje vaše kode med vašim gostiteljem in vašo virtualno napravo, kar 
pomeni, da lahko naredite in uredite vaše datoteke na vaši gostiteljski napravi in nato poženete kodo znotraj virtualne naprave.

### Malo pomoči

Če potrebujete malo pomoči za začetek uporabe Vagranta, so na voljo tri storitve, ki so lahko uporabne:

- [Rove][rove]: storitev, ki vam omogoča vnaprej genererati tipične Vagrant gradnje, PHP med opcijami na primer. Oskrbovanje
  je narejeno s Chef-om.
- [Puphpet][puphpet]: enostaven GUI, da nastavite virtualno napravo za PHP razvoj. **Močno osredotočeno na PHP**. Poleg
  lokalnih virtualnih naprav (VM), je lahko tudi uporabljen za postavitev na oblačne storitve. Oskrbovanje je narejeno s Puppet-om.
- [Protobox][protobox]: je nivo nad vagrant-om in spletni GUI za nastavitev virtualnih naprav za spletni razvoj. En YAML dokument krmili vse, kar je nameščeno na virtualni napravi.

[vagrant]: http://vagrantup.com/
[puppet]: http://www.puppetlabs.com/
[chef]: http://www.opscode.com/
[rove]: http://rove.io/
[puphpet]: https://puphpet.com/
[protobox]: http://getprotobox.com/
