# kotitehtävä3

# 

a) Latasimme Typoran ja teimme tekstitiedoston. Tutustuimme Typoraan ja jatkoimme tehtävää.

# d) Näytä omalla git-varastollasi esimerkit komennoista ‘git log’, ‘git diff’ ja ‘git blame’. Selitä tulokset.

Komennot:

***git log*** = komento näyttää tiedoston lokitiedot, esim: tekijän nimi, sähköposti, milloin tiedosto on tehty

***git diff*** = näyttää tiedostojen sisällä tehdyt muutokset

***git blame*** = komento näyttää kuka teki tiedostoon muutokset, kuka muutti tiedoston rivit ja miksi



e) Tein tahallaan turhan muutoksen gittiin, jonka jälkeen tein komennon ***git reset --hard***, joka tuhosi huonot muutokset ja haki viimeisen tallennettun version githubista.



# f) Tee uusi salt-moduli. Voit asentaa ja konfiguroida minkä vain uuden ohjelman: demonin, työpöytäohjelman tai komentokehotteesta toimivan ohjelman. Käytä tarvittaessa ‘find -printf “%T+ %p\n”|sort’ löytääksesi uudet asetustiedostot. (Tietysti eri ohjelma kuin aiemmissa tehtävissä, tarkoitushan on harjoitella Salttia)

Asensin fail2ban ohjelman

***sudo apt-get update***

***sudo apt-get -y install fail2ban***

Tämän jälkeen kopioin jail conf tiedoston jail localiin.

***sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local***

Tämän jälkeen käynnistin fail2ban uudestaan.

***sudo systemctl restart fail2ban***

Seuraavaksi tein hakemiston fail2ban tiedostolle.

***sudo mkdir /srv/salt/fail2ban***

Kopioin sinne tiedoston.

***sudo cp /etc/fail2ban/jail.local /srv/salt/fail2ban***

Loin sls tiedoston.

***sudoedit /srv/salt/fail2ban.sls***

fail2ban:
  pkg.installed

/etc/fail2ban/jail.local:
  file.managed:
    – source: salt://fail2ban/jail.local

fail2banservice:
  service.running:
    – name: fail2ban
    – file: /etc/fail2ban/jail.local

Lopuksi testasin fail2ban.

***sudo salt '*' state.apply fail2ban***

ID: fail2ban

Function: pkg.installed

Result: True

Comment: All specified packages are already installed

Started: 12:40:01.857314

Duration: 1592.934 ms



ID: /etc/fail2ban/jail.local

Function: file.managed

Result: True

Comment: File /etc/fail2ban/jail.local is in the correct state

Started: 12:40:03.455464

Duration: 36.006 ms



ID: fail2banservice

Function: service.running

Name: fail2ban

Result: True

Comment: The service fail2ban is already running

Started: 12:40:03.502377

Duration: 81.333 ms



Summary for samu



Succeeded: 3

Failed: 0

Total states run: 3

Total run time: 1.710 s



Kaikki toimii!



**Lähteet:**

Käytin sivustoja:

www.terokarvinen.com

https://hannukankkunen.wordpress.com/2018/12/10/palvelinten-hallinta-h3/

