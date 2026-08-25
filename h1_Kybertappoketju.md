# Harjoitus 1: Kybertappoketju 

## Materiaalit
Herrasmieshakkerit, Tietomurron anatomia:
- Vähän turhan paljon mainontaa ja sponsorien etsintää jakson alkuun.
- Mielenkiintoista keskustelua maksukorteista, maksukorttien turvakoodeista ja siitä kuinka sivustot päättävät itse kuinka arkaa tietoa tallentaa.
- MIE (ei savoa, vaan Memory Integrity Enforcement), Applen uusien puhelimien suoja puhelimen muistin ylivuodolle ja tämän kautta muistiin käsiksi pääsemiselle.
- Paljon keskustelua Vastaamon tietomurrosta, sekä tietomurtojen havaitsemisesta yrityksen sisällä (sekä kuinka havaitsemisen jälkeen edetään).
- Erittäin mielenkiintoinen podcast, pidin varsinkin Antti Kurittun uratarinoista.

Tappoketju:
- Järjestelmällinen prosessi, jonka avulla haluttuun kohteeseen vaikutetaan haluttujen tavoitteiden aikaansaamiseksi.
- Vaiheet:
  1. Tiedustelu
  2. Aseistaminen
  3. Toimitus
  4. Hyväksikäyttö
  5. Asennus
  6. Komentaminen ja kontrollointi (Command and Control (C2))
  7. Tavoitteisiin liittyvät toimenpiteet

The Art of Hacking:
Passiivnen tiedustelu:
- Ei näy logeissa.
- Kohdeympäristöön ei lähetetä ollenkaan paketteja.
   
Aktiivinen tiedustelu:
- Ensimmäinen osa tappoketjua.
- Näkyy logeissa.
- Kohdeverkkoa käsitellään aktiivisesti, esimerkiksi porttiskannauksen muodossa.
- Hyödyllisiä ohjelmia:
    - NMAP (Yleisin porttsikannausohjelma)
    - Masscan (useille porteille)
 
Korkeimman oikeuden päätös
- Henkilö A porttiskannannut Osuuspankkikeskusta porttiskannerilla ja tuomittu ensiksi sakkoon, mutta myöhemmin valituksen myötä joutunut maksamaan pankille ja yhtiölle yhteensä 75 000 markkaa (noin 12 600e).
- Päätös tuntuu hieman kummalliselta, sillä pelkästä skannauksesta ei mielestäni aiheutuisi pankille/yhtiölle näin suurta rahallista vahinkoa.

## Kali asennus
Latasin itselleni Kali-imagen VirtualBox asennusta varten sivulta https://www.kali.org/get-kali/#kali-installer-images. Aluksi ihmettelin eri valintojen välillä, mutta päädyin normaaliin installer valintaan.

Asennuksen aikana muutin virtuaalikonetta antamalla tälle enemmän muistia (4 GB) ja enemmän CPU voimaa (2 cpu). Asennuksessa käytin kalin sivuilta saatavaa _"kali-linux-2026.2-installer-amd64"_ iso-tiedostoa. Asennus suijuikin ilman kummempia vaivoja, vaikka veikin normaalia Debian-versiota enemmän aikaa. Tämän jälkeen varmistin kaikkien ohjelmieni olevan päivitettynä komennoilla _"sudo apt-get update"_ ja _"sudo apt-get upgrade"_

## Box the hack
Ryhdyin seuraavaksi irroittamaan virtuaalikonettani verkosta. Aluksi luin ja tallensin Hack The Box-sivuston säännöt itselleni. Tämän jälkeen sivuston oikealta yläreunalta valitsin _Connect>Starting Point>OpenVPN>Download VPN_.

<img width="1920" height="767" alt="VirtualBox_Kali_25_08_2026_21_19_23" src="https://github.com/user-attachments/assets/61bddb82-76bb-4799-b633-0dee605922ff" />

<img width="578" height="758" alt="VirtualBox_Kali_25_08_2026_21_19_52" src="https://github.com/user-attachments/assets/50af8826-0fd8-4e46-8e0a-f49b3ef23c00" />

<img width="435" height="772" alt="VirtualBox_Kali_25_08_2026_21_20_15" src="https://github.com/user-attachments/assets/2da1b3cb-6c30-4338-9102-0a922a99ab29" />

Ladattuani VPN koneelleni, ryhdyin ottamaan sitä käyttööni ruudun oikeasta yläreunasta, josta Ethernet porttia klikkaamalla valitsin _VPN Connections>Add a VPN connection...>Import a saved VPN configuration_. Tämän avulla pystyinkin valitsemaan juuri lataamani VPN tiedoston.

<img width="565" height="379" alt="VirtualBox_Kali_25_08_2026_21_20_55" src="https://github.com/user-attachments/assets/15060c8e-db79-449f-91f2-c77283c6876f" />

<img width="698" height="598" alt="VirtualBox_Kali_25_08_2026_21_30_19" src="https://github.com/user-attachments/assets/37a1e136-ebc5-40bc-bfc2-ce51d976fcbc" />

<img width="527" height="619" alt="VirtualBox_Kali_25_08_2026_21_25_40" src="https://github.com/user-attachments/assets/2f6213ac-5317-4a6b-bcc6-d5a37370f2aa" />

Tämän jälkeen varmistin VPN yhteyden toimivuuden pingaamalla osoitetta 8.8.8.8. Toimivuus varmistui sillä ping-pyynnöt eivät menneet läpi, eikä kokeillessani verkkokoneen selaimella googlen sivut toimineet.

<img width="601" height="227" alt="VirtualBox_Kali_25_08_2026_21_55_05" src="https://github.com/user-attachments/assets/1f99f0f7-51d8-4c34-a360-970e53dae45c" />

<img width="657" height="540" alt="VirtualBox_Kali_25_08_2026_21_54_54" src="https://github.com/user-attachments/assets/3833cf67-98f5-494c-972e-05e8a42ad32c" />

Varmistettuani kaiken toimivan halutulla tavalla lähdin skannaamaan koneeni verkkoportteja komennolla _nmap -T4 -A localhost_. 
Komennon osat toimivat jotakuinkin näin:
Nmap: haluttu toiminto, eli network mapping
-T4: Timing Template, jossa numeron kohotessa skannauksen nopeus kasvaa aggressiivisemmaksi (1-5).
-A: käyttöjärjestelmän tunnistus, version tunnistus, skriptiskannaus ja traceroute
localhost: oma laitteeni!

<img width="649" height="514" alt="VirtualBox_Kali_25_08_2026_21_56_09" src="https://github.com/user-attachments/assets/10c39559-c188-4ca0-b025-268b9e6ec656" />

Aluksi näistä ei ollut yksikään auki.

Seuraavaksi poistuin skannauksesta ja suljin VPN-yhteyden, jonka jälkeen asensin itselleni pari demonia (ssh ja nginx). Aktivoin molemmat uusista demoneista ja palautin VPN-yhteyden päälle. Yhteyden palauduttua skannasin porttini uudelleen ja huomasinkin kahden portin (22 ja 80) tulleen käyttöön!

<img width="647" height="529" alt="VirtualBox_Kali_25_08_2026_22_02_31" src="https://github.com/user-attachments/assets/41916f9d-1b60-4c02-85c9-3f2c57e5eba9" />

## Orion
Lähdin ratkaisemaan Hack The Boxin tarjoamia "helppoja" koneita. En kuitenkaan tässä vaiheessa osannut oikeastaan mitään muuta kuin skannata tämän toisen koneen joten lähdinkin hakemaan itselleni verkosta apua! Sivuston virallinen writeup oli mielestäni sekava ja hyppäsi erittäin syvään päätyyn, käyttäen ohjelmia joista en ollut edes kuullut, joten lähdinkin itse tutkimaan mahdollisia muita hyödyllisiä lähteitä. Tällöin törmäsinkin Brandistone Nyabonyi Mabeyan erittäin hyödylliseen writeuppiin jota seuraten sainkin tehtävän suoritettua onnistuneesti!

Tehtävän ideana oli murtautua "Orion"-palvelua pyörittävälle koneelle ja napata tämän admin-käyttäjältä (Adam) lippu, sekä telnet-sovelluksen kautta laitteen root-kansiosta toinen lippu.

<img width="1526" height="201" alt="Näyttökuva 2026-08-25 233219" src="https://github.com/user-attachments/assets/e881f0a0-4811-4163-a4b6-12bbc4cba396" />



## Lähteet:
Brandistone Nyabonyi Mabeya Orion HTB Luettavissa: https://medium.com/@brandynyabonyi/orion-htb-42ad8ad1c374 Luettu 25.8.2026

Herrasmieshakkerit 2025: Tietomurron anatomia, vieraana Antti Kurittu. Kuunneltavissa: https://herrasmieshakkerit.fi/ Kuunneltu 23.8.2026

Hutchins et al 2011: Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains, luku 3.2 Intrusion Kill Chain. Luettavissa: https://lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/LM-White-Paper-Intel-Driven-Defense.pdf Luettu 24.8.2026

KKO 2003:36 Luettavissa: https://www.finlex.fi/fi/oikeuskaytanto/korkein-oikeus/ennakkopaatokset/2003/36#OT0_OT1 Luettu 25.8.2026

Santos et al: The Art of Hacking (Video Collection): 4.3 Surveying Essential Tools for Active Reconnaissance. Katsottavissa: https://learning.oreilly.com/videos/the-art-of/9780135767849/9780135767849-SPTT_04_00/ Katsottu 24.8.2026.
