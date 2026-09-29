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

## c2) The interesting non-200
Seuraavaksi ryhdyin suodattamaan aikaisemmin saadusta tulosteestamme pois kaikki tulosteet jotka eivät olleet statuskoodi 200. Tehtävässä oli tarkoituksena käyttää komennossa funktioita ```-mc all``` sekä ```fc```. Ffuf -h komennon avulla pystymme näkemään, että ```-mc all``` viittaa HTTP statuskoodeihin kun taas ```-fc``` filtteröi tuloksia. Komennoksemme muodostuukin siis ```ffuf -w content.txt -u https://ffuf.io.fi/FUZZ -mc all -fc 200```

<img width="770" height="508" alt="VirtualBox_Kali_30_09_2026_00_32_05" src="https://github.com/user-attachments/assets/5bde2d9c-8ce1-4eb4-94d5-17a02a6e0961" />

Voisimme ottaa tilanteessa myös käyttöömme ```-ac``` komennon lisän (auto calibration), joka rajaa pois ns. "roskavastaukset". 

## c3) Recursion
Selvittääkseni aikaisempien suodatettujen kansioiden sisältöä pystyin kääntymään ```-recursion``` ja ```recursion-depth``` komentojen puoleen. ```-recursion``` komennolla kutsumme komentoamme käyttämään rekursiivista hakua, joka alkaa katsomaan mahdollisia polkuja haussamme. ```recursion-depth``` komennolla taas pystymme rajoittamaan kuinka syvälle hakuja teemme.

Syötin komentoriville komennon /usr/local/bin/ffuf -w content.txt -u https://ffuf.io.fi/FUZZ -recursion -recursion-depth 1 -ac. Tässä komennossa -recursion käskee ohjelmaa aloittamaan sanalistan läpikäymisen automaattisesti alusta jokaisen löydetyn uuden kansion kohdalla. Lisäsin mukaan vivun -recursion-depth 1, joka rajoittaa kansion sisään sukeltamisen vain yhden tason syvyyteen jottei skannaus karkaa loputtomiin alikansioihin.

Tulosteesta huomasin, että ohjelma lisäsi löytämänsä hakemistot työjonoon (esim. Adding a new job to the queue) ja alkoi skannata niitä vuorotellen. Tämän avulla sain esiin syvemmälle piilotettuja tiedostoja, joita pelkkä etusivun skannaus ei olisi ikinä löytänyt. Tuloksista paljastui muun muassa /backup/-kansion sisältä tietokannan kopio db.sql.bak, sekä muiden kansioiden sisältä uusia polkuja kuten v2, 2024, 2025 ja 2026.
## c4) Virtual hosts
## c9) The login you cannot replay (Has preflight! Has CSRF token!)

## Lähteet:
Chatgpt, Kielimalli GPT-6 Astra

Hoikkala, 2026, Fuzzing with Fuff, Luettavissa: https://terokarvinen.com/tunkeutumistestaus/hoikkala-2026-fuzzing-with-ffuf.pdf Luettu 27.9.2026

Hoikkala, 2026, ffuf README.md, Luettavissa: https://github.com/ffuf/ffuf/blob/master/README.md) Luettu 29.9.26
