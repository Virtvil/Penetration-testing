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
## c1) Content discovery (Vaultline https://ffuf.io.fi/play tehtävät on numeroitu näin, käytetään tässä samoja.).
## c2) The interesting non-200
## c3) Recursion
## c4) Virtual hosts
## c9) The login you cannot replay (Has preflight! Has CSRF token!)

## Lähteet:
Hoikkala, 2026, Fuzzing with Fuff, Luettavissa: https://terokarvinen.com/tunkeutumistestaus/hoikkala-2026-fuzzing-with-ffuf.pdf Luettu 27.9.2026
