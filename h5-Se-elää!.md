# h5 Se elää!

Tämän viikon tehtävissä käytetään GNU Debuggeria. En ymmärtänyt tunnilla käytännössä mitään, enkä materiaalien lukemisen jälkeen ole yhtään viisaampi. Tämän takia näissä tehtävissä on kysytty apua tekoälyltä.

## a) Lab1

Aloitin tämänlaisilla komennoilla, jotta saan ohjelman käyntiin ja pääsen tutkimaan ohjelmaa.

<img width="822" height="690" alt="image" src="https://github.com/user-attachments/assets/2e820a59-1941-47e9-85d6-c605a37bddd1" />

Ymmärsin, että tässä kohtaa tulee virhe.

<img width="738" height="48" alt="image" src="https://github.com/user-attachments/assets/db809a51-e80e-4c7b-9ed7-85a206c27b57" />

Joten asetin breakpointin ennen tätä kohtaa.

<img width="443" height="99" alt="image" src="https://github.com/user-attachments/assets/9089f878-440a-4280-ad85-2bc1b43105f6" />

Tekoälyn avulla korjasin koodin poistamaan virheen, ja se näytti tältä. Tässä poistettiin print_scrambled(bad_message) ja lisättiin loppuun if-lauseke.

<img width="430" height="554" alt="image" src="https://github.com/user-attachments/assets/da4f34b8-b1df-4d98-afe9-f0ef5991f5d0" />

Lopulta ohjelma toimi niin kuin pitikin, eli tulostaa Hello, World! +3 kohtaa ASCII-merkeistä.

<img width="735" height="133" alt="image" src="https://github.com/user-attachments/assets/4d59b11a-1f73-4433-a50b-75b17530cdfb" />

## Lab2

Tässä harjoituksessa piti ajaa ohjelma ./passtr, joka kysyy käyttäjältä salasanaa. Väärästä salasanasta tulee "Sorry, no bonus."

Lähdin README.md tiedoston ohjeiden mukaan avaamaan tiedoston microlla, ja tiedostossa luki salasana selvästi.

Tämä salasana toimi passtr ohjelmassa, mutta ei passtr2o.

Makefile tiedoston ohjeiden ajamisen jälkeen avasin passtr2o gdb:llä, ja ohjelma kysyi salasanaa. 

Pääsin tekoälyn avulla tarkastelemaan main:n koostumusta disassemble-komennolla, mutta tämän jälkeen selitykset menivät täysin yli minulta. En osannut jatkaa tästä eteenpäin. Raporttiakin on kovin vaikea kirjoittaa kun ei ymmärrä mitä tapahtuu.

<img width="810" height="610" alt="image" src="https://github.com/user-attachments/assets/1cdcec5d-378a-444c-b19a-66aae433618e" />

## Lab3

Kohdassa c tehtävänä on crackme 03 ja 04. Sain vastauksen 03 käyttämällä less crackme03.c, joka ei varmaan ollut haettu tapa.

<img width="896" height="47" alt="image" src="https://github.com/user-attachments/assets/b42ab6f6-d6fd-48e7-a8ee-e9ff63cae509" />

Kokeilin myös debuggerin avulla löytää jotain tapaa mistä saisin oikean salasanan, mutta yritykseni ei johtanut mihinkään.

04 avasin samalla tavalla käyttämällä less crackme04.c, ja alussa luki, että ohjelma hyväksyy salasanan joka on 16 merkkiä pitkä ja ASCII summa on 1652. Toisaalta seuraavalla rivillä luki 16 * 110 +2, josta tulee 1762.

Kokeilin ASCII-laskimella ensin 1652, sitten 1762 joka oli oikein.

<img width="907" height="75" alt="image" src="https://github.com/user-attachments/assets/a2866515-b9d6-4790-a6bd-aa1cc02d68dd" />

Tässäkin olisi varmaan ollut jotain käyttöä debuggerilla, mutta en osaa käyttää sitä riittävän hyvin.

## Lähteet

Kurssisivu ja tehtävänanto: https://terokarvinen.com/sovellusten-hakkerointi/#h5-se-elaa-lari

ChatGPT.

ASCII Calculator. https://opendsa-server.cs.vt.edu/embed/StringSimple
