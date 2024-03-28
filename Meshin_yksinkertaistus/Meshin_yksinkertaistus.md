# Meshin yksinkertaistus

3D-malli on usein mesh-muodossa. Mesh on tarkemmin sanottuna <em>polygoniverkko</em>, joka koostuu useista toisiinsa kiinnittyneistä monikulmioista. Kyseessä on siis eri asia kuin pistepilvi. Siinä missä pistepilviä voidaan värjätä, voidaan polygoniverkkoja joko värjätä polygoni kerrallaan, tai sitten kietoa verkko <em>tekstuuriin</em>. 
Fotogrammetrisesti tehdyissä malleissa saattaa olla usein liikaakin polygoneja. Polygonien suuri määrä voi periaatteessa tarkoittaa myös suurempaa tarkkuutta ja yksityiskohtien erottelua, mutta näin ei aina ole -- esimerkiksi huonolaatuisista valokuvista tehty malli pysyy epätarkkana, vaikka ohjelman asetuksissa lisättäisiin polygonien määrää. Näin ollen on usein järkevää yksinkertaistaa mallia. Kun meshiä yksinkertaistaa, pienenee sen tiedostokoko samalla huomattavasti, jolloin sitä on helpompi käsitellä. Tässä ohjeessa esitellään yksinkertainen keino tehdä se ilmaisella [Meshlabilla](https://www.meshlab.net/). Kannattaa kuitenkin selvittää myös, onko mallin tuottamiseen käytetyssä ohjelmassa työkalua yksinkertaistukseen; esimerkiksi RealityCapturen Simplify toimii hyvin.

## Meshlab ja tiedoston tuonti

Meshlab on helppokäyttöinen yleisohjelmisto polygoniverkkojen käsittelyyn. Se on avoin, ilmainen ja toimii niin Windowsilla, Linuxilla kuin Macillakin. Meshlabissa on todella paljon ominaisuuksia -- oikeastaan niin paljon, että välillä on vaikea löytää sitä, mitä etsii. 

Lisätään yksinkertaistettava aineisto (File->Import mesh, tai vaihtoehtoisesti Ctrl+I). Oheinen teksturoitu polygoniverkko on tehty fotogrammetrisesti eräästä roomalaisesta cubiculumista ja leikattu sopivan kokoiseksi CloudComparessa. Tiedosto on kuitenkin yhä liian iso esimerkiksi SketchFabiin ladattavaksi. 

![Kuva 1: Seinä tekstuureilla.](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/Meshin_yksinkertaistus/Kuva1.png?raw=true)

Koska tässä tapauksessa olemme lähinnä kiinnostuneet seinämaalauksista ja seinien mittasuhteista, ei verkon tarvitse olla niin tiheä -- tärkeintä on, että tekstuuri on hyvälaatuinen. Esimerkiksi tasaisten pintojen kuvaamiseen ei tarvita niin paljon polygoneja, kuin mitä tässä mallissa.  Saamme tekstuurit pois päältä painamalla oikealla paneelissa olevan valinnan Texture Coord Off.

![Kuva 2: Seinä ilman tekstuureja.](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/Meshin_yksinkertaistus/Kuva2.png?raw=true)

Kun aktivoimme verkon reunat näkyviin näemme hyvin, että polygoneja on aivan liikaa:

![Kuva 3: Lähikuva seinästä.](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/Meshin_yksinkertaistus/Kuva3.png?raw=true)

## Yksinkertaistus

Polygonien määrää voidaan vähentää muutamalla eri keinolla. Tässä käytetään työkalua nimeltä Quadric Edge Collapse Decimation, jonka taustalla on Michael Garlandin ja Paul Heckbertin [tutkimus](http://mgarland.org/files/papers/quadrics.pdf). Se löytyy valikosta Filters->Remeshing, Simplification and Reconstruction->Simplification: Quadric Edge Collapse Decimation (with texture). On tärkeä valita tämä versio, jotta tekstuurien asemointi säilyy oikein. Erilaiset menetelmät, joiden nimessä on decimation, perustuvat joka n:nnen vektorin tai pisteen säilyttämiseen verkossa.[^1]

![Kuva 4: Desimoinnin asetukset.](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/Meshin_yksinkertaistus/Kuva4.png?raw=true)

Muutama sana asetuksista. Target number of faces on siis tavoitteena olevien polygonien määrä, joka ainakin omassa Meshlabin versiossani näyttäisi olevan vakiona puolet aloitusmallin polygoneista (näkyy alapalkin tiedoissa kohdassa Faces). Quality threshold on luku 0 ja 1 väliltä. 1 yrittää säilyttää mahdollisimman hyvin alkuperäisen muodon, kun taas 0 ei välitä siitä. Samaten Preserve Boundary of the mesh kannattaa valita: silloin algoritmi säilyttää verkon rajat ennallaan. Kun asetukset on valittu, voidaan painaa Apply ja yksinkertaistus alkaa. 

Kun laitamme tekstuurit takaisin päälle, näemme, että lopputulos ei näytä äkkiseltään lainkaan erilaiselta. Polygonien määrä on kuitenkin puolittunut. Muoto on säilynyt ennallaan ja malli näyttää kaikin puolin oikealta, mutta on huomattavasti pienempi kuin aiemmin.

![Kuva 5: Lopputulos tekstuurien kanssa.](https://github.com/nikolaipaukkonen/AvoinArkeologi/blob/main/Meshin_yksinkertaistus/Kuva5.png?raw=true)

Kunhan tekstuurien laatu on hyvä, voi hyvinkin rajulla yksinkertaistuksella saada kelvollista jälkeä esimerkiksi visualisointeja varten. 
 
[^1]: Decimation-sanan taustalla on latinan <em>decimatio</em>. Kirjaimellisesti se tarkoittaa joka kymmenennen ottamista -- Rooman legioonien kurinpitojärjestelmässä tunnettiin nimittäin rangaistus, jossa jokainen kohortti jaettiin kymmenen miehen ryhmiin. Jokaisen ryhmän piti sitten surmata joukostaan yksi, joka valittiin arvalla (esm. Liv. 2.59; Suet. <em>Aug.</em> 25). 
