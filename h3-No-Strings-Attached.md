# h3 No Strings Attached

## a) Strings. Lataa ezbin-challenges.zip Aja 'passtr'. Selvitä oikea salasana 'strings' avulla. Selvitä myös lippu. 

Aloitin lataamalla ezbin-challenges.zip

    wget https://terokarvinen.com/loota/yctjx7/ezbin-challenges.zip

Sitten

    unzip ezbin-challenges.zip

Sain tiedoston auki, jonka jälkeen piti avata tiedosto käyttämällä strings. 

<img width="695" height="523" alt="image" src="https://github.com/user-attachments/assets/f96b7faa-1431-4a65-aec0-cd9c0148555f" />

Tässä kohtaa sain näkyviin salasanan (oletetusti) mutta halusin nähdä sen hieman siistimmällä tavalla ilman kaikkea muuta tekstiä. Kokeilin mm. -d ja -n5, mutta tulos ei ollut paras mahdollinen.

Yritin hakea sanaa password käyttämällä grep: 

<img width="716" height="68" alt="image" src="https://github.com/user-attachments/assets/399d7597-537c-46b7-9bd6-7a465806f04d" />

Sain tulokseksi sanan 'password' sisältävät rivit, mutta en itse salasanaa. Joten luin sitten ```man grep

Sieltä löysin komennon -A, joka näyttää seuraavia rivejä. Joten lisäsin grep -A1 password:

<img width="785" height="111" alt="image" src="https://github.com/user-attachments/assets/c7bc6257-f1ca-4145-8a10-b3d7560f3e79" />

## b) Tee passtr.c -ohjelmasta uusi versio, jossa salasana ei näy suoraan sellaisenaan binääristä. Osoita testillä, että salasana ei näy. (Obfuskointi riittää.)

Avasin passtr.c ja tutkin tiedostoa hetken aikaa. Yritin myös googlettaa "C++ obfuscation" mutta en löytänyt pienen etsinnän jälkeen mitään, mikä auttaisi minun taitotasollani olevaa eteenpäin.

Joten annoin ChatGPT:lle tehtävänannon ja kuvan passtr.c -tiedostosta, jota lähdin muokkaamaan ohjeiden mukaan. 

Unohdin ottaa kuvan alkuperäisestä tiedostosta, mutta tässä on tulos muokkaamisen jälkeen:

<img width="948" height="694" alt="image" src="https://github.com/user-attachments/assets/4c3ec0ac-5c71-4d32-a35d-c226bd71e5bc" />

Tämän jälkeen ajoin tekoälyn ohjeiden mukaan gcc passtr.c -o passtr ja sitten strings passtr:

<img width="718" height="203" alt="image" src="https://github.com/user-attachments/assets/edee1d0c-0940-4b88-97e4-1188eb200735" />

Välistä oli hävinnyt aikaisemmin näkynyt salasana.

Tein jossain kuitenkin virheen, sillä ajamalla ./passtr ja syöttämällä sala-hakkeri-321 vastaus on Sorry, no bonus. En kokeillut ajaa tätä aluksi, mutta oletan että sen pitäisi toimia.

## c) Packd. Aja 'packd' paketista ezbin-challenges.zip. Mikä on salasana? Mikä on lippu?

Kokeilin ensimmäiseksi avata strings packd, ihan vain nähdäkseni miltä se näyttää. Arvatenkin salasanan löytäminen ei ollut näin yksinkertaista.

<img width="394" height="238" alt="image" src="https://github.com/user-attachments/assets/d775c833-9d14-4a74-82b4-c7c54efc28be" />

Katsoin ensimmäiset vinkit, ja yhdistin heti nähneeni kirjaimet upx myös tutkiessani tiedostoa aikaisemmin. Pienen taistelun jälkeen sain lopulta ladattua upx omalle koneelleni ja tekoälyltä kysyttyäni sain myös .tar paketin auki.

Kun tämä oli meneillään, olin löytänyt [videon](https://www.youtube.com/watch?v=0jVikfySiII) jossa käytiin läpi upx decompress. Nähtyäni komennon -d loppu menikin suht helposti.

    upx -d ./challenges/packd/packd

  Ja 

    strings ./challenges/packd/packd

  Sieltä näin salasanan ja sitten pääsinkin syöttämään salasanan:

<img width="694" height="89" alt="image" src="https://github.com/user-attachments/assets/799d5e2d-bc61-4d07-a833-eaba3bfb7ec5" />

## Lähteet

Tehtävänanto ja kurssisivu. https://terokarvinen.com/sovellusten-hakkerointi/#h3-no-strings-attached-tero 

John Hammond. Unpacking UPX Binaries. Katsottavissa: https://www.youtube.com/watch?v=0jVikfySiII Katsottu 4.9.2025.

ChatGPT. Prompt: Tee passtr.c -ohjelmasta uusi versio, jossa salasana ei näy suoraan sellaisenaan binääristä. Osoita testillä, että salasana ei näy. (Obfuskointi riittää.) + kuva passtr.c tiedostosta.











