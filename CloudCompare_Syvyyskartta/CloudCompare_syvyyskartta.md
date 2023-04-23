# Syvyyskartan tekeminen CloudComparessa

Tällä ohjeella voi tehdä värjätyn syvyyskartan (depth map) CloudComparessa 3D-aineistolle (verkolle tai pistepilvelle). Aloitetaan tuomalla käsiteltävä aineisto ohjelmaan (File→ Open / Ctrl+O). Esimerkissä on kyse roomalaisen monumentaali-inskription fragmentista, joka on dokumentoitu fotogrammetrisesti.

Kuva 1.

Tässä tapauksessa haluan tehdä syvyyskartan vain itse kirjoituksesta, joten leikkaan sen erilleen Segment-työkalulla (saksien kuva).

Kuva 2.

Seuraavaksi luodaan avuksi taso-olio (Plane), josta saaduilla sijaintitiedoilla voidaan korjata itse malli tasaisesti Z-tasolle. Valitse ensin vasemmalla DB Treessä käsiteltävä aineisto ja paina sitten Edit → Plane → Fit. Alas konsoliin ilmestyy lista numeerisia arvoja. Valitse ja kopioi nämä arvot Ctrl+C:llä.

Kuva 3.

Valitse sitten käsiteltävä aineisto uudestaan DB Treessä ja mene Edit → Apply transformation (Ctrl+T). Liitä kopioimasi arvot kenttään ja paina OK.

Kuva 4.

Nyt aineiston pitäisi maata tasaisesti Z-tasolla. Voit tarkistaa tämän työkaluriviltä esim. Set front view tai Set left side view -nappuloista (valkea laatikko jossa oranssi sivu).

Kuva 5.

Seuraavaksi toteutetaan itse värjäys. Valitse taas aineisto DB Treessä ja paina sitten Tools → Projection → Export Coordinate(s) to SF. 

Kuva 6.

Värjäys on valmis. Kohteen Properties-valikon kohdissa Color Scale ja SF display params voi muokata värjäystä sopivampaan muotoon. Color Scalen alla olevasta visible-täpästä saa mitta-asteikon näkyviin. 

Kuva 7.

Värjäysasetuksien suhteen ei ole yhtä oikeaa toimintatapaa, ja paljon riippuu siitä, mitä halutaan korostaa. Esimerkiksi esimerkin piirtokirjoituksen kohdalla alempaa pienemmällä kaiverrettua tekstiä korostettaessa ylemmän rivin kirjoitus hälvenee näkyvistä. Myös esimerkiksi EDL shaderin laittaminen päälle voi auttaa tämän kaltaisissa kohteissa (Display → Shaders & Filters → EDL shader). 

Kuva 8.
