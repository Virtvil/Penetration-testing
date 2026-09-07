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
