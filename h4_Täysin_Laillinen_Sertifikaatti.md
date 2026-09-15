# Harjoitus 4: Täysin Laillinen Sertifikaatti
## x) Materiaalit
### A01:2021 – Broken Access Control 
- Pääsynvalvonta varmistaa käytäntöjen noudattamisen niin etteivät käyttäjät voi toimia sallittujen oikeuksien ulkopuolella.
- Häiriötilanteet johtavat yleisesti tiedon luvattomaan paljastumiseen, muuttamiseen tai tuhoutumiseen.
### PortSwigger Academy: Insecure direct object references (IDOR)
- Insecure direct object references (Turvattomat suorat objektiviittaukset (IDOR)) ovat pääsynvalvontaan liittyvä haavoittuvuus. Tilanne syntyy, kun sovellus käyttää käyttäjän antamaa syötettä objektien suoraan käsittelyyn.
- Hyökkääjä saattaa päästä käsiksi esimerkiksi muitten asiakkaitten tietoihin simppelillä URL-osoitteen muutoksella.
- Hyökkääjä saattaa pystyä toteuttamaan sekä horisontaalisen että vertikaalisen oikeuksien laajentamisen muuttamalla käyttäjätiedot sellaisiksi, jotka omaavat suurempia oikeuksia, kiertämällä samalla pääsynvalvonnan.
- Muita mahdollisia hyökkäyksiä ovat esimerkiksi vuotaneiden salasanojen hyödyntäminen tai parametrien muokkaaminen sen jälkeen, kun hyökkääjä on päässyt käyttäjän tilitiedoille.
### PortSwigger Academy: Path traversal
- Path traversal tunnetaan myös nimellä hakemiston läpikäynti (directory traversal). Nämä haavoittuvuudet mahdollistavat sen, että hyökkääjä voi lukea mielivaltaisia ​​tiedostoja palvelimelta, jossa sovellusta suoritetaan.
- Tiedostojen polkujen kautta tehtävä hyökkäys, jossa käytetään hyväksi polkujen oikeuksia lisäämällä polkujen osoitteisiin ```../```-ketjua. Tiedostopolku voi hyväksyä ketjun jolloin se sallii siirtymisen yhden tason ylöspäin hakemistopuussa.
### PortSwigger Academy: Cross-site scripting
- Mahdollistaa hyökkääjälle saman alkuperän käytännön (same-origin policy) kiertämisen. Käytäntö on suunniteltu eristämään eri verkkosivustot toisistaan.
- Sivustojen välisten komentosarja-ajojen (XSS) haavoittuvuudet mahdollistavat yleensä sen, että hyökkääjä voi esiintyä uhrina, suorittaa mitä tahansa toimintoja, joihin käyttäjällä on oikeudet, ja päästä käsiksi käyttäjän tietoihin.
- Jos uhrilla on sovelluksessa korkeat käyttöoikeudet, hyökkääjä saattaa pystyä saamaan täyden hallinnan sovelluksen kaikista toiminnoista ja tiedoista.
- Cross-site scripting toimii muokkaamalla haavoittuvaa verkkosivustoa siten, että se palauttaa käyttäjille haitallista JavaScript-koodia. Kun haitallinen koodi suoritetaan uhrin selaimessa, hyökkääjä voi ottaa täyden hallinnan uhrin ja sovelluksen välisestä vuorovaikutuksesta.
## a) Totally Legit Sertificate. 
Seurasin Zaproxyn asentamisessa Kali-sivuston omia neuvoja asennukseen (linkki lähteissä).

Aloitin muuttamalla Kali-koneeni aiemmista tehtävistä suljetusta verkoista avoimeen, jotta pystyisin lataaman itselleni Zaproxyn käyttämällä komentoja:

```
sudo apt update
sudo apt install zaproxy
```
<img width="955" height="605" alt="VirtualBox_Kali_15_09_2026_20_38_08" src="https://github.com/user-attachments/assets/314f66af-0297-4127-904c-5bdb827ef412" />

Tämän jälkeen pystin käynnistämään ZAProxyn simppelillä ```zaproxy``` komennolla.

<img width="955" height="690" alt="VirtualBox_Kali_15_09_2026_20_46_31" src="https://github.com/user-attachments/assets/63b39eaa-7f60-47fc-9e4b-306dce93f44e" />

Tämän myötä avautuikun Zaproxylle oma ikkuna, jossa kysyttiin haluanko tallentaa tämänhetkisen istuntoni, johon valitsin _"Yes, I want to persist this session with name based on the current timestamp"_. Seuraavaksi aloin luomaan itselleni sertifikaattia, navigoimalla yläpalkissa kohteeseen ```Tools -> Options -> Network -> Server Certificates```. Tallensin pyynnöstäni autoomaattisesti luodun sertifikaatin uuteen _harjoitus4_-kansioon.

<img width="793" height="660" alt="VirtualBox_Kali_15_09_2026_20_53_17" src="https://github.com/user-attachments/assets/b2514e54-6ebf-48bd-882c-49bcd150e6df" />

Siirsin sertifikaatin kali-koneeni firefoxiin menemällä ```Settings -> Certificates -> View Certificates -> Import```.

<img width="955" height="384" alt="VirtualBox_Kali_15_09_2026_20_59_29" src="https://github.com/user-attachments/assets/e093218a-e1ad-4e1a-9fbc-7fc8afc0c535" />

<img width="649" height="468" alt="VirtualBox_Kali_15_09_2026_20_59_52" src="https://github.com/user-attachments/assets/cc3e8966-6d10-4461-9089-eb1befeff374" />

<img width="955" height="380" alt="VirtualBox_Kali_15_09_2026_21_00_47" src="https://github.com/user-attachments/assets/0d7313ef-0ddb-4adb-a147-0609fa116878" />

<img width="787" height="298" alt="VirtualBox_Kali_15_09_2026_21_01_06" src="https://github.com/user-attachments/assets/653f201a-d5ce-4101-bbc5-ca998f5a1fef" />

Varmistin vielä että Zaproxy tallentaa kuvat suuntaamalla ohjelmaan ja kohteeseen ```Tools -> Options -> Display -> Process Images in HTTP requests/responses``` jossa laitoin täpän ruutuun.

<img width="789" height="600" alt="VirtualBox_Kali_15_09_2026_21_08_00" src="https://github.com/user-attachments/assets/4a874d3e-8265-4c0f-a845-338a41d301fe" />

Lopuksi tarkistin vielä toimivuuden suuntaamalla proxyn _Manual Explorer_ kautta _example.com_-sivustolle.

<img width="955" height="879" alt="VirtualBox_Kali_15_09_2026_21_11_35" src="https://github.com/user-attachments/assets/9009350f-290f-4c49-81cc-17e07ddcb004" />


## b) Kettumaista. 
Asenna "FoxyProxy Standard" Firefox Addon, ja lisää ZAP proxyksi siihen. Käytä FoxyProxyn "Patterns" -toimintoa, niin että vain valitsemasi weppisivut ohjataan Proxyyn. (Läksyssä ohjataan varmaankin PortSwigger Labs ja localhost.)

# PortSwigger Labs. 
Ratkaise tehtävät. Selitä ratkaisusi: mitä palvelimella tapahtuu, mitä eri osat tekevät, miten hyökkäys löytyi, mistä vika johtuu. Kannattaa käyttää ZAPia, vaikka malliratkaisut käyttävät harjoitusten tekijän maksullista ohjelmaa. Monet tehtävät voi ratkaista myös pelkällä selaimella. Malliratkaisun kopioiminen ZAP:n tai selaimeen ei ole vastaus tehtävään, vaan ratkaisu ja haavoittuvuuden etsiminen on selitettävä ja perusteltava.

## Cross Site Scripting (XSS)
### c) Reflected XSS into HTML context with nothing encoded

### d) Stored XSS into HTML context with nothing encoded

### e) Selitä esimerkin avulla, mitä hyökkääjä hyötyy XSS-hyökkäyksestä. 
Alert("Hei Tero!") ei vielä tarjoa kummoista pääsyä. (Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella, pelkkä lyhyt ja selkeä selitys riittää.)

## Path traversal
### f) File path traversal, simple case. Laita tarvittaessa Zapissa kuvien sieppaus päälle.

### g) File path traversal, traversal sequences blocked with absolute path bypass

### h) File path traversal, traversal sequences stripped non-recursively
## Insecure Direct Object Reference (IDOR)
### i) Insecure direct object references

# Lähteet:
Kali - Zaproxy Tool Documentation Luettavissa: https://www.kali.org/tools/zaproxy/ Luettu 15.9.2026

OWASP 2021: OWASP Top 10:2021 - Broken Access Control. Luettavissa: https://top10.owasp.org/2021/A01_2021-Broken_Access_Control/ Luettu 13.9.2026

PortSwigger Academy - Insecure direct object references (IDOR). Luettavissa: https://portswigger.net/web-security/access-control/idor Luettu 14.9.2026

PortSwigger Academy - Path traversal. Luettavissa: https://portswigger.net/web-security/file-path-traversal Luettu 14.9.2026

PortSwigger Academy - Cross-site scripting. Luettavissa: https://portswigger.net/web-security/cross-site-scripting Luettu 14.9.2026

Karvinen Tero 2026. Täysin Laillinen Sertifikaatti. Luettavissa: https://terokarvinen.com/tunkeutumistestaus/ Luettu 13.9.2026
