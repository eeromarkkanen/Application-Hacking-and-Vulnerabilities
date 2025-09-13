# h4 Kääntöpaikka

## x) Lue/katso/kuuntele ja tiivistä

Videolla on PicoCTF tehtävä reverse engineering

- Ensin Hammond kokeilee ratkaista tehtävää "What's my favorite number?" komentorivillä käyttämättä Ghidraa siinä onnistumatta
- Sen jälkeen hän asentaa Ghidran ja neuvoo käytössä
- Tämän jälkeen hän alkaa tutkimaan tiedostoa ja löytää heksadesimaalin koodista
- Lopulta hän kääntää numeron pythonilla desimaaliksi ja ratkaisee tehtävän

## a) Asenna Ghidra.

Ghidra asennettu Kaliin tunnilla komennolla sudo apt-get install ghidra.

## b) rever-C. Käänteismallinna packd-binääri C-kielelle Ghidralla

Latasin Teron sivuilta ezbin-challenges.zip ja sen jälkeen tiedostolle komento unzip. Avasin Ghidran ja loin uuden projektin, jossa tämä packd-tehtävä suoritetaan.

Minulla oli tunnilla sama ongelma kuin nyt, eli ensimmäisellä kerralla kun avaan tiedoston, CodeBrowser aukeaa tyhjänä kun yritän suorittaa sen Ghidralla. Apu on ihan vain sulkea CodeBrowser ja sen jälkeen kokeilla uudestaa, jolloin Ghidra lähtee analysoimaan tiedoston. (Tämä alkoin myöhemmin toimia, kun tuplaklikkasin tiedoston auki, enkä käyttänyt 'lohikäärme' nappia.)

Lähdin etsimään oikeaa funktiota vasemman puolen valikon Symbol Tree:stä. Avasin sieltä löytyvät funktiot, ja päättelin yhden niistä olevan main-funktio, jota ohjelma käyttää.

<img width="1404" height="677" alt="image" src="https://github.com/user-attachments/assets/3ce2534d-e736-4789-9cdd-246ce97f8445" />

Päättelin korostetun kohdan olevan salasana, jota koodi vertaa oikeaan arvoon ja sen jälkeen suorittaa alla olevat funktiot. Tässä kohtaa yritin samaa kikkaa kuin aluksi katsotulla [videolla](https://www.youtube.com/watch?v=oTD_ki86c9I) eli pythonilla avata tätä kohtaa. Tämä palautti vain numerosarjan.

<img width="575" height="99" alt="image" src="https://github.com/user-attachments/assets/9256ee01-cb58-4024-b1ab-24bf245b341c" />

Klikkasin oikeaa kohtaa ja yritin listings-kohdasta muokata 0x106399 tyyppiä, mutta mikään ei tuottanut tulosta.

Turhauduin hieman tässä kohtaa ja kyselin apua tekoälyltäkin, se ei kuitenkaan osannut neuvoa mitään hyödyllistä.

Tässä kohtaa purin ohjelman niin kuin edellisellä viikolla upx -d packd ja avasin Ghidralla uudestaan, ihan vain tarkistaakseni että etsin oikeaa kohtaa. Tässä näkyy, että salasana "piilos-AnAnAs" on täysin sama kohta, jota yritin jo aikaisemmin selvittää.

<img width="1408" height="680" alt="image" src="https://github.com/user-attachments/assets/74462689-43c9-4ff3-9cce-70bed4714399" />

## c) Jos väärinpäin

Testasin ensimmäisenä, että ohjelma toimii niin kuin pitääkin. Etsin salasanan strings passtr komennolla, jossa se oli suojaamattomana.

<img width="575" height="93" alt="image" src="https://github.com/user-attachments/assets/da699ddf-c179-48aa-aabb-192c4cbbbda0" />

Sen jälkeen avasin Ghidran ja loin uuden projektin tälle tehtävälle. Etsin koodista tunnilla näytetyn JNZ kohdan ja muutin sen JZ. [Lähde](https://materials.rangeforce.com/tutorial/2020/04/12/Patching-Binaries/)

<img width="569" height="208" alt="image" src="https://github.com/user-attachments/assets/c6f0c331-62a5-4b46-a827-4c96d5e0472a" />

Sitten piti valita valikosta Export program, ja tallensin sen original file - muodossa samaan kansioon kuin alkuperäinen passtr nimellä passtrbroken. Lisäsin oikeudet ajaa ohjelma ja sitten kokeilin väärällä salasanalla ja oikealla salasanalla, ja tässä on lopputulos.

<img width="634" height="236" alt="image" src="https://github.com/user-attachments/assets/f1706e2a-07f0-44b2-b0ed-87a8bc462856" />

## d) Nora CrackMe

Kloonasin repositorion Kaliin ja käänsin binäärit gcc -o crackme01 crackme01.c jne komennoilla.

## e) Nora crackme01 

Ajoin ohjelman ./crackme01 ja tuloksena oli:

<img width="284" height="63" alt="image" src="https://github.com/user-attachments/assets/609d7442-ab71-43b2-baef-1c5a9005574a" />

Avasin ohjelman Ghidralla ja main:sta löytyi kohta __n = strlen("password1"); joten kokeilin lisätä sen.

<img width="279" height="60" alt="image" src="https://github.com/user-attachments/assets/0e96e00c-2a3c-40a0-a3a6-846f41b37824" />

Muilla merkkijonoilla tuloksena oli "No, *anything* is not correct."

## f) Nora crackme01e

Tämä ohjelma tulosti saman "Need exactly one argument." ja kokeilin samaa password1, mutta se ei tietenkään ollut oikein. Joten Ghidra auki ja tutkimaan.

Ohjelmasta näytti samalta kuin ensimmäinen, mutta eri salasanalla. Kokeilin ajaa salanan slm!paas.k:

<img width="276" height="58" alt="image" src="https://github.com/user-attachments/assets/c9307c61-446c-4277-9cef-5fe276291b19" />

Tästä tuloksesta päättelin, että "!" tekee jotain salasanalle. Mietinkin, pystyykö salasanan jotenkin "eristämään," jotta huutomerkki ei vaikuttaisi syötteeseen.

Kokeilin "slm!paas.k" mutta tulos oli sama kuin aikaisemmin. Sitten korvasin lainausmerkit ' ja tämä tuottikin tulosta.

<img width="278" height="122" alt="image" src="https://github.com/user-attachments/assets/be7d27e4-3cf0-4ca7-a056-a9e3d64e3e32" />

## g) Nora crackme02

Jälleen tähänkin ohjelmaan vaaditaan 1 argumentti, mutta password1 ei tuottanut tulosta. Ohjelma auki Ghidralla ja tutkimaan. 

<img width="725" height="470" alt="image" src="https://github.com/user-attachments/assets/6ac3ff19-296a-4022-995d-c0a5cb3d8daf" />

Tuijotettuani ohjelmaa hetken muutin local_c muuttujan nimen i:ksi, koska sen olen tottunut näkemään for-loopissa. Jouduin kysymään tekoälyltä, mitä mikäkin osa tässä loopissa tarkoittaa, ja sain vastaukseksi, että ohjelma käy läpi jokaisen käyttäjän antaman merkin yksitellen.

Taas lisää mietittyäni kiinnitin huomion "password[i]" + -1 kohtaan, joka vaikutti mielestäni epänormaalilta. En kuitenkaan ymmärtänyt mihin tämä johtaisi, ja jouduin tästäkin kysymään tekoälyltä apua, ja se vahvisti, että ohjelma käy merkkijonoa läpi edelliseltä paikalta, eli p -> o jne.

Joten lähdin kokeilemaan salasanaa, jossa vähensin password1 kaikista yhden. Aluksi kokeilin ozrrvnqc0, mutta se ei ollut oikein. Jälleen kerran kysyin apua tekoälyltä, joka ohjasi minut oikeiden merkkien pariin. (a ei ollutkaan z, vaan `)

Sekään merkkijono ei ihan heti toiminut, vaan jouduin kikkailemaan \ kanssa, jotta ohjelma ei lukisi ` merkkiä.

<img width="295" height="393" alt="image" src="https://github.com/user-attachments/assets/bdf9c43e-8522-4c83-8fe3-0657a3672c41" />

## Lähteet

Kurssisivu ja tehtävänanto. Luettavissa https://terokarvinen.com/sovellusten-hakkerointi/#h4-kaantopaikka-tero Luettu 13.9.2025

RangeForce. Patching Binaries With Ghidra. Luettavissa https://materials.rangeforce.com/tutorial/2020/04/12/Patching-Binaries/ Luettu 13.9.2025.

John Hammond. GHIDRA for Reverse Engineering. Katsottavissa https://www.youtube.com/watch?v=oTD_ki86c9I Katsottu 13.9.2025.

ChatGPT. chat.openai.com







