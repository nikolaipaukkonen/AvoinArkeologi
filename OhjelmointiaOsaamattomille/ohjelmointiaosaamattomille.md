# Ohjelmointia osaamattomille

Arkeologiaan kuuluu nykyään välttämättömänä pahana tietokoneella istuminen ja erilaisten ohjelmistojen käyttö. Vähintäänkin karttojen ja raporttien laatiminen vaatii päätteellä istumista, puhumattakaan tutkimussuuntauksista, joihin kuuluvat erilaiset analyysit, prosessoinnit ja simuloinnit. Useimmiten näihin käytettävät ohjelmistot eivät ole arkeologeja varten suunniteltuja, minkä vuoksi niiden käyttö vaatii joskus luovuutta ja joustavuutta. Ohjelmistokehitys on hidasta ja kallista, minkä vuoksi harvat arkeologeille tarkoitetut ohjelmistot ovat yleensä arkeologien itsensä kehittämiä. Koodaaminen on kuitenkin vuosien aikana karttuva taito, ja vaikka taitoa olisikin, on käyttökelpoisen ohjelman kirjoittaminen joka tapauksessa hidasta ja monimutkaista puuhaa.

Vaan ei enää! Uusimmat tekoälypohjaiset kielimallit (Large Language Model, LLM) tuottavat niin hyvää koodia, että riittää, kun käyttäjä osaa kuvailla tarkasti sen, mitä haluaa ohjelmiston tekevän. Pieniä koodinpätkiä on helppo tuottaa ja käyttää ChatGPT:n tai muun vastaavan avulla. Kielimallia voi esimerkiksi pyytää kirjoittamaan Powershell-koodia, jolla muuttaa kaikki kansion tiedostonimet seuraamaan tiettyä kaavaa, tai luokitella eri tyyppiset tiedostot omiin kansioihinsa.

Halusin testata eri kielimallien kykyä kirjoittaa kokonainen Internet-selaimessa toimiva pieni ohjelma. Esimerkiksi valikoitui ohjelma, joka tekisi stratigrafisten yksiköiden välisiä suhteita kuvaavan taulukon perusteella Harrisin matriisin. Ideana oli, että kaiken koodin pitäisi mahtua yhteen tiedostoon ja syntyä yhden vastauksen aikana. Testeissä käytettiin seuraavia malleja:

| Julkaisija | Malli | Julkaistu |
|------------|-------|-----------|
| OpenAI | GPT-4o | Toukokuu 2024 |
| Claude (Anthropic) | Haiku 3.5 | Lokakuu 2024 |
| Copilot (Microsoft) | GPT-4 Turbo (Copilot) | 2024 |
| Gemini (Google) | 2.0 Flash | Helmikuu 2025 |
| Cursor | GPT-4o-mini | Heinäkuu 2024 |
| Mistral AI | Mistral small 3.1 | Maaliskuu 2025 |

Niille annettiin seuraava CSV-tiedosto, joka kuvaa yksinkertaisia stratigrafisia relaatioita:

| unitno | type | above | below |
|--------|------|-------|--------|
| 1 | deposit | 2 | |
| 2 | deposit | 3;4;7 | 1 |
| 3 | structure | 2;6 | 2 |
| 4 | deposit | 5 | 2 |
| 5 | deposit | 8 | 4 |
| 6 | deposit | 8 | 3 |
| 7 | deposit | 8 | 2 |
| 8 | deposit | | 5;6;7 |

Minkä jälkeen kielimallille annettiin alla oleva ohjeistussyöte (tiivistetty verkkoversioon):

- Luoda Harrisin matriisi -automaatti, jolla arkeologit voivat generoida visuaalisen Harrisin matriisin strukturoidusta stratigrafisesta datasta
- Käyttäjä lataa CSV-tiedoston
- Sovellus visualisoi stratigafiset suhteet ylhäältä alas -hierarkkisena kuvana, jossa uusimmat yksiköt ovat ylhäällä ja vanhimmat alhaalla
- Teknisiä vaatimuksia: 
  - Kaikki koodi yhdessä HTML-tiedostossa
  - Käyttää HTML, CSS ja JavaScriptiä
  - Mahdollisesti D3.js-kirjasto apuna
  - Eri yksikkötyypeillä eri muodot (deposit = soikio, structure = suorakulmio)
  - Toimii sekä desktop- että mobiiliversiona

Tulokset:

### Claude

![Claude Harris Matrix](screenshots/Kuva1.png)

- Matriisi piirtyi periaatteessa oikein, joskin kyljellään
- Eri yksikkötyypit eritelty väreillä
- Koodia: 269 riviä

### Cursor

![Cursor Harris Matrix](screenshots/Kuva2.png)

- Matriisi piirtyi oikein
- Yksikkötyypit eritelty ohjeiden mukaisesti
- Alkuasetelmassa pallukat olivat epämääräisessä kasassa
- Koodia: 278 riviä

### Gemini

![Gemini Harris Matrix](screenshots/Kuva3.png)

- Alkuasetelma: yksikköpallukat päällekkäin
- Linkit oikein
- Mielenkiintoinen tulkinta rakenneyksiköstä
- Koodia: 458 riviä

### Copilot

![Copilot Harris Matrix](screenshots/Kuva4.png)

- Matriisi piirtyi periaatteessa oikein
- Yksikkötyypit eroteltu pelkän värin mukaan
- Generoitui kyljellään
- Koodia: 157 riviä

### OpenAI GPT-4

![OpenAI GPT-4 Harris Matrix](screenshots/Kuva5.png)

- Yksikkötyypit eritelty oikein
- Linkit näyttävät oikeilta
- Yksiköt epämääräisessä kasassa
- Koodia: 272 riviä

### Mistral

![Mistral Harris Matrix](screenshots/Kuva6.png)

- Yksiköiden numerot eivät näy
- Matriisi vaikuttaa oikeelliselta
- Yksikkötyypit eritelty muodon perusteella
- Yksiköitä voi raahata, mutta ne jäävät sivuun
- Koodia: 163 riviä

## Yhteenveto

Kaiken kaikkiaan mallien suoritus on melko hyvä: lopputulokset syntyivät yhdellä tai kahdella ohjeistuksella muutamassa minuutissa. Kaikki ohjelmat toimivat myös isommilla aineistoilla (testasin jokaista esimerkkidatalla jossa oli 28 yksikköä). 

Yhtäkään näistä ei ehkä sellaisenaan kannata käyttää, mutta niiden muokkaaminen ja jatkokehittäminen olisi tarvittaessa helppoa joko koodaamalla itse tai käskemällä kielimalleja tekemään parannuksia.
