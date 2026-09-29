# Harjoitus 6: Fuzzy Feeling Upon Finding
- Kurssi: Tunkeutumistestaus (Karvinen 2026)
- Opettaja: Tero Karvinen
- Raportin kirjoittaja: Vili Virtanen
## x) Materiaalit:
### Hoikkala 2026: Fuzzing with Fuff
- HTTP bruteforce työkalu.
- Lähettää suuren määrän pyyntöjä ja havaitsee poikkeamia.
- Kohdistettavissa mihin tahansa HTTP-pyynnön osaan.
- Käyttää sanakirjoja, joissa on hyvä luoda omat sanakirjat esimerkiksi valmiiden pohjien avulla.

```
HTTP-statuskoodi: -mc / -fc
- Esim. täsmäys 200 OK -vastauksiin

Rivien määrä -ml / -fl

Sanojen määrä -mw / -fw
- Jos tuloste sisältää syötetyn arvon

Vastauksen sisältöpituus -ms / -fs
- Jos vastaukset ovat staattisia

Vasteaika -mt / -ft
- Hitaat päätepisteet, SQL-injektiot

Automaattinen kalibrointi käytettävissä: -ac
```

## a) Tallenna itsellesi kopio säännöistä. Kirjoita omin sanoin,

### Scope. Mikä on kohde?
https://ffuf.io.fi/play on kohdekone fuzzing-testaukselle. Mikään kohteella ei ole aitoa eikä haurasta, joten se soveltuu täydellisesti fuffin testaukseen.
### Rules of engagement. Mitä sille saa tehdä, eli mitä tai millaisia menetelmiä saa käyttää?
Kohteesta on tarkoitus fuffin avulla löytää seuraavat kymmenen asiaa, jotka kattavat työkalun toiminnot:
- Sanastot ja avainsanan sijoittaminen, 
- Täsmäytys ja suodatus
- Kalibrointi
- Rekursio
- Virtuaaliisännät
- Parametrit
- Raa’at pyynnöt
- Sanaston lukeminen vakiosyötteestä (stdin) sekä pyynnöt, jotka on muodostettava aiemman vastauksen perusteella.
### Mihin oikeutesi tehdä tietoturvatestausta tähän kohteeseen perustuu?
Sivusto kertoo kyseessä olevan FUZZING DEMO TARGET. Sivusto myös erikseen listaa tehtäviä joita suorittaa sivustolla käyttäen fuzzausta.
Palvelun ylläpitäjä on itse asettanut kyseisen palvelimen fuzzauksen harjoittelukohteeksi ja julkaissut siihen liittyvät säännöt sekä tehtävät.
### Riskit ja mitigointi. Tuo palvelin on Internetissä. Tunnista lyhyesti riskit ja niiden mitigointi ennen käytännön harjoittelua.
Verkkosivu on julkinen ja siihen yhdistetään avoimessa verkossa. On siis hyvä varmistaa kohteen olevan oikea ennen harjoituksen alkua, ettei tutkintamme yllä luvallisen kohteen ulkopuolelle. On hyvä myös ymmärtää useamman oppilaan tekevän samoja tehtäviä, joten lähettämiä pyyntöjämme on hyvä rajoittaa.
## b) Asenna ffuf versio, joka tukee aivan uutta preflight-ominaisuutta.
Sivusto pyytää meitä asentamaan ffuf v2.3.0-version. Ennen kuin pystymme asentamaan fuffia, vaatii tämä kuitenkin go-compilerin. Tämän asentaminen onnistuu helposti komennolla ```sudo apt install gccgo-go```. Seuraavaksi voimme ryhtyä asentamaan fuffia komennolla ```go install github.com/ffuf/ffuf/v2@latest```. Seuraavaksi tarkistin fuff version komennolla ```fuff -V```, mutta komento palautti versionani 2.1.0. 

Haluamme kuitenkin versioksi version 2.3.0. Huomasin fuffia asentaessa tämän valittavan väärästä gccgo versiosta, joten tarkistin version komennolla ```go version```, jonka jälkeen päivitin tämän ja yritin päivittää fuffin uudelleen.

<img width="695" height="192" alt="VirtualBox_Kali_29_09_2026_21_52_59" src="https://github.com/user-attachments/assets/bcae8709-2394-4a0d-99b3-7afedd4e5499" />

Kokeilin tällä kertaa käyttää ohjeissa olevaa ```git clone https://github.com/ffuf/ffuf ; cd ffuf ; go get ; go build```-komentoa, mutta jälleen kerran asennus valitti go-versioni olevan väärin? Kokeilin asentaa Go-kielen vielä kerran komennolla ```sudo apt install golang-go```, josta näyttikin heti asentuvan versio 1.26! Samalla asennus poisti myös gccgo-asennuksen...

<img width="937" height="669" alt="VirtualBox_Kali_29_09_2026_22_29_45" src="https://github.com/user-attachments/assets/34e99164-196b-47ee-8a80-0fa5d37a873d" />

Tarkistetaampas vielä go-versio tutulla ```go version``` komennolla.

<img width="338" height="71" alt="VirtualBox_Kali_29_09_2026_22_30_08" src="https://github.com/user-attachments/assets/5db3573d-764b-4d65-89b4-c49e28ea53b1" />

Oikein! Kokeillaan taas komentoa ```git clone https://github.com/ffuf/ffuf ; cd ffuf ; go get ; go build```!

<img width="695" height="392" alt="VirtualBox_Kali_29_09_2026_22_59_11" src="https://github.com/user-attachments/assets/b3a5f759-40e3-40fc-9773-12990bb937b7" />

Go-komento ei näytä asentavan ffufia...

Tässä vaiheessa päätin putsata kaikki aiemmat asennukseni komennoilla:
```
sudo apt remove --purge ffuf -y
sudo rm -f /usr/local/bin/ffuf
sudo rm -f /usr/bin/ffuf
rm -f ~/go/bin/ffuf
rm -rf ~/ffuf
go clean -modcache
hash -r
```

Yritin tämän jälkeen toistaa aiemmat askeleet lataamalla ja asentamalla komennolla ```git clone https://github.com/ffuf/ffuf ; cd ffuf ; go get ; go build```, sekä komennolla ```go install github.com/ffuf/ffuf/v2@latest```, mutta molemmat komennot vain latasivat github repositorion minulle, eivätkä asentaneet tätä.

Taistelin tämän kanssa useamman tuntia, luovutin ja kysyin apua chatgpt kielimallilta GPT-6 Astra seuraavalla promptilla:

```
"Yritän asentaa virtuaalikoneelleni korkeakoulun tehtävää varten ffuf-ohjelmaa. Kone on Kali Linux pohjainen ja yritän käyttää golang-avulla ohjelman simppeliä asennusta, mutta ohjelman molemmat annetuista asennuskomennoista ei toimi.

Komento: "go install github.com/ffuf/ffuf/v2@latest" ei tee yhtään mitään, kun taas komento: git "clone https://github.com/ffuf/ffuf ; cd ffuf ; go get ; go build" vain lataa repositorion minulle. Yrittäessäni tarkistaa versiota Kali-koneeni ilmoittaa että ffuf ei ole asennettuna, haluanko asentaa sen? Ongelmana on, että tarvitsen githubin kautta ladattavan v2.3.0.-version ja sudo install ffuf antaa minulle 2.1.0.-version."
```

Neuvojen avuilla minulle selvisi että ffuf kyllä asentuu laitteelle, mutta tämän polku on sotkussa. Neuvon avulla pääsin seuraavaan komentoketjuun:
```
go install github.com/ffuf/ffuf/v2@latest
echo 'export PATH="$PATH:$(go env GOPATH)/bin"' >> ~/.zshrc
source ~/.zshrc
which ffuf
ffuf -V
```

<img width="264" height="165" alt="VirtualBox_Kali_30_09_2026_00_04_23" src="https://github.com/user-attachments/assets/387c2e42-cce3-46fc-867b-af92329b08c4" />

Joka SILTI antoi minulle version 2.1.0. Tässä vaiheessa minulle selvisi että versiointi on ladattava GitHubin julkaisusta erikseen. Hoikkalaa kiroten pääsin VIHDOIN lopulliseen tulokseeni komennoilla:
```
cd /tmp
wget https://github.com/ffuf/ffuf/releases/download/v2.3.0/ffuf_2.3.0_linux_amd64.tar.gz
tar -xzf ffuf_2.3.0_linux_amd64.tar.gz
./ffuf -V
mkdir -p ~/.local/bin
mv ffuf ~/.local/bin/
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
which ffuf
ffuf -V
```

<img width="525" height="522" alt="VirtualBox_Kali_30_09_2026_00_13_05" src="https://github.com/user-attachments/assets/448a1ff5-1689-4f64-bdfb-0326240693ef" />

Komentoketju lataa uusimman version ffufista, purkaa sen, siirtää sen sisällön bin-hakemistoon ja saa tämän polun näkymään oikein.

## c1) Content discovery (Vaultline https://ffuf.io.fi/play tehtävät on numeroitu näin, käytetään tässä samoja.).
Seuraavaksi pääsin vihdoin tehtävien pariin. Tarkoituksena oli ladata Kali-koneelle talteen demoa varten luodut wordlistit, eli ffufin hakema sisältö, sekä sanakirjat salasanoille joita ffuf käyttäisi myöhemmin. Wordlistis ja sanakirjat latautuivat komennoilla: 
```
curl -O https://ffuf.io.fi/wordlists/content.txt 
curl -O https://ffuf.io.fi/wordlists/passwords.txt
```

<img width="725" height="191" alt="VirtualBox_Kali_30_09_2026_00_24_45" src="https://github.com/user-attachments/assets/cfd5a418-73e1-4228-97e8-ac73df01b89c" />

Nyt pääsimme vihdoin kohdesivuston kimppuun komennolla ```ffuf -w content.txt -u https://ffuf.io.fi/FUZZ```!

<img width="804" height="608" alt="VirtualBox_Kali_30_09_2026_00_26_31" src="https://github.com/user-attachments/assets/5c1f9e1b-36df-4775-a00b-322b62d1195b" />

Lisäämällä komentoon ```-ac```-parametrin, pystymme myös rajaamaan pois ns. "roskavastaukset". 

<img width="766" height="622" alt="VirtualBox_Kali_30_09_2026_00_58_55" src="https://github.com/user-attachments/assets/41850c12-d996-4f1b-918e-0f43f4c32409" />

Käyttämällä parametria ```-rate 100```, voimme rajoittaa sekunnin aikana tehtyjä pyyntöjä sataan, jotta palvelin ei kuormittuisi hirveästi.
## c2) The interesting non-200
Seuraavaksi ryhdyin suodattamaan aikaisemmin saadusta tulosteestamme pois kaikki tulosteet jotka eivät olleet statuskoodi 200. Tehtävässä oli tarkoituksena käyttää komennossa funktioita ```-mc all``` sekä ```fc```. Ffuf -h komennon avulla pystymme näkemään, että ```-mc all``` viittaa HTTP statuskoodeihin kun taas ```-fc``` filtteröi tuloksia. Komennoksemme muodostuukin siis ```ffuf -w content.txt -u https://ffuf.io.fi/FUZZ -mc all -fc 200```

<img width="770" height="508" alt="VirtualBox_Kali_30_09_2026_00_32_05" src="https://github.com/user-attachments/assets/5bde2d9c-8ce1-4eb4-94d5-17a02a6e0961" />

Tehtävässä toimisi myös aiemman tehtävän ```-ac```-lisäke.
## c3) Recursion
Selvittääkseni aikaisempien suodatettujen kansioiden sisältöä pystyin kääntymään ```-recursion``` ja ```recursion-depth``` komentojen puoleen. ```-recursion``` komennolla kutsumme komentoamme käyttämään rekursiivista hakua, joka alkaa katsomaan mahdollisia polkuja haussamme. ```recursion-depth``` komennolla taas pystymme rajoittamaan kuinka syvälle hakuja teemme.

Käytin polkujen tutkimiseen komentoa ```ffuf -w content.txt -u https://ffuf.io.fi/FUZZ -recursion -ac -recursion-depth 2```, joka hakee osuman jälkeen polkuja, lopettaen haun 2 polun jälkeen jotta tämä ei karkaisi aivan käsistä. 

<img width="798" height="701" alt="VirtualBox_Kali_30_09_2026_01_03_47" src="https://github.com/user-attachments/assets/4bd0e077-22a5-43a4-afa5-9ee9809b1250" />

Tulosteesta näemme komennon lisäävän hakusanojen perusteella löydetyt hakemistot työjonoon (Adding a new job to the queue) ja ryhtyy käymään näitä läpi antamiemme parametrien avulla. Tällä tavalla pysymme löytämään toistensa alle piilotettuja tiedostoja, joita normaali skannaus ei löydä.
## c4) Virtual hosts
Seuraavana tavoitteenani oli löytää palvelimen taustalta kolme piilotettua virtuaalipalvelinta. Vinkkimme tehtävään on, ettei avainsanan tarvitse sisältyä URL-osoitteeseen. Osoittamalla ```-u```-parametriamme pääverkkotunnukseen ja asettamalla `FUZZ` Host-otsikkotietoon. Osoittaessa ```-u```-parametria aliverkkotunnukseen varmenne kattaa vain pääverkkotunnuksen jolloin kättely  hylätään, eikä HTTP-yhteyttä muodostu lainkaan. Kaikki pyynnöt, jotka eivät vastaa jotakin näistä kolmesta, ohjautuvat oletussivustolle, joten tarvitsemme suodattimen. Komentoni alkuun näytti siis tältä:
```
ffuf -w content.txt -u https://ffuf.io.fi/FUZZ -H "Host: FUZZ.ffuf.io.fi"
```
Komentoni kuitenkin antoi erittäin laajan lajitelman tuloksia, joista suurimassa osassa oli kuitenkin 135 sanaa. Lisäämällä komentoon ```-fw``` parametrin pystyn kuitenkin suodattamaan pois haluamani vastaukset, ja yritinkin uudelleen suodattamalla nämä pois uudella versiolla komennosta:
```
ffuf -w content.txt -u https://ffuf.io.fi/FUZZ -H "Host: FUZZ.ffuf.io.fi" -fw 135
```

<img width="785" height="661" alt="VirtualBox_Kali_30_09_2026_01_21_07" src="https://github.com/user-attachments/assets/6f755b9f-b220-424c-875a-dfd4472fcc22" />

Näemme, että saamamme tulos on nyt huomattavasti pienempi! Mutta ei kuitenkaan kolmea? Valitettavasti en kyseisessä tehtävässä päässyt pidemmälle...
## c9) The login you cannot replay (Has preflight! Has CSRF token!)
Lopuksi tutustuin Ffufin uuteen _preflight_-toimintoon! Aloitin tarkistamalla ominaisuuden toiminnan komennolla ```ffuf -h | grep -c preflight```

<img width="327" height="68" alt="VirtualBox_Kali_30_09_2026_01_30_47" src="https://github.com/user-attachments/assets/f9c36463-d679-4fb0-a5d3-57fa112ccc3e" />

Tulos ei ole 0, eli se toimii! Seuraavaksi ajamaan tehtävänannon meille tarjoama koodi:

```
cat > login.raw <<'EOF'
GET /login HTTP/1.1
Host: ffuf.io.fi
Accept: text/html

EOF

ffuf -w passwords.txt -u https://ffuf.io.fi/login -X POST \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "csrf_token=CSRFTOKEN&username=admin&password=FUZZ" \
  -preflight login.raw \
  -preflight-var 'CSRFTOKEN:name="csrf_token" value="([a-f0-9]+)"' \
  -preflight-mode per-request \
  -mc 302
```

<img width="809" height="722" alt="VirtualBox_Kali_30_09_2026_01_33_13" src="https://github.com/user-attachments/assets/e8680304-0918-47be-903d-762a89d74b78" />

## Lähteet:
Chatgpt, Kielimalli GPT-6 Astra

Hoikkala, 2026, Fuzzing with Fuff, Luettavissa: https://terokarvinen.com/tunkeutumistestaus/hoikkala-2026-fuzzing-with-ffuf.pdf Luettu 27.9.2026

Hoikkala, 2026, ffuf README.md, Luettavissa: https://github.com/ffuf/ffuf/blob/master/README.md) Luettu 29.9.26

Vaultline Oy, 2026, Vaultline – fuzzing demo target for the ffuf talk. Luettavissa: https://ffuf.io.fi/play Luettu: 29.9.2026.
