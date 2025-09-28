# h6) Sulaa hulluutta

## a) Lab 0

Yritin tutkia h1.jpg ominaisuuksia, mutta en nähnyt mitään tavallisesta poikkeavaa. Tutkin muutamaa muuta kuvaa omalta koneeltani, ja huomasin että kuvan koko on huomattavasti isompi kuin muutamissa kuvissa mitä tarkastelin. (840kt ja ~<140kt)

Sitten mietin, millä jo opitulla työkalulla voisin yrittää löytää jotakin. Kokeilin tässä kohtaa ainoastaan strings-komentoa, mutta se ei palauttanut mitään järkevää.

## b) Lab 1

Tässä kohtaa kuvaa oli tarkoitus tutkia binwalk-ohjelmalla. Komento binwalk antaa vaihtoehtoja mitä ohjelmalla voi tehdä. 

<img width="1387" height="724" alt="image" src="https://github.com/user-attachments/assets/77babc39-3de8-41f1-8a22-5be760c816ad" />

Komento binwalk h1.jpg antoi seuraavan tuloksen:

<img width="1567" height="453" alt="image" src="https://github.com/user-attachments/assets/75874aa9-3e24-42ff-8ae7-95565e69b4fc" />

Kuvasta näkee, että h1.jpg sisällä on jonkinlaisia dokumentteja. Joten lisäsin alkuperäiseen komentoon -e (--extract), jolla sain tallennettua tiedostot.

Puretuista tiedostoista löytyi seuraavaa. Näistä minua kiinnosti kansio word, josta löytyi erilaisia dokumentteja. Avasin tiedoston document.xml, ja sieltä löytyikin aikamoinen sekamelska. (toinen screenshot)

<img width="1002" height="110" alt="image" src="https://github.com/user-attachments/assets/cf0988da-9e32-4d7a-aed1-507b93dc6e97" />

<img width="1899" height="788" alt="image" src="https://github.com/user-attachments/assets/df36f449-d5a9-4728-8880-7322bb22597e" />

Seassa näkyy kuitenkin selkeitä lauseita, ja halusin nähdä voinko jollakin tapaa saada pelkästään tuon tekstin näkyviin. Tässä kohtaa kysyin apua tekoälyltä, koska en itse osannut/jaksanut selvittää sellaista komentoa.

Sain tulokseksi tämännäköisen komennon: grep -oP '(?<=<w:t>).*?(?=</w:t>)' document.xml

grep: etsii tiedostosta

-oP: -o etsii only matching ja -P on Perl-yhteensopiva. Se mahdollistaa lookbehind ja lookahead, joita tavallinen grep ei tue. (ChatGPT)

'(?<=<w:t>).*?(?=</w:t>)': palauttaa kaiken kyseisten tägien välistä, mutta ei tägejä itseään

document.xml: dokumentti, josta etsitään

Tuloksena tällaista:

<img width="1449" height="806" alt="image" src="https://github.com/user-attachments/assets/a447ce0e-3443-4e54-adcf-a008fc40b4b1" />

* Huomio: tein tämän aikaisemmin kirjoittamatta raporttia, ja olen jotenkin tallentanut tiedoston uudelleen nimellä extracted_text.txt. En löydä tätä komentoa nyt mistään.

## c) Lab 2. FOSS (Free Android OpenSource) Tutustu listaan eri android applikaatioita. Valitse listalla itsellesi mielenkiintoisin applikaatio ja mene sen GitHubiin. Lataa ohjelman APK itsellesi ja käytä seuraavia työkaluja tutustuaksesi miten APK:n voi avata. 
ZIP, JADX ( https://github.com/skylot/jadx ), Bytecode-viewer ( https://github.com/Konloch/bytecode-viewer/ )

Tehtävänä oli tutustua listaan eri applikaatioita ja valita sieltä joku. Valitsin applikaation nimeltä FlashDim, jonka APK:n latasin virtuaalikoneelle.

Seuraavaksi piti ladata JADX, jonka asensin [sivujen](https://github.com/skylot/jadx) ohjeiden mukaan:

    git clone https://github.com/skylot/jadx.git
    cd jadx
    ./gradlew dist

Halusin avata jadx:n GUI:n joten etsin sen komentoriviltä ja käynnistin. Sitten valitsin tiedoston FlashDim-2.4.3.apk ja avasin sen.

<img width="280" height="129" alt="image" src="https://github.com/user-attachments/assets/3672058d-50c2-4d2f-a30c-47af9fcd9e70" />

Availin eri kansioita ja tiedostoja, mutta en kiinnittänyt mihinkään erityisemmin huomiota. Paljon erilaista koodia sieltä löytyi.

<img width="1339" height="622" alt="image" src="https://github.com/user-attachments/assets/db20cdc7-511f-4192-bbb4-ad8ef3961fcd" />

## Lähteet

Kurssisivu ja tehtävänanto: https://terokarvinen.com/sovellusten-hakkerointi/#h6-sulaa-hulluutta-lari

ChatGPT. chat.openai.com

Free Android Open Source. https://github.com/offa/android-foss

Jadx. https://github.com/skylot/jadx
