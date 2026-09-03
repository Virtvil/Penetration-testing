# Harjoitus 2: DORA the Explora
## x) Materiaalit:
DORA: Digital Operations Resilience Act
- Sisältää vaatimuksia häiriönsietokyvyn testaukselle (digitaalisen toiminnan häiriönsietokyvyn perustason testaus ja uhkiin perustuva tunkeutumistestaus)
- Auttaa yrityksia luomaan omia penetraatiotestejä
- Sisältämät roolit koostuvat ohjaustiimistä, ohjaustiimin vetäjästä, palveluntarjoajasta (uhkatietopalvelun tarjoaja ja Red Team -testaajat), sekä Blue Teamistä (työntekijöitä jotka puolustavat yhteisön tieto- ja viestintätekniikkaa).

DORA regulaatio
- ETLPT-menetelmään perustuvaa vaativaa testausta on suoritettava vähintään kolmen vuoden välein. Joissain tapauksissa tätä tiheyttä voidaan käskeä korottamaan.
- Testaajien on toimitettava viranomaisille yhteenveto havainnoinneista, sekä tutkimuksen vaatimusten mukaisesta suorittamisesta.
- Rahoituslaitosten on käytettävä TLPT-testauksen suorittamisessa testaajia, joita koskee erittäin laajat vaatimukset tiedon turvallisuuden vuoksi.

Red team testing
- Red teaming vaiheessa RTT suunnittelee ja toteuttaa TIBER-testin kohdejärjestelmille ja palveluille valittujen skenaarioiden pohjalta.
- Red-teaming-vaihe koostuu kahdesta eri vaiheesta:
  1. Red Team -testaussuunnitelman (RTTP) laatimisesta
  2. Aktiivisesta testaamisesta.
- Prosessi on suunniteltu luomaan mahdollisimman realistisia skenaarioita, jotka jäljittelevät mahdollisia oikeita hyökkäyksiä organisaatiota vastaan.

## a) Metasploitable asennus
Aloitin etsimällä verkosta latauslinkkiä Metasploitable 2:lle, päätyen Rapid 7 Docs sivustolle. Sivusto sisälsi ohjeet Metasploitablen käyttöön, sekä linkin (https://www.rapid7.com/products/metasploit/metasploitable/) tämän lataamiseen virtuaalikoneelle.

Ladattuani tämän ryhdyin luomaan itselleni uutta virtuaalikonetta VirtualBoxissa.

New Machine > Hard Disk > Use an existing Virtual Hard Disk File > Metasploitable.vmdk

<img width="990" height="686" alt="Näyttökuva 2026-08-31 191855" src="https://github.com/user-attachments/assets/263d5a5d-3637-4301-b938-061c6f45c8f5" />

<img width="988" height="682" alt="Näyttökuva 2026-08-31 192017" src="https://github.com/user-attachments/assets/73c664fa-bbe4-485d-a2da-f0e552b6a1b7" />

## b) Virtuaaliverkko
Saatuani Metasploitablen asennettua ryhdyin luomaan yhteyttä tämän ja aikaisemmin luomani Kali-virtuaalikoneen välille. En tiennyt kuinka tämän tehdään, joten turvauduin VirtualBoxin manuaaliin ja kappaleeseen 6, Virtual Networking.

Käyttäessä Host-Only Network on host-kone yhteydessä virtuaalikoneisiin, jolloin ne pystyvät olemaan yhteyksissä toisiin virtuaalikoneisiin, sekä host-koneeseen. Manuaalin selittää kohdassa 6.7. Host-Only Networking seuraavalla tavalla miten Host-Only Network otetaan käyttöön:

- Avataa virtuaalikoneen asetukset ja täältä _Network_.
- Valitse _Adapter_ ja tarkista että _Enable Network Adapter_ on päällä.
- Vaiha _NAT_:in tilalle _Attached to: Host-Only Adapter_.

Seuraavaksi vaihdoin haluamalleni host-koneelle (eli Kali) toiseksi verkkoadapteriksi _Host-Only_, jotta tämä saa yhdistettyä itsenä Metasploitable-koneeseen.

<img width="970" height="636" alt="Näyttökuva 2026-08-31 193035" src="https://github.com/user-attachments/assets/78860b6b-5014-49ba-94d2-c49eb8668be3" />

Asetusten sijainti.

<img width="968" height="638" alt="Näyttökuva 2026-08-31 193213" src="https://github.com/user-attachments/assets/82ce7867-0753-4128-9bd2-4bb48c98aa81" />

Molemmat koneista omaavat nyt _host-only_ adapterin. Kali:ssa tämä on adapteri 2, kun taas Metasploitable-koneessa tämä on ainoa adapteri (1). 

## c) Virtuaaliverkon tutkiminen 

Seuraavaksi minun piti varmistaa, että koneet näkevät toisensa.

<img width="630" height="341" alt="VirtualBox_Kali_31_08_2026_19_40_29" src="https://github.com/user-attachments/assets/7b7e6beb-7e24-44e9-ada3-8c1c9aada84b" />

Yhteyden voi katkaista tai muodostaa Kalin verkkokuvakkeen kautta, jonka onkin jo tuttu aiemmasta tehtävästä ja VPN-yhteyksien muodostamisesta. Tehtävää varten katkaisin seuraavaksi Kali-koneen NAT-adapterin sulkeakseni tämän pois verkosta, etteivät haluamattomat tahot (kuten lainsäädäntö) pääsisi näkemään mitä laittomuuksia koneiden välillä puuhaillaan.

Yhdistin koneet toisiinsa, mutta varmistaakseni näiden välisen yhteyden ryhdyin pingaamaan niitä. Tätä varten tarvitsemmekin ensin molempien koneiden ip osoittet, jotka hain komennolla _ifconfig_.


<img width="640" height="383" alt="VirtualBox_Kali_31_08_2026_19_54_31" src="https://github.com/user-attachments/assets/95afe2f0-6ee4-4263-9196-2e47e4df7adc" />

Kalin ip-osoite

<img width="720" height="400" alt="VirtualBox_Metasploitable 2_31_08_2026_19_47_14" src="https://github.com/user-attachments/assets/75ff97a3-7a88-4a13-9d85-02badb211bca" />

Metasploitable ip-osoite

Seuraavaksi varmistin koneiden olevan irti verkosta, simppelillä _ping 8.8.8.8._ komennolla.

<img width="640" height="134" alt="VirtualBox_Kali_31_08_2026_19_54_31_2" src="https://github.com/user-attachments/assets/d575eb8a-8efd-4980-85e5-18f1443e8fb3" />

Verkkoyhteys ei onnistu, olemme piilossa!

Tämän jälkeen testasin koneiden välistä yhteyttä, pingaamalla Kalilla Metasploitable. Tähän käytin komentoa _ping 192.168.56.104 -c 4_. Komennon osa _-c 4_ rajaa pingien määrän neljään.

<img width="650" height="245" alt="VirtualBox_Kali_31_08_2026_20_02_30" src="https://github.com/user-attachments/assets/73f14316-ad04-4b3c-baf4-bc4d7bbd3c82" />

Onnistunut pingaus Kalilta.

Seuraavaksi siirryin Metasploitablelle, jossa pingasin _8.8.8.8_, sekä Kalia.

<img width="657" height="238" alt="VirtualBox_Metasploitable 2_31_08_2026_20_06_51" src="https://github.com/user-attachments/assets/497bf05c-863e-4649-ba19-26998444cb38" />

Halutut toimivat pingit.

## d) Etsi Metasploitable

Etsin seuraavaksi porttiskannerilla Metasploitablen, käyttämällä komentoa _nmap -sn 192.168.56.104_.

<img width="629" height="180" alt="VirtualBox_Kali_31_08_2026_20_50_00" src="https://github.com/user-attachments/assets/5db716dd-c5bc-470a-b954-23525dbf1675" />

Löytyy!

Seuraavaksi tarkistin selaimella, että löysin oikean IP:n, tässä tapauksessa Metasploitablen weppipalvelimen ja tämän etusivun:

<img width="601" height="500" alt="VirtualBox_Kali_31_08_2026_20_51_30" src="https://github.com/user-attachments/assets/10cf1438-d839-428f-9305-b8f45835b73b" />

Löytyyhän se!

## e) Metasploitable porttiskannaus

Aloitin porttiskannauksen komennolla nmap -A -T4 -p- 192.168.56.104. Pitkän skannauksen jäälkeen sain tietooni seuraavat avoimet portit:

<img width="955" height="910" alt="VirtualBox_Kali_31_08_2026_21_01_34" src="https://github.com/user-attachments/assets/13e60fc3-cee3-46c0-b181-b3d503343f46" />

<img width="955" height="910" alt="VirtualBox_Kali_31_08_2026_21_01_55" src="https://github.com/user-attachments/assets/2f7d9ce5-c311-45e5-ad4c-1815a9ef15e0" />

<img width="955" height="640" alt="VirtualBox_Kali_31_08_2026_21_02_15" src="https://github.com/user-attachments/assets/0a3c8b44-b911-4381-b4e9-b9c3eb972e48" />

Itselleni tuttuja ja kiinnostavia avoimia portteja ovet:

- 22: Ssh, ssh palvelin jolla koneeseen saa etäyhteyden.
- 23: Telnet, Hack the Boxin kautta tutuksi tullut salaamaton ja haavoittuvainen etähallinta.
- 80: http, verkkopalvelimen käyttämä. Usein myös hyökkäysten kohteena.
- 1099: java-rmi. Javan poistuessa käytössä on systeemi haavoittuvainen. HUOM ensimmäinen tulos googlatessa on "java-rmi exploit". PentestPad kuvaa java-rmi:tä nimipalveluna, jota Java-sovellus käyttää olioiden etsimiseen ja niiden metodien kutsumiseen verkon yli. 

<img width="417" height="128" alt="Näyttökuva 2026-08-31 210756" src="https://github.com/user-attachments/assets/f9c89949-39f3-42ca-bf34-6765d374aa73" />


## Lähteet:
Buuri 2026: DORA and TLPT testing - Lecture for Haaga-Helia on 31 March 2026. Luettavissa: https://terokarvinen.com/buuri-2026-dora-and-threat-lead-penetration-testing/buuri-2026-dora-and-threat-lead-penetration-testing--teros-pentest-course.pdf Luettu 27.8.2026

Eur-Lex DORA (Regulation ... on digital operational resilience for the financial sector) 2022. Luettavissa: https://eur-lex.europa.eu/eli/reg/2022/2554/oj/eng Luettu 28.8.2026

PentestPad Port 1099 – Java RMI (Remote Method Invocation) Luettavissa: https://www.pentestpad.com/port-exploit/port-1099-java-rmi-remote-method-invocation Luettu 31.8.2026

Rapid 7 Docs, Metasploitable 2. Luettavissa: https://docs.rapid7.com/metasploit/metasploitable-2/ Luettu 31.8.2026

TIBER-FI procedures and guidelines, 5.4 Testing phase: Red team testing 2025. Luettavissa: https://www.suomenpankki.fi/globalassets/bof/en/money-and-payments/the-bank-of-finland-as-catalyst-payments-council/tiber-fi/tiber-fi-2.0-procedures-and-guidelines.pdf Luettu 29.8.2026

VirtualBox Chapter 6. Virtual Networking. Luettavissa: https://www.virtualbox.org/manual/ch06.html Luettu 31.8.2026.

