# Harjoitus 4: Täysin Laillinen Sertifikaatti
## x) Materiaalit
### A01:2021 – Broken Access Control 
- Pääsynvalvonta varmistaa käytäntöjen noudattamisen niin etteivät käyttäjät voi toimia sallittujen oikeuksiens ulkopuolella.
- Häiriötilanteet johtavat yleisesti tiedon luvattomaan paljastumiseen, muuttamiseen tai tuhoutumiseen.
### PortSwigger Academy: Insecure direct object references (IDOR)

### PortSwigger Academy: Path traversal

### PortSwigger Academy: Cross-site scripting

## a) Totally Legit Sertificate. 
Asenna OWASP ZAP, generoi CA-sertifikaatti ja asenna se selaimeesi. Laita ZAP proxyksi selaimeesi. Laita ZAP sieppaamaan myös kuvat, niitä tarvitaan tämän kerran kotitehtävissä. Osoita, että hakupyynnöt ilmestyvät ZAP:n käyttöliittymään. (Voi vaatia Firefox about:config network.proxy.allow_hijacking_localhost. Foxyproxy laittoi tämän aiemmin päälle itse. Kalin Firefox ESR oli viimeksi ongelmia Foxyproxyn kanssa - vaihtoehtona on asettaa Proxy käsin Settings, hakusana "proxy")

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
OWASP 2021: OWASP Top 10:2021 - Broken Access Control. Luettavissa: https://top10.owasp.org/2021/A01_2021-Broken_Access_Control/ Luettu 13.9.2026

PortSwigger Academy - Insecure direct object references (IDOR)

PortSwigger Academy - Path traversal

PortSwigger Academy - Cross-site scripting

Karvinen Tero 2026. Täysin Laillinen Sertifikaatti. Luettavissa: https://terokarvinen.com/tunkeutumistestaus/ Luettu 13.9.2026
