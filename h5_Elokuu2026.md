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


## e) Tiedosto. Tee itse tai etsi verkosta jokin salakirjoitettu tiedosto, jonka saat auki. Murra sen salaus. (Jokin muu formaatti kuin aiemmissa alakohdissa kokeilemasi).
## f) Tiiviste. Tee itse tai etsi verkosta salasanan tiiviste, jonka saat auki. Murra sen salaus. (Jokin muu formaatti kuin aiemmissa alakohdissa kokeilemasi. Voit esim. tehdä käyttäjän Linuxiin ja murtaa sen salasanan.)
## g) Sanakirja. Oman sanakirjan teko parantaa onnistumismahdollisuuksia. Demonstroi, kuinka teet oman sanakirjan hashcat:n tai john:iin.
## h) Hash rules. Näytä esimerkki HashCatin sääntöjen käytöstä (rules).
# Lähteet:
Karvinen Tero, 2022, Cracking Passwords with Hashcat, Luettavissa: https://terokarvinen.com/2022/cracking-passwords-with-hashcat/ Luettu 20.9.2026

Karvinen Tero, 2023, Crack File Password With John, Luettavissa: https://terokarvinen.com/2023/crack-file-password-with-john/ Luettu 20.9.2026

Bitwarden, s.a. a, What is password hashing? Luettavissa: https://bitwarden.com/resources/what-is-password-hashing/ Luettu 21.9.2026
