# Kartta-aineistojen tuominen ja käyttö WMS/WMTS-rajapintojen kautta

GIS-ohjelmat vaativat jonkinlaista tuotavaa paikkatietoaineistoa, jotta niistä on mitään iloa. Perinteisesti niihin on voitu tuoda (import) erilaisia paikallisesti tallennettuja vektori- tai rasterimuotoisia tiedostoja, jotka on tallennettu milloin mihinkin tiedostoformaattiin. Mikäli mahdollista, kannattaa kuitenkin suosia Web Map Service (WMS) tai Web Map Tile Service (WMTS) -protokolien mukaisia verkon kautta tuotavia aineistoja, kun puhutaan suuremmista kokonaisuuksista. Esimerkiksi pohjakarttaa tehdessä kannattaa käyttää WMS/WMTS:ää. Näiden ero on tekninen -- WMS tuo karttadatan yhtenä kuvana, kun taas WMTS tuo sen erillisistä pienemmistä ruuduista koostuvana kokonaisuutena. Peruskäytön kannalta ero ei ole merkittävä. Yleisesti ottaen WMTS on nopeampi käyttää. Rajapintojen käytön etuna on myös se, että aineisto päivittyy automaattisesti.

## 1. Maanmittauslaitoksen rajapinta ja API-avain

Käytetään tässä esimerkkinä Maanmittauslaitoksen (MML) (WMS/WMTS-aineistoja)[https://www.maanmittauslaitos.fi/karttakuvapalvelu]. MML tarjoaa ilmaiseksi pienimuotoiseen käyttöön WMTS-rajapinnan, jonka kautta voi käyttää mm. maastokarttaa ja kiinteistörajoja ja -tunnuksia. MML:n WMTS-yhteyden osoite on [https://avoin-karttakuva.maanmittauslaitos.fi/avoin/wmts/1.0.0/WMTSCapabilities.xml](https://avoin-karttakuva.maanmittauslaitos.fi/avoin/wmts/1.0.0/WMTSCapabilities.xml).

WMTS-rajapinnan käyttö vaatii oman API-avaimen (application programming interface, API = rajapinta). MML:n oma ohje avaimen rekisteröintiin:
1.    Rekisteröidy [OmaTili](https://omatili.maanmittauslaitos.fi/user/new/avoimet-rajapintapalvelut)-palveluun.
2.    [Kirjaudu palveluun](https://omatili.maanmittauslaitos.fi/user/profile) rekisteröimälläsi käyttäjätunnuksella.
    Kirjautumisen jälkeen voit
    - luoda uuden API-avaimen,
    - poistaa olemassa olevan API-avaimen.
    - muokata tietojasi tai poistaa käyttäjätunnuksesi.

![Kuva 1: API-avaimen luominen](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/QGIS_WMS-aineistojen_kaytto/Kuva1.png?raw=true)

## 2. Rajapintaan yhdistäminen

Avaa QGIS ja luo uusi projekti. Mene Layer -> Add Layer -> Add WMS/WMTS Layer (Ctrl+Shift+W). Valitse ylärivistä nappi New. Anna yhteydelle sopiva nimi (esim. "Maanmittauslaitos WMTS") ja kopioi kohtaan URL yllä oleva URL, joka päättyy ".xml". Muuten asetuksiin ei tarvitse koskea. Klikkaa OK.

![Kuva 2: Uuden yhteyden luominen](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/QGIS_WMS-aineistojen_kaytto/Kuva2.png?raw=true)

Nyt Data Source Managerissa pitäisi Maanmittauslaitos WMTS:n kohdalla olla aktiivisena Connect-painike.

![Kuva 3: Data Source Manager](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/QGIS_WMS-aineistojen_kaytto/Kuva3.png?raw=true)

Paina Connect. Nyt pitäisi aueta Enter Credentials -ruutu. Vaiheessa 1. luotu API-avain syötetään tänne. Kopioi ja liitä se kohtaan Username -- kohta Password jää tyhjäksi.

![Kuva 4: API-avaimen syöttäminen](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/QGIS_WMS-aineistojen_kaytto/Kuva4.png?raw=true)

Nyt pitäisi aueta Tilesets-näkymä. Valitse haluamasi klikkaamalla (esim. Maastokartta) ja paina alaoikealta Add.

![Kuva 5: Tilesets](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/QGIS_WMS-aineistojen_kaytto/Kuva5.png?raw=true)

Paina Close. Nyt kartta-aineiston pitäisi olla näkyvissä. Lähentäessä ja loitontaessa kartta päivittyy automaattisesti sopivaan tarkkuuteen, mutta yhteyden laadusta riippuen tässä saattaa kestää hetki. 

![Kuva 6: Kartta esillä](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/QGIS_WMS-aineistojen_kaytto/Kuva6.png?raw=true)

WMS/WMTS-yhteyksien luominen onnistuu myös klikkaamalla WMS/WMTS-kohtaa Browser-työkaluikkunassa, jonka saa näkyviin valitsemalla View -> Panels -> Browser.

![Kuva 7: Browser-työkaluikkuna](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/QGIS_WMS-aineistojen_kaytto/Kuva7.png?raw=true)

## 3. Muita hyödyllisiä rajapintalinkkejä

Muista noudattaa rajapintojen ylläpitäjien käyttösopimuksia ja ohjeita. Vaikka palvelu olisi avoin ja ilmainen, voi sen lisenssiin liittyä ehtoja, joita kuuluu noudattaa. Esimerkiksi OpenStreetMap vaatii, että sen käytöstä pitää mainita julkaisemisen yhteydessä.
- [Museoviraston rajapinta](https://www.museovirasto.fi/fi/palvelut-ja-ohjeet/tietojarjestelmat/kulttuuriympariston-tietojarjestelmat/kulttuuriympaeristoen-paikkatietoaineistot) on Suomessa toimivan arkeologin perustyökalu
- [Suomen ympäristökeskus](https://www.syke.fi/fi-FI/Avoin_tieto/Avoimet_rajapinnat) tarjoaa avoimen rajapinnan ympäristötietojärjestelmien julkisiin aineistoihin
- [Metsäkeskus](https://www.metsakeskus.fi/fi/avoin-metsa-ja-luontotieto/aineistot-paikkatieto-ohjelmille/rajapinnat) tarjoaa metsiin liittyviä aineistoja liittyen metsiin
- [OpenStreetMap](https://wiki.openstreetmap.org/wiki/WMS#OSM_WMS_Servers) on avoin ja ilmainen karttarajapinta, joka kattaa koko maailman. URL-osoitteita varten selaa alaspäin kohtaan kohtaan OSM WSM Servers.
- [GeoSeer](https://www.geoseer.net/) on WMS-palveluita kokoava hakupalvelu. Kokeile vaikkapa hakusanaa "Archaeology"
- [Spatineo](https://directory.spatineo.com/) on toinen hyödyllinen hakupalvelu
