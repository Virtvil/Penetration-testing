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

## a) Asenna Hashcat ja testaa sen toiminta murtamalla esimerkkisalasana.
## c) Asenna John the Ripper ja testaa sen toiminta murtamalla jonkin esimerkkitiedoston salasana.
## e) Tiedosto. Tee itse tai etsi verkosta jokin salakirjoitettu tiedosto, jonka saat auki. Murra sen salaus. (Jokin muu formaatti kuin aiemmissa alakohdissa kokeilemasi).
## f) Tiiviste. Tee itse tai etsi verkosta salasanan tiiviste, jonka saat auki. Murra sen salaus. (Jokin muu formaatti kuin aiemmissa alakohdissa kokeilemasi. Voit esim. tehdä käyttäjän Linuxiin ja murtaa sen salasanan.)
## g) Sanakirja. Oman sanakirjan teko parantaa onnistumismahdollisuuksia. Demonstroi, kuinka teet oman sanakirjan hashcat:n tai john:iin.
## h) Hash rules. Näytä esimerkki HashCatin sääntöjen käytöstä (rules).
# Lähteet:
Karvinen Tero, 2022, Cracking Passwords with Hashcat, Luettavissa: https://terokarvinen.com/2022/cracking-passwords-with-hashcat/ Luettu 20.9.2026

Karvinen Tero, 2023, Crack File Password With John, Luettavissa: https://terokarvinen.com/2023/crack-file-password-with-john/ Luettu 20.9.2026

Bitwarden, s.a. a, What is password hashing? Luettavissa: https://bitwarden.com/resources/what-is-password-hashing/ Luettu 21.9.2026
