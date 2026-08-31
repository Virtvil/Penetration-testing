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
ALoitin etsimällä verkosta latauslinkkiä Metasploitable 2:lle, päätyen Rapid 7 Docs sivustolle. Sivusto sisälsi ohjeet Metasploitablen käyttöön, sekä linkin (https://www.rapid7.com/products/metasploit/metasploitable/) tämän lataamiseen virtuaalikoneelle.

Ladattuani tämän ryhdyin luomaan itselleni uutta virtuaalikonetta VirtualBoxissa.

New Machine > Hard Disk > Use an existing Virtual Hard Disk File > Metasploitable.vmdk

<img width="990" height="686" alt="Näyttökuva 2026-08-31 191855" src="https://github.com/user-attachments/assets/263d5a5d-3637-4301-b938-061c6f45c8f5" />

<img width="988" height="682" alt="Näyttökuva 2026-08-31 192017" src="https://github.com/user-attachments/assets/73c664fa-bbe4-485d-a2da-f0e552b6a1b7" />

## b) Virtuaaliverkko
Saatuani Metasploitablen asennettua ryhdyin luomaan yhteyttä tämän ja aikaisemmin luomani Kali-virtuaalikoneen välille. En tiennyt kuinka tämän tehdään, joten turvauduin VirtualBoxin manuaaliin ja kappaleeseen 6, Virtual Networking.

## c) Virtuaaliverkon tutkiminen 

## d) Etsi Metasploitable

## e) Metasploitable porttiskannaus

## Lähteet:
Buuri 2026: DORA and TLPT testing - Lecture for Haaga-Helia on 31 March 2026. Luettavissa: https://terokarvinen.com/buuri-2026-dora-and-threat-lead-penetration-testing/buuri-2026-dora-and-threat-lead-penetration-testing--teros-pentest-course.pdf Luettu 27.8.2026

Eur-Lex DORA (Regulation ... on digital operational resilience for the financial sector) 2022. Luettavissa: https://eur-lex.europa.eu/eli/reg/2022/2554/oj/eng Luettu 28.8.2026

Rapid 7 Docs, Metasploitable 2. Luettavissa: https://docs.rapid7.com/metasploit/metasploitable-2/ Luettu 31.8.2026

TIBER-FI procedures and guidelines, 5.4 Testing phase: Red team testing 2025. Luettavissa: https://www.suomenpankki.fi/globalassets/bof/en/money-and-payments/the-bank-of-finland-as-catalyst-payments-council/tiber-fi/tiber-fi-2.0-procedures-and-guidelines.pdf Luettu 29.8.2026

VirtualBox Chapter 6. Virtual Networking. Luettavissa: https://www.virtualbox.org/manual/ch06.html Luettu 31.8.2026.

