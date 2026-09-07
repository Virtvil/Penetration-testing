# Harjoitus 3: EternalHomework

## x) Materiaalit:
### Jaswal 2020: Mastering Metasploit - 4ed: Chapter 1: Approaching a Penetration Test Using Metasploit
- Penetraatiotestauksen perusteet käyttäen Metasploittia.
- Koostuu seitsemästä osasta:
  1. Esivuorovaikutukset
  2. Tiedusteluvaihe
  3. Uhkamallinnus
  4. Haavoittuvuusanalyysi
  5. Hyödyntäminen
  6. Hyödyntämisen jälkeiset toimet
  7. Raportointi
- Metasploit Frameworkin perusteet sekä exploit-, post-exploit-, liitännäis- ja apumoduulien (auxiliary modules) käyttö Metasploitissa.

### nmap -sn
_-sn_ komento ohjeistaa Nmapia olemaan suorittamatta porttiskannausta kohteen tunnistamisen jälkeen, jolloin komento kertoo ainoastaan käytettävissä olevat isännät, jotka vastasivat tunnistuskyselyihin.

Tunnetaan usein myös _"ping"_-komentona.

## b) Tallenna porttiskannauksen tuloksia Metasploitin tietokantoihin.
Aloitin tehtävän avaamalla molemmat virtuaalikoneeni, Kalin, sekä Metasploitable 2:n. Seuraavaksi halusin, että Metasploitablella olisi käytössään tehtävässä haluttu tietokanta (tässä tapauksessa postgresql). Käytin tähän seuraavia komentoja Kali-koneellani:

```
systemctl status postgresql.service

sudo systemctl start postgresql.servic
```
<img width="642" height="191" alt="VirtualBox_Kali_07_09_2026_19_38_47_2" src="https://github.com/user-attachments/assets/1efcbbc5-c165-4936-868c-837214af2586" />

Saatuani postgresql-palvelun päälle, avasin yhteyden kali-laitteelta metasploitableen komennoilla:
```
sudo msfdb init

sudo msfconsole

sudo db_status
```

<img width="955" height="462" alt="VirtualBox_Kali_07_09_2026_20_05_26" src="https://github.com/user-attachments/assets/8d223acd-f77e-461e-9c32-2e8050054036" />

(HUOM! Muista oikeinkirjoitus, sillä kirjoitin itse aluksi useaan otteeseen msfdb komennon väärinpäin msfbd)

Loin tehtävää varten itselleni myös workspacen, käyttämällä komentoa ```workspace -a h3``` ja otin tämän käyttööni komennolla ```workspace h3```.

<img width="289" height="103" alt="VirtualBox_Kali_07_09_2026_19_48_47" src="https://github.com/user-attachments/assets/6193c1d5-ec61-493a-ae8a-f45817c26933" />

Päästyäni tähän asti aloitin metasploitablen skannauksen komennolla ```db_nmap -sV 192.168.56.104```. Osoite oli itselläni muistissa viime tehtävästä, mutta tämän saisi helposti tietoon käyttämällä kohdelaitteella ```ifconfig```-komentoa.

(Tässä tehtävän osiossa skannasin alkuun myös vahingossa myös Kali-koneen (192.168.56.103), joka näkyykin myös tallentuneena harjoituksen c-osiossa.)

<img width="935" height="578" alt="VirtualBox_Kali_07_09_2026_20_03_19" src="https://github.com/user-attachments/assets/b42dd711-f6ac-4e3b-bbe6-4da71a680956" />


Kannattaa skannata.

## c) Tarkastele Metasploitin tietokantoihin tallennettuja tietoja komennoilla "hosts" ja "services". 

Seuraavaksi käyttäen komentoja ```hosts``` ja ```services``` aloin tarkastelemaan tietokantaan tallentuneita kohdekoneita (saatu tietoon ```nmap```-komennoilla), sekä myös tallentuneita palveluita.

<img width="955" height="650" alt="VirtualBox_Kali_07_09_2026_20_10_36" src="https://github.com/user-attachments/assets/d61847b5-8570-4104-99e5-ba0f383652c8" />

Tämän jälkeen komennolla ```services -h``` pystymme tarkkailemaan mahdollisia tapoja rajata hakuja. ```-S``` parametri kuulostaakin parhaalta tähän touhuun! Rajataampas haku siis myöskin edellisessä tehtävässä tutuksi tulleeseen _java-rmi_-palveluun käyttäen komentoa ```services -S java-rmi```!

<img width="937" height="478" alt="VirtualBox_Kali_07_09_2026_20_18_18" src="https://github.com/user-attachments/assets/61e58f6b-36c7-43ef-bf71-e6cab23e7247" />

## d) Internet famous. 

Tutkikaamme hieman lisää tätä java-rmi exploittia!

National Vulnerability Database (NIST), kertoo Java RMI -palvelimen oletusasetuksien ovat turvattomuudesta, joka mahdollistaa Java-koodin suorittamisen URL-osoitteesta, sillä ohjelma käyttää RMI:n hajautetun roskienkeruun (Distributed Garbage Collector) metodia. Kyseinen haitta vaikutti palveluun vuosista 2001 jopa 2020 asti! Huh!

<img width="940" height="225" alt="VirtualBox_Kali_07_09_2026_20_30_32" src="https://github.com/user-attachments/assets/f667f799-c720-47c3-a5bf-71d2a79249f6" />

## e) Vertaile nmap:n omaa tiedostoon tallennusta (-oA foo) ja db_nmap:n tallennusta tietokantoihin. 

Mitkä ovat eri tiedostomuotojen ja Metasploitin tietokannan hyvät puolet?

### Metasploitable: 
Tallentaa nmap tulokset suoraan tietokantaan:
- Tietokannasta datan voi viedä ulos ja sisään helposti käyttäjän haluamalla tavalla.
- Pääsy tietokantaan sallii nopean ja luotettavan pääsyn skannauksien tuloksiin.

### Nmap:in oma tiedosto tallennus (-oA foo)
Skannauksien tulostus on mahdollista kolmeen eri muotoon:
- XML
- Grepable, helppo tiedostojen luku (grep-komento).
- Normal


## f) Murtaudu Metasploitablen vsftpd-palveluun.

Aika kaivaa sormikkaat esiin ja käydä hyökkäykseen! Aloitin etsimällä Metasploitablen valmiita hyökkäyspaketteja käyttämällä komentoa ```search vsftpd```. Tämän avulla pääsin valitsemaan itselleni käyttöön haluamani moduulin, joista valitsin moduulin 1 komennolla ```use 1```.

<img width="955" height="515" alt="VirtualBox_Kali_07_09_2026_20_51_42" src="https://github.com/user-attachments/assets/8aa8e762-4172-4d09-b6e6-458875d7fbec" />

Tämän jälkeen pääsinkin valitsemaan mitä kyseisellä hyökkäyksellä haluaisin tehdä. Tietääkseni lisää, käytin komentoa ```show options```, tietääkseni hieman lisää hallussani olevista komennoista!

<img width="955" height="785" alt="VirtualBox_Kali_07_09_2026_20_52_50" src="https://github.com/user-attachments/assets/bd4f57f9-6c65-4a9e-ba51-c925ccbd4632" />

Halusin seuraavaksi varmistaa hyökkääväni oikealle koneelle, joten asetin itseni komennon ajajaksi 

```set LHOST 192.168.56.103```

Sekä Metasploitablen kohteekseni komennolla 

```set RHOST 192.168.56.104```

Ja ei muutakun rankkaa hakkerointia antamalla komento 

```exploit```

<img width="942" height="226" alt="VirtualBox_Kali_07_09_2026_21_00_04" src="https://github.com/user-attachments/assets/f552806b-523e-47b8-878e-42b4f9cd625b" />

<img width="498" height="280" alt="hacker-hackerman" src="https://github.com/user-attachments/assets/85d9cb9c-6bc7-4ab8-b0f4-f9963fdda48d" />


## g) Kerää levittäytymisessä (lateral movement) tarvittavaa tietoa metasploitablesta. 

Analysoi tiedot. Selitä, miten niitä voisi hyödyntää.

## h) Murtaudu Metasploitableen jollain toisella tavalla. 

(Jos tämä kohta on vaikea, voit tarvittaessa turvautua verkosta löytyviin läpikävelyohjeisiin. Merkitse silloin raporttiin, missä määrin tarvitsit niitä).

## i) Demonstroi Meterpretrin ominaisuuksia.

## j) Tallenna shell-sessio tekstitiedostoon script-työkalulla tai tmux:lla.

## k) Pivot point. 

Laita kaikki harjoituksen tiedostot (script -fa, nmap -oA...) samaan kansioon. Hae sopiva pivot point (sovellus, versio, osoite, MAC-numero) 'grep -r' -komennolla. Keksi uskottava esimerkkikysymys, johon haet vastausta.

## l) Attaaack! 

Mitä Mitre Attack taktiikoita ja tekniikoita käytit tässä harjoituksessa?

# Lähteet:
Jaswal 2020: Mastering Metasploit - 4ed: Chapter 1: Approaching a Penetration Test Using Metasploit. Luettavissa: https://learning.oreilly.com/library/view/mastering-metasploit/9781838980078/B15076_01_Final_ASB_ePub.xhtml Luettu 7.9.20206

NIST, https://nvd.nist.gov/vuln/detail/cve-2020-9761

nmap manual, Host Discovery. Luettavissa: https://nmap.org/book/man-host-discovery.html Luettu 7.9.2026
