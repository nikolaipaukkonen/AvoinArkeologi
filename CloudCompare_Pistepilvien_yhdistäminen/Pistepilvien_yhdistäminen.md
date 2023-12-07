# Pistepilvien yhdistäminen CloudComparessa

Eräs tyypillinen 3D-aineistojen käsittelyyn liittyvä ongelma on eri aineistojen yhdistäminen ja asemointi keskenään. Moderneissa laserkeilaimissa on usein sisäänrakennettuna toiminnallisuutta, jolla eri asemista otetut keilaukset yhdistyvät automaattisesti toisiinsa, mutta välillä yhdistäminen saattaa epäonnistua. Toisinaan saattaa ilmetä myös tarve asemoida kaksi eri lähteestä olevaa aineistoa keskenään -- esimerkiksi itse olen usein skannannut ensin georeferoidun pohjakeilauksen maalaserkeilaimella, minkä jälkeen jatkuva kaivausdokumentointi on voitu hoitaa kevyemmin fotogrammetrisesti: jokainen uusi malli on sitten voitu asemoida suhteessa isoon pohjakeilaukseen. 

Tämä ohje käsittelee pistepilvien keskinäistä asemointia ja referentointia. Aineiston georeferointi on erillinen kysymys, jota varten kirjoitan erillisen ohjeen.

Asemointiin on monia menetelmiä ja ohjelmia. Tässä esittelen CloudComparessa olevaa Cloud Registration -työkalua. Peruslähtökohtana on raahata pistepilvet suurin piirtein päällekkäin, minkä jälkeen työkalu laskee pilvet yhteen [Iterative closest point](https://en.wikipedia.org/wiki/Iterative_closest_point) (ICP) -algoritmilla. Monia muitakin menetelmiä on -- esimerkiksi CloudComparessa oleva yhteisten yksittäisten pisteiden poimintaan perustuva työkalu -- mutta omassa käytössäni tämä työkalu on yleensä riittänyt.

Aloita yhdistäminen tuomalla pistepilvet samaan CloudCompare-projektiin. Jos pilvien erottumista toisistaan on vaikea hahmottaa, voi ne värjätä eri värisiksi (Edit -> Colors -> Set unique / Alt + C). 

![Kuva1](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/CloudCompare_Pistepilvien_yhdistäminen/Kuva1.png)

Valitse siirrettävä pistepilvi DB Treestä (eli eri elementtien listasta) ja aktivoi Translate/Rotate -työkalu, jolla pistepilvi raahataan paikallaan pysyvän referenssipistepilven päälle. Raahaa sitten pilvi (oikea hiirenpainike pohjassa) suurin piirtein kohdalleen. Huomioi, että voit deaktivoida jotkin ulottuvuudet kokonaan Tx, Ty ja Tz -painikkeista. Esimerkiksi joidenkin laserkeilainten aineisto saattaa tulla vakiona samalle tasolle, jolloin aineistoa ei tarvitse juurikaan liikutella korkeuskoordinaatin suhteen. Sinisellä pause-näppäimellä voi keskeyttää raahaamisen ja vaihtaa kuvakulmaa. Varsinkin suoraan ylhäältä / alhaalta oleva kuvakulma on hyödyllinen tässä vaiheessa. 

![Kuva2](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/CloudCompare_Pistepilvien_yhdistäminen/Kuva2.png)

Kun pistepilvet ovat suurin piirtein kohdillaan, on aika avata itse rekisteröintityökalu. Valitse ensin DB Treessä sekä referenssipistepilvi, että yhdistettävä pilvi. Avautuvassa ikkunassa on liuta erilaisia asetuksia. Tarkista ensin, että pilvien roolit ovat kohdillaan (aligned tarkoittaa pilveä, joka liikkuu; reference pysyy paikoillaan). Näistä kaikkein kriittisin on Final overlap. Valitse 100% vain, jos aineistot ovat tasan samasta kohdasta -- muissa tapauksissa prosenttilukua kannattaa hilata huomattavasti matalammaksi. Tyypillisesti referensointi kannattaa tehdä esimerkiksi yhden seinäpinnan perusteella, ja tällöin saattaa riittää esimerkiksi 40% tai jopa 20%. Jos yhdistettäviä pistepilviä yhdistävä osa on hyvin pieni -- vaikkapa siten, että pilvet on laserkeilattu kahdesta eri huoneesta ja yhteiset pisteet löytyvät vain oviaukon karmeista -- voi Final overlap olla jopa vain 10% tai vähemmänkin. Muut parametrit vaikuttavat yhdistämisen tarkkuuteen ja laskenta-aikaan. Kun kaikki on kohdallaan, paina OK.

![Kuva3](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/CloudCompare_Pistepilvien_yhdistäminen/Kuva3.png)

Kun rekisteröinti on ajettu läpi, lävähtää ruutuun pieni Registration info -ikkuna. Mikäli siitä tarvitsee kopion (esimerkiksi raportointia varten), voi sen copy pasteta konsolista (joka avautuu F8-näppäimellä, mikäli se ei ole jo näkyvissä). Tämän jälkeen kannattaa tarkastaa vielä visuaalisesti, että kaikki näyttää siltä, miltä pitääkin. 

![Kuva4](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/CloudCompare_Pistepilvien_yhdistäminen/Kuva4.png)

Isommissa projekteissa täytyy tietenkin rekisteröidä useita eri positioita. Jos näin on pakko tehdä, kannattaa olla systemaattinen eri positioiden nimeämisen suhteen sekä sen suhteen, mitä pilveä milloinkin käytetään referenssinä. Tyypillistä on tehdä rekiströinnit "jonossa", eli päätetään, että pilvi no. 1 toimii referenssiaineistona ja asemoidaan pilvi no. 2 sen päälle, sen jälkeen asemoidaan pilvi no. 3 käyttäen pilveä no. 2 referenssiaineistona, ja niin edelleen. 


