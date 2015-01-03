---
isChild: true
anchor:  vagrant
---

## Vagrant {#vagrant_title}

[Vagrant][vagrant] vam pomaga graditi vaše virtualne naprave na vrhu znanih virtualnih okolj in bo nastavil
ta okolja na osnovi ene nastavitvene datoteke.
Te naprave se lahko nastavi ročno ali pa lahko uporabite "provisioning" (rezervacijsko)
programsko opremo, kot je [Puppet][puppet] ali [Chef][chef], ki to naredi za vas. Rezerviranje osnovne škatle je odličen način
za zagotovitev, da je več škatel nameščenih v identični obliki in odstrani potrebo po vzdrževanju komplicirane
namestitve seznama komand. Lahko tudi odstranite vašo osnovno škatlo in jo ponovno kreirate brez mnogih ročnih korakov, kar omogoča
enostavno novo namestitev.

Vagrant naredi skupne mape, ki se uporabljajo za deljenje vaše kode med vašim gostiteljem in vašo virtualno napravo, kar
pomeni, da lahko naredite in uredite vaše datoteke na vaši gostiteljski napravi in nato poženete kodo znotraj virtualne naprave.

### Malo pomoči

Če potrebujete malo pomoči za začetek uporabe Vagranta, je na voljo nekaj storitev, ki so lahko uporabne:

- [Rove][rove]: storitev, ki vam omogoča vnaprej genererati tipične Vagrant gradnje, PHP med opcijami na primer. Oskrbovanje
  je narejeno s Chef-om.
- [Puphpet][puphpet]: enostaven GUI, da nastavite virtualno napravo za PHP razvoj. **Močno osredotočeno na PHP**. Poleg
  lokalnih virtualnih naprav (VM), je lahko tudi uporabljen za postavitev na oblačne storitve. Oskrbovanje je narejeno s Puppet-om.
- [Protobox][protobox]: je nivo nad vagrant-om in spletni GUI za nastavitev virtualnih naprav za spletni razvoj. En YAML dokument krmili vse, kar je nameščeno na virtualni napravi.
[Phansible][phansible]: ponuja vmesnik, ki je enostaven za uporabo in vam pomaga generirati t.i. Ansible Playbooks za PHP osnovane projekte.

[vagrant]: http://vagrantup.com/
[puppet]: http://www.puppetlabs.com/
[chef]: http://www.opscode.com/
[rove]: http://rove.io/
[puphpet]: https://puphpet.com/
[protobox]: http://getprotobox.com/
[phansible]: http://phansible.com/
