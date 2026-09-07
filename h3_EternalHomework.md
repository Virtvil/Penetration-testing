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

(HUOM! Muista oikeinkirjoituis, sillä kirjoitin itse aluksi useaan otteeseen msfdb komennon väärinpäin msfbd)

Loin tehtävää varten itselleni myös workspacen, käyttämällä komentoa ```workspace -a h3``` ja otin tämän käyttööni komennolla ```workspace h3```.

<img width="289" height="103" alt="VirtualBox_Kali_07_09_2026_19_48_47" src="https://github.com/user-attachments/assets/6193c1d5-ec61-493a-ae8a-f45817c26933" />

Päästyäni tähän asti aloitin metasploitablen skannauksen komennolla ```db_nmap -sV 192.168.56.104```. Osoite oli itselläni muistissa viime tehtävästä, mutta tämän saisi helposti tietoon käyttämällä kohdelaitteella ```ifconfig```-komentoa.

<img width="935" height="578" alt="VirtualBox_Kali_07_09_2026_20_03_19" src="https://github.com/user-attachments/assets/b42dd711-f6ac-4e3b-bbe6-4da71a680956" />


Kannattaa skannata.

## c) Tarkastele Metasploitin tietokantoihin tallennettuja tietoja komennoilla "hosts" ja "services". 

## d) Internet famous. 

Etsi Metasploitablen mukana tulevista hyökkäyksistä (en: exploits; search) sellainen, joka on ollut julkisuudessa.

## e) Vertaile nmap:n omaa tiedostoon tallennusta (-oA foo) ja db_nmap:n tallennusta tietokantoihin. 

## f) Murtaudu Metasploitablen vsftpd-palveluun.

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

nmap manual, Host Discovery. Luettavissa: https://nmap.org/book/man-host-discovery.html Luettu 7.9.2026
