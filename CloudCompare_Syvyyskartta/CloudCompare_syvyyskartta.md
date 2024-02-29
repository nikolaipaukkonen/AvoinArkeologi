# Syvyyskartan tekeminen CloudComparessa

Tällä ohjeella voi tehdä värjätyn syvyyskartan (depth map) CloudComparessa 3D-aineistolle (verkolle tai pistepilvelle). Aloitetaan tuomalla käsiteltävä aineisto ohjelmaan (File→ Open / Ctrl+O). Esimerkissä on kyse roomalaisen monumentaali-inskription fragmentista, joka on dokumentoitu fotogrammetrisesti.

![Kuva1](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/CloudCompare_Syvyyskartta/Kuva1.png?raw=true)

Tässä tapauksessa haluan tehdä syvyyskartan vain itse kirjoituksesta, joten leikkaan sen erilleen Segment-työkalulla (saksien kuva).

![Kuva2](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/CloudCompare_Syvyyskartta/Kuva2.png?raw=true)

Seuraavaksi luodaan avuksi taso-olio (Plane), josta saaduilla sijaintitiedoilla voidaan korjata itse malli tasaisesti Z-tasolle. Valitse ensin vasemmalla DB Treessä käsiteltävä aineisto ja paina sitten Edit → Plane → Fit. Alas konsoliin ilmestyy lista numeerisia arvoja. Valitse ja kopioi nämä arvot Ctrl+C:llä.

![Kuva3](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/CloudCompare_Syvyyskartta/Kuva3.png?raw=true)

Valitse sitten käsiteltävä aineisto uudestaan DB Treessä ja mene Edit → Apply transformation (Ctrl+T). Liitä kopioimasi arvot kenttään ja paina OK.

![Kuva4](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/CloudCompare_Syvyyskartta/Kuva4.png?raw=true)

Nyt aineiston pitäisi maata tasaisesti Z-tasolla. Voit tarkistaa tämän työkaluriviltä esim. Set front view tai Set left side view -nappuloista (valkea laatikko jossa oranssi sivu).

![Kuva5](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/CloudCompare_Syvyyskartta/Kuva5.png?raw=true)

Seuraavaksi toteutetaan itse värjäys. Valitse taas aineisto DB Treessä ja paina sitten Tools → Projection → Export Coordinate(s) to SF. 

![Kuva6](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/CloudCompare_Syvyyskartta/Kuva6.png?raw=true)

Värjäys on valmis. Kohteen Properties-valikon kohdissa Color Scale ja SF display params voi muokata värjäystä sopivampaan muotoon. Color Scalen alla olevasta visible-täpästä saa mitta-asteikon näkyviin. 

![Kuva7](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/CloudCompare_Syvyyskartta/Kuva7.png?raw=true)

Värjäysasetuksien suhteen ei ole yhtä oikeaa toimintatapaa, ja paljon riippuu siitä, mitä halutaan korostaa. Esimerkiksi tämän piirtokirjoituksen kohdalla alempaa pienemmällä kaiverrettua tekstiä korostettaessa ylemmän rivin kirjoitus hälvenee näkyvistä. Yksi vaihtoehto on leikata kumpikin taso omaksi oliokseen ja tehdä käsittely kummallekin erikseen. Myös EDL shaderin (Eye-Dome Lighting) laittaminen päälle voi auttaa tämän kaltaisissa kohteissa (Display → Shaders & Filters → EDL shader). 

![Kuva8](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/CloudCompare_Syvyyskartta/Kuva8.png?raw=true)
