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
Aloitin tehtävän tarkastamalla tarkastamalla, että Metasploitablella olisi käytössään tehtävässä haluttu tietokanta (tässä tapauksessa postgresql). Käytin tähän seuraavia komentoja:

```
systemctl status postgresql.service
sudo systemctl start postgresql.servic
```
<img width="642" height="191" alt="VirtualBox_Kali_07_09_2026_19_38_47_2" src="https://github.com/user-attachments/assets/1efcbbc5-c165-4936-868c-837214af2586" />

Saatuani postgresql-palvelun päälle, avasin yhteyden metasploitableen komennoilla:
```
sudo msfdb init

sudo msfconsole

sudo db_status
```
<img width="735" height="769" alt="VirtualBox_Kali_07_09_2026_19_43_33" src="https://github.com/user-attachments/assets/35a79bdf-1438-4a33-8b2c-7dd9dc663132" />

(HUOM! Muista oikeinkirjoituis, sillä kirjoitin itse aluksi useaan otteeseen msfdb komennon väärinpäin msfbd)

<img width="442" height="65" alt="VirtualBox_Kali_07_09_2026_19_44_28" src="https://github.com/user-attachments/assets/e6d8963f-8fb6-4a2d-a99d-83cf231ae775" />

Loin tehtävää varten itselleni myös workspacen, käyttämällä komentoa ```workspace -a h3``` ja otin tämän käyttööni komennolla ```workspace h3```.

<img width="289" height="103" alt="VirtualBox_Kali_07_09_2026_19_48_47" src="https://github.com/user-attachments/assets/6193c1d5-ec61-493a-ae8a-f45817c26933" />

Päästyäni tähän asti aloitin skannauksen komennolla ```db_nmap -sV 192.168.56.103```.

<img width="955" height="225" alt="VirtualBox_Kali_07_09_2026_19_52_43" src="https://github.com/user-attachments/assets/1c86e3b0-2d7c-4e7c-8186-d54a7b532e0a" />

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
