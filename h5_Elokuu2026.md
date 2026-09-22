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
## c) Asenna John the Ripper ja testaa sen toiminta murtamalla jonkin esimerkkitiedoston salasana.
## e) Tiedosto. Tee itse tai etsi verkosta jokin salakirjoitettu tiedosto, jonka saat auki. Murra sen salaus. (Jokin muu formaatti kuin aiemmissa alakohdissa kokeilemasi).
## f) Tiiviste. Tee itse tai etsi verkosta salasanan tiiviste, jonka saat auki. Murra sen salaus. (Jokin muu formaatti kuin aiemmissa alakohdissa kokeilemasi. Voit esim. tehdä käyttäjän Linuxiin ja murtaa sen salasanan.)
## g) Sanakirja. Oman sanakirjan teko parantaa onnistumismahdollisuuksia. Demonstroi, kuinka teet oman sanakirjan hashcat:n tai john:iin.
## h) Hash rules. Näytä esimerkki HashCatin sääntöjen käytöstä (rules).
# Lähteet:
Karvinen Tero, 2022, Cracking Passwords with Hashcat, Luettavissa: https://terokarvinen.com/2022/cracking-passwords-with-hashcat/ Luettu 20.9.2026

Karvinen Tero, 2023, Crack File Password With John, Luettavissa: https://terokarvinen.com/2023/crack-file-password-with-john/ Luettu 20.9.2026

Bitwarden, s.a. a, What is password hashing? Luettavissa: https://bitwarden.com/resources/what-is-password-hashing/ Luettu 21.9.2026
