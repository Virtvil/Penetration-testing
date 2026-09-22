# Harjoitus 5: Elokuu2026!
## x) Materiaalit:
### Karvinen 2022: Cracking Passwords with Hashcat
- Sanakirjojen (lista yleisimmistä salasanoista) avulla salasanojen murto helpottuu
- Hashcat pystyy tunnistamaan salasanojen merkkijonoista mahdolliset käytetyt salausfunktiot ja ehdottaa näiden avulla mahdollisia tapoja purkaa salasanat.
- ```Status: Cracked``` kertoo salasanan onnistuneesta murrosta, sekä ilmoittaa myös mikä sanakirjan sana on oikea.
- ```Status: Exhausted``` kertoo, että kaikki sanakirjan sanat on käyty läpi, eikä yksikään niistä ole oikea haettu salasana.
- Ajettaessa näytönohjaimella on haun suoritus moninkertaisesti nopeampi.

Bitwarden sivusto kertoo hash olevan yksisuuntainen matemaattinen funktio, joka muuntaa selväkielisen salasanan tietynmittaiseksi merkkijonoksi, jossa merkit ovat sekaisin, mahdollistaen turvallisen tunnistautumisen ilman varsinaisen salasanan tallentamista.
### Karvinen 2023: Crack File Password With John
- Githubista ladattavissa oleva John the Ripper, Jumbo versio, pystyy murtamaan todella monia tiedostomuotoja/formaatteja.
- Yllätyin kuinka hankalasti selvinnyt salasana on sijoitettu tuloksiin.
## a) Asenna Hashcat ja testaa sen toiminta murtamalla esimerkkisalasana.
Asennus onnistuu komennoilla:
```
sudo apt-get update
sudo apt install hashcat
sudo apt install hashid
```
<img width="1900" height="688" alt="VirtualBox_Kali_22_09_2026_14_42_20" src="https://github.com/user-attachments/assets/fd87d26f-f82e-48b4-9c98-5e590b07b7ca" />

Olin asentanut hashcatin itse jo aiemmin oppitunnin aikana, mutta tässä silti todistus onnistuneista asennuksista.

Lähdin seuraavaksi purkamaan simppeliä ```Password123```-salasanaa sillä olin 100% varma tämän löytyvän mistä tahansa valmiista sanakirjasta.

Loin harjoitukselleni uuden harjoitus5-kansion (```mkdir harjoitus5```) ja siirryin tämän sisälle luomaan ```nano hash```-komennolla itselleni tiedoston jota ryhdyin purkamaan!

<img width="1012" height="284" alt="VirtualBox_Kali_22_09_2026_14_47_15" src="https://github.com/user-attachments/assets/e79ba68b-0187-4de5-b5be-cec4fb3bd8dc" />

Tämän jälkeen ryhdyin salaamaan valitsemaamme ```Password123```-salasanaa md5-funktiolla. Tähän käytämme seuraavaa komentoa:
```
echo -n 'Password123' |md5sum
```

Joka antaa meille kryptatun salasanan:
```
42f749ade7f9e195bf475f37a44cafcb
```

Kopioimme ja siirrämme tämän aiemmin jo tutulla ```nano hash```-komennolla harjoitustiedostoomme.

<img width="396" height="501" alt="VirtualBox_Kali_22_09_2026_14_57_54" src="https://github.com/user-attachments/assets/8b1d053e-0fc5-402c-8725-525d435f0ade" />

Ladataan seuraavaksi suosittu sanakirja salasanoille, Rockyou! Lataus onnistuu komennoilla:
```
wget https://github.com/danielmiessler/SecLists/raw/master/Passwords/Leaked-Databases/rockyou.txt.tar.gz
tar xf rockyou.txt.tar.gz
rm rockyou.txt.tar.gz
```
<img width="1885" height="684" alt="VirtualBox_Kali_22_09_2026_15_10_01" src="https://github.com/user-attachments/assets/6e53b352-1828-4f7f-aec5-1d74d96e0ad6" />

Nyt meillä on sanakirja salasanoille tekstimuodossa! 

Tässä vaiheessa työskennellessä virtuaalikoneella on tälle asennettava jonkinlainen toolkit, jonka avulla hashcat pystyy läpikäymään sanakirjaamme. Tähän käy esimerkiksi OpenCL CPU-runtime, jonka pystyy asentamaan komennolla: ```sudo apt install -y pocl-opencl-icd```. 

Asennuksen jälkeen pystymme ryhtymään käymään läpi salasanoja! Komento ```hashid -m 42f749ade7f9e195bf475f37a44cafcb``` antaa meille ehdotuksen millä salausfunktiolla salasanamme on kryptattu.

<img width="504" height="424" alt="VirtualBox_Kali_22_09_2026_15_30_40" src="https://github.com/user-attachments/assets/c1c1ef84-874a-432f-b74c-a335eadb597f" />

M5 ollessa käytetyin salausmuoto, käyttäkäämme sitä (vaikka tässä tehtävässä tiedämmekin itse salanneemme salasanamme tällä)! Käytetään seuraavaa komentoa:
```
hashcat -m 0 '42f749ade7f9e195bf475f37a44cafcb' rockyou.txt -o solved
```

<img width="1319" height="535" alt="VirtualBox_Kali_22_09_2026_15_34_14" src="https://github.com/user-attachments/assets/1d9474ba-4cde-436d-bd84-cfa0b4cd8952" />

<img width="1318" height="540" alt="VirtualBox_Kali_22_09_2026_15_35_15" src="https://github.com/user-attachments/assets/feaf9fd3-bcf9-4751-9271-41cc798ee606" />


Cracked-rivi kertoo meille salasanan paljastuneen! Tarkistetaan salasana vielä komennolla ```cat solved```.

<img width="424" height="118" alt="VirtualBox_Kali_22_09_2026_15_36_39" src="https://github.com/user-attachments/assets/2a9f8fd1-899e-49f3-a5f5-c5677533e4c0" />

Salasana onnistuneesti murrettu!
## c) Asenna John the Ripper ja testaa sen toiminta murtamalla jonkin esimerkkitiedoston salasana.
Seuraavaksi ryhdyin asentamaan _John the Ripperiä_. Asennuksen ohjeissa käytettiin komentoa ```sudo apt-get -y install micro bash-completion git build-essential libssl-dev zlib1g zlib1g-dev zlib-gst libbz2-1.0 libbz2-dev atool zip wget```, mutta asennus antoi ilmoituksen ettei pakettia ```zlib-gst``` löydy. Kokeilinkin uudelleen tiputtamalla komennon ```zlib-gst``` osan ja pääsin jatkamaan asennusta onnistuneesti komennolla:
```
sudo apt-get -y install micro bash-completion git build-essential libssl-dev zlib1g zlib1g-dev libbz2-1.0 libbz2-dev atool zip wget
```

<img width="1131" height="301" alt="VirtualBox_Kali_22_09_2026_17_37_53" src="https://github.com/user-attachments/assets/e0adee22-590b-4f57-bbb3-48d7b9342b3d" />


Ryhdyinkin tämän jälkeen asentamaan tarkemmin ohjelman _Jumbo_-versiota, jonka asennukseen käytin komentoa:
```
git clone --depth=1 https://github.com/openwall/john.git
```

<img width="697" height="171" alt="VirtualBox_Kali_22_09_2026_17_26_36" src="https://github.com/user-attachments/assets/851b57e1-2024-4ce5-96ee-c44356dd2084" />


Kopioituani git-kansion suuntasin hakemistoon ```/john/src/``` jossa suoritin ```./configure```-komennolla jumbo-version konfiguroinnin.

<img width="739" height="468" alt="VirtualBox_Kali_22_09_2026_17_38_41" src="https://github.com/user-attachments/assets/1b2e7f50-c568-46d9-96fd-a7bd0f3e040d" />

Onnistunut konfigurointi.

Konfiguroinnin päätyttyä ohjelma pyyltää meiltä _compile_-käskyä muodossa ```make -s clean && make -sj2```.

<img width="689" height="105" alt="VirtualBox_Kali_22_09_2026_17_47_48" src="https://github.com/user-attachments/assets/4e4d87d8-4b84-4a9c-a3c0-2e25415b6683" />

Löydämme kompilaation jälkeen ```.../john/run```-kansion sisältä ohjelman skriptit.

<img width="1865" height="516" alt="VirtualBox_Kali_22_09_2026_17_49_17" src="https://github.com/user-attachments/assets/9fedf8f9-71a5-445a-bba6-a0ab869a0d89" />

Seuraavaksi latasin itselleni tehtävänannosta murrettavan _Zip_-tiedoston _harjoitus5_-kansioon komennolla:
```
wget https://TeroKarvinen.com/2023/crack-file-password-with-john/tero.zip
```

<img width="1879" height="272" alt="VirtualBox_Kali_22_09_2026_17_53_05" src="https://github.com/user-attachments/assets/eb7d1f5a-f58c-40f2-a812-d61c455092e8" />

Yritetään avata tiedosto ```unzip tero.zip```-komennolla.

<img width="668" height="155" alt="VirtualBox_Kali_22_09_2026_18_00_30" src="https://github.com/user-attachments/assets/53cb733b-6f0c-4ba6-8589-a42fe9cabb57" />

Tiedosto pyytää salasanaa. Olisipa meillä tapa saada se selville... Kuten juuri lataamamme John the Ripper! Käytetään seuraavia komentoja ajamaan meille selvittävät skriptit:

```
john/run/zip2john tero.zip > tero.zip.hash  

john/run/john tero.zip.hash  
```

<img width="1165" height="369" alt="VirtualBox_Kali_22_09_2026_18_05_52" src="https://github.com/user-attachments/assets/da1dcc6b-e884-4b69-8564-3fc1bab7fb18" />

Ahaa! Salasanamme on ```butterfly```! Unzipataan tiedosto salasanan avulla komennolla:

```
unzip -P butterfly tero.zip

```

<img width="658" height="250" alt="VirtualBox_Kali_22_09_2026_18_08_24" src="https://github.com/user-attachments/assets/7341e02b-d1d4-4413-b66f-0790fd2e0239" />

Ja paketin sisältö on meidän!
## e) Tiedosto. Tee itse tai etsi verkosta jokin salakirjoitettu tiedosto, jonka saat auki. Murra sen salaus. (Jokin muu formaatti kuin aiemmissa alakohdissa kokeilemasi).
## f) Tiiviste. Tee itse tai etsi verkosta salasanan tiiviste, jonka saat auki. Murra sen salaus. (Jokin muu formaatti kuin aiemmissa alakohdissa kokeilemasi. Voit esim. tehdä käyttäjän Linuxiin ja murtaa sen salasanan.)
Tutkiessani muita tiivisteitä esiin pomppasi useita vaikeammin ratkottavia salauksia, mutta näiden purkamisen varoitettiin kestävän. Tämän takia päädyinkin _SHA_-tyypin salaukseen ja tälle yleisimpään _SHA265_-tiivisteeseen. Päätin käyttää tehtävässä tehtävännimikettä ```Elokuu2026``` uutena murrettavana salasanana. Aloitin luomalla tiivisteen käyttäen komentoa:

```
echo -n 'Elokuu2026' | sha256sum
```

Ja tallensin tästä saadun tiivisteen nano-komennolla _Fsinchat_-tekstitiedostoon. Tämän jälkeen varmistin tunnistaako hashid tiedoston salauksen komennolla ```hashid Fsinchat```. 

<img width="669" height="408" alt="VirtualBox_Kali_22_09_2026_20_12_23" src="https://github.com/user-attachments/assets/925a7ecc-2fd9-43fe-85c5-df0652703f19" />

Seuraavaksi tarkistin minkä hashcat moodin haluan käyttöön purkamaan salausta komennolla: 
```
hashid -m 00e3d8962c8d9adfbb2ab7a2cf8c6c2fa51d6f01b4382b1dec84feb95e8208c4
```

Salauksen purkuun käytetään mode 1400, joten seuraavaksi käytettävä komentomme onkin:
```
hashcat -m 1400 -O '00e3d8962c8d9adfbb2ab7a2cf8c6c2fa51d6f01b4382b1dec84feb95e8208c4' haistpassu -o solved2
```

HUOM! Komennossa ei käytetä rockyou.txt, vaan seuraavassa tehtävässä g luotua uutta haistpassu sanakirjaa, joka sisältää lisättyjä suomenkielisiä salasanoja!

Käytämme myös komennossa solved2, sillä normaali solved tiedosto sisältää edellisessä tehtävän ratkaistun salasanan.

<img width="1265" height="688" alt="VirtualBox_Kali_22_09_2026_20_18_44" src="https://github.com/user-attachments/assets/0f267707-cf01-401c-b885-5bbff7f24783" />

<img width="682" height="732" alt="VirtualBox_Kali_22_09_2026_20_19_25" src="https://github.com/user-attachments/assets/3b9ef872-1ab6-4558-bf11-7de588e09d7a" />

Salasana murrettu! Tutkitaanpas tutulla ```cat solved2```-komennolla.

<img width="625" height="67" alt="VirtualBox_Kali_22_09_2026_20_23_57" src="https://github.com/user-attachments/assets/ec177acd-c1e1-462b-89a6-649081e9343c" />

## g) Sanakirja. Oman sanakirjan teko parantaa onnistumismahdollisuuksia. Demonstroi, kuinka teet oman sanakirjan hashcat:n tai john:iin.
Oman sanakirjan voi luoda esimerkiksi kopioimalla rockyou.txt sanakirjan sisällön ja lisätä siihen vaikkapa yleisimpiä Suomalaisia versioita salasanoista:

```cp rockyou.txt haistpassu``` kopioi rockyou-sanakirjan sisälön uuteen _haistpassu_-tiedostoon. Tämän jälkeen komennolla ```nano haistpassu``` voit lisätä listalle itse yleisimmin käytettyjä salasanoja, kuten esimerkiksi _Elokuu2026_, _salasana123_ tai muita vastaavia tietoturvan ihmeitä!

<img width="694" height="242" alt="VirtualBox_Kali_22_09_2026_18_25_47" src="https://github.com/user-attachments/assets/12f46ac3-5f40-40f1-bc78-750005b867c7" />

<img width="340" height="297" alt="VirtualBox_Kali_22_09_2026_18_24_35" src="https://github.com/user-attachments/assets/acb07160-9c7a-4760-91b1-2cccbe03f88b" />

## h) Hash rules. Näytä esimerkki HashCatin sääntöjen käytöstä (rules).
Hashcat.net Rule-based Attack kertoo, että lisäämällä erilaisia sääntöjä komennoille pystymme muokkaamaan sanakirjoista haettuja salasanoja. Esimerkkisääntöjä ovat 
```
l - Vaihtaa haetun salasanan kaikki kirjaimet pieniksi
u - Vaihtaa haetun salasanan kaikki kirjaimet suuriksi
c - Vaihtaa haetun salasanan ensimmäisen kirjaimen isoksi, loput tekstistä pieneksi
C - Vaihtaa haetun salasanan ensimmäisen kirjaimen pieneksi, loput tekstistä isoksi
r - Kääntää haetun salasanan ympäri 
```

Hashcat sisältää myös valmiita sääntömuunnoksia, jotka voit lisätä komentoon jotta tämä kävisi läpi automaattisesti erilaisia versioita salasanoista!

Esimerkiksi best66.rule sisältää 66 yksittäistä muunnossääntöä. Hashcat hyödyntää näitä sääntöjä ja testaa nopeasti yleisiä muutoksia. Jos esimerkiksi tehtävässä f olevassa salasanassa olisikin pieni kirjain edessä, testaisi sääntö automaattisesti myös version pienellä kirjaimella. 

Voisimme aiemmassa tehtävässä f ajaa seuraavanlaisen komennon jotta tämä testaisi myös kaikki yleisimmät vaihtelut salasanoistamme:

```
hashcat -m 1400 -O Fsinchat haistpassu -r /usr/share/hashcat/rules/best66.rule -o solved66
```

Valitettavasti kuitenkin komennon ajaminen jo ratkaistulle salasanalle antaa meille _All hashes found as potfile and/or empty entries!_ vastauksen...

<img width="1314" height="285" alt="VirtualBox_Kali_22_09_2026_21_10_27" src="https://github.com/user-attachments/assets/4cd3e3ed-37fa-420d-b99c-2b704dd65cff" />

# Lähteet:
Bitwarden, s.a. a, What is password hashing? Luettavissa: https://bitwarden.com/resources/what-is-password-hashing/ Luettu 21.9.2026

Hashcat, s.a. a, Rule-based Attack Luettavissa: https://hashcat.net/wiki/doku.php?id=rule_based_attack Luettu 22.9.2026

Karvinen Tero, 2022, Cracking Passwords with Hashcat, Luettavissa: https://terokarvinen.com/2022/cracking-passwords-with-hashcat/ Luettu 20.9.2026

Karvinen Tero, 2023, Crack File Password With John, Luettavissa: https://terokarvinen.com/2023/crack-file-password-with-john/ Luettu 20.9.2026
