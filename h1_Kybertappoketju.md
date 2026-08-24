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

## Kali asennus
Latasin itselleni Kali-imagen VirtualBox asennusta varten sivulta https://www.kali.org/get-kali/#kali-installer-images. Aluksi ihmettelin eri valintojen välillä, mutta päädyin normaaliin installer valintaan.

## Lähteet:
Herrasmieshakkerit 2025: Tietomurron anatomia, vieraana Antti Kurittu. Kuunneltavissa: https://herrasmieshakkerit.fi/ Kuunneltu 23.8.2026

Hutchins et al 2011: Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains, luku 3.2 Intrusion Kill Chain. Luettavissa: https://lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/LM-White-Paper-Intel-Driven-Defense.pdf Luettu 24.8.2026

Santos et al: The Art of Hacking (Video Collection): 4.3 Surveying Essential Tools for Active Reconnaissance. Katsottavissa: https://learning.oreilly.com/videos/the-art-of/9780135767849/9780135767849-SPTT_04_00/ Katsottu 24.8.2026.
