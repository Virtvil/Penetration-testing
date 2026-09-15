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
Foxyproxy-lisäri löytyi helposti etsimällä Firefoxin _addons_-osiosta ja asentuu simppelisti _Add_-painiketta painamalla.

<img width="955" height="496" alt="VirtualBox_Kali_15_09_2026_21_19_05" src="https://github.com/user-attachments/assets/576e33d3-ee7a-4247-b3ab-9f5678e4f510" />

Foxy Proxylle oman Zapin asettaminen löytyy siirtymällä asetuksissa _"Proxies"_-osioon, josta proxysta saa tehtyään halutunlaisen. Määrittelin omani seuraavalla tavalla:

```
Title: Zap
Type: HTTP
Country:
City:
Hostname: localhost
Port: 8080
```

Tämän lisäksi _Patterns_-toiminnon avulla pystyin lisäämään PortSwiggerin ja localhostin, jotta proxy käsittelisi vain näiden kautta kulkevaa liikennettä.

```
portswigger labs *web-security-academy.net*
localhost *localhost*
```

Loppujen lopuksi tulokseni näytti tältä:

<img width="955" height="522" alt="VirtualBox_Kali_15_09_2026_22_27_38" src="https://github.com/user-attachments/assets/4b52e5f3-dd78-40e4-832f-d7673743c8da" />

Luodut proxyt saatiin tallennuksen jälkeen käyttöön avaamalla Foxy Proxyn kuvake ja valitsemalle luodut proxyt.

<img width="303" height="381" alt="VirtualBox_Kali_15_09_2026_21_39_03" src="https://github.com/user-attachments/assets/d25013db-86c2-43a9-aee6-807b5a62bc2c" />


# PortSwigger Labs. 

## Cross Site Scripting (XSS)
### c) Reflected XSS into HTML context with nothing encoded
Aloitetaan tekemällä haku sivuston hakukenttään. Tässä tapauksessa halusin kokeilla jotain niinkin simppeliä kuin _"admin"_. Hakua tehtdessä tämä ilmestyykin näkyviin Zaproxyssa! Tiedämme nyt, että hakukenttään syötetyt komennot lähettävät GET-pyynnön suodattamatta tätä.

<img width="286" height="512" alt="VirtualBox_Kali_15_09_2026_22_34_37" src="https://github.com/user-attachments/assets/844a6dce-33d1-4864-9b36-73b54d7d98a8" />

<img width="955" height="438" alt="VirtualBox_Kali_15_09_2026_22_33_30" src="https://github.com/user-attachments/assets/85a8f6be-a53b-4907-ab19-51531df8ed42" />

Olisin ehdottomasti voinut valita helpommin löydettävän lauseen kuin admin...

Seuraavaksi syötin hakukenttään hirvittävän skriptin:

```<script>alert("TERO OIS YLPEE")</script>```

<img width="955" height="474" alt="VirtualBox_Kali_15_09_2026_22_13_09" src="https://github.com/user-attachments/assets/914bfb6e-8a4c-4a2e-aa72-67d46f9eefb0" />

Onnistunut tulos!

Haavoittuvuus tehtävän tilanteessa mahdollistaa haitallisen koodin syöttämisen ja ulospäin tulostuvan tiedon näyttämisen!
### d) Stored XSS into HTML context with nothing encoded
Tehtävän ideana on hyödyntää haavoittuvuutta jossa haitallinen tieto tallennetaan palvelimelle jolloin se on saatavilla kaikille käyttäjille.

Aloitin jättämällä sivustolle kommentin, joka pyysi tarkkaa formaattia (tutkin aluksi tästä annettavaa viestiä, mutta en löytänyt mitään ihmeellisempiä lähetettyjä pyyntöjä). Korjasin formaatin _www._-muotoon jolloin pyyntöni meni läpi ja Zaproxyyn ilmestyi uusi ```post -> comment -> GET:confrimation``` ja ```POST:comment``` tuloste! 

<img width="955" height="835" alt="VirtualBox_Kali_15_09_2026_22_48_23" src="https://github.com/user-attachments/assets/d4784197-54bd-45e0-934e-0671e53ae563" />

<img width="234" height="354" alt="VirtualBox_Kali_15_09_2026_22_54_31" src="https://github.com/user-attachments/assets/b7554e04-fc8b-467b-9066-1aa5f8833087" />

Palasinkin siis blogiin aikeenani syöttää MYRKYTETTY KOMMENTTI!

```<script>alert("SAFKIS BE UPON YE")</script>```

<img width="793" height="701" alt="VirtualBox_Kali_15_09_2026_22_58_07" src="https://github.com/user-attachments/assets/663f2d2b-92e3-46c4-9614-3be6dc9f6614" />

<img width="955" height="747" alt="VirtualBox_Kali_15_09_2026_22_58_57" src="https://github.com/user-attachments/assets/5ac58194-0ef4-4ce8-af5f-291d496a1a70" />

Verkkosivun ja sähköpostin pyytämät syötekentät pyysivät tietyssä formaatissa tietoja, mutta komenttikenttä ei! Tällöin pystyin syöttämään oman skriptini kommenttikentän kautta, jolloin se myös tallentui sivulle, näkyen myös muille sivuston käyttäjille.

### e) Selitä esimerkin avulla, mitä hyökkääjä hyötyy XSS-hyökkäyksestä. 
XSS-hyökkäyksessä hyökkääjä pystyy syöttämään haitallista koodia luotettavalle verkkosivustolle, jolloin koodi suoritetaan uhrin selaimessa. Hyökkääjä ei yleensä vaaranna itse palvelinta, vaan kaappaa uhrin selainistunnon ja oikeudet.

Mahdollisia hyötyjä hyökkääjälle:
- Istunnon kaappaus
- Evästeiden varastaminen: Hyökkääjä voi lukea käyttäjän istuntoevästeet ja kirjautua palveluun uhrin nimissä ilman salasanaa.
- Phishing: Hyökkääjä voi muokata sivun sisältöä ja näyttää väärennetyn kirjautumislomakkeen, jolla uhrin tiedot saadaan hyökkääjän haltuun.
- Käyttäjän oikeuksilla toimiminen
- Sivuston ja laitteiden saastuttaminen: Hyökkääjä voi ohjata käyttäjän sivustolle, joka lataa uhrin laitteelle haittaohjelmia.

## Path traversal
### f) File path traversal, simple case. Laita tarvittaessa Zapissa kuvien sieppaus päälle.
Aloitin nappaamalla ensimmäisen tarjotun tuotteen verkkokaupasta. Menin tuotteen omalle sivulle ja aloin tutkimaan mitä tietoja Zaproxy minulle tästä tarjoaa.

<img width="955" height="835" alt="VirtualBox_Kali_15_09_2026_23_11_07" src="https://github.com/user-attachments/assets/47456811-f019-47ab-96f3-c59f4f4e0c3e" />

Ahaa! Sivusto näyttää tarkan polun mistä kuva on saatavilla! _Materiaali_-osiossa keskustelimmekin path traversalista, sekä ```../```-ketjun käyttämisestä! Kokeillaanpas päästä tämän avulla käsiksi _passwd_-kansioon...

<img width="955" height="722" alt="VirtualBox_Kali_15_09_2026_23_12_00" src="https://github.com/user-attachments/assets/2caad9a2-4f3f-4132-a87e-cb4f4c56f1b8" />

Hmmm, ymmärrettävästi meille ei tarjota kuvaa, mutta pystymme tarkastelemaan varmasti Zaproxyn avulla kyseisen hakemiston sisältöjä?

<img width="955" height="317" alt="VirtualBox_Kali_15_09_2026_23_13_13" src="https://github.com/user-attachments/assets/e1816bde-25c7-4450-b55e-de6049f3a7d0" />

Hakemalla Zaproxyn kautta kuvan tiedot pystyin muuttamaan näytettäviä tietoja ja sainkin tietooni kaiken passwd kansion sisällön!

<img width="887" height="764" alt="VirtualBox_Kali_15_09_2026_23_15_09" src="https://github.com/user-attachments/assets/c767e715-7c31-4f40-a67c-a704e707d0ba" />

### g) File path traversal, traversal sequences blocked with absolute path bypass

Tämä tehtävä toimi samalla tapaa kuin edellinen, paitsi käyttämämme ```../```-ketjutus on estetty. Tämän sijaan tiedosto löytyykin (omasta mielestäni huomattavasti helpommalla) tavalla: 

```https://0a810020035a87ef81624d1900270057.web-security-academy.net/image?filename=/etc/passwd```

<img width="955" height="460" alt="VirtualBox_Kali_15_09_2026_23_26_57" src="https://github.com/user-attachments/assets/a9d3fbca-7188-4dcf-b73e-bc2864a4caa0" />

<img width="955" height="299" alt="VirtualBox_Kali_15_09_2026_23_30_30" src="https://github.com/user-attachments/assets/96357d18-c1fd-430b-9cf7-e7cd9c4eda48" />

<img width="955" height="533" alt="VirtualBox_Kali_15_09_2026_23_31_15" src="https://github.com/user-attachments/assets/6de8e389-7d15-4668-89b2-bd32c5a8bcfb" />

Haavoittuvuus onkin siis sama kuin aiemmassa tehtävässä, erona vain kuinka tietoihin navigoidaan. Tässä tehtävässä absoluuttisen osoitteet päästävät käyttäjän käsiksi _passwd_-hakemistoon.

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
