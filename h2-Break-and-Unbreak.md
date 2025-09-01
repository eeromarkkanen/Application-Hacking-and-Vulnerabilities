# h2) Break and Unbreak

## x) Lue/katso/kuuntele ja tiivistä.

### OWASP Top 10: A01 Broken Access Control

- Sivulla kerrotaan OWASP:n yleisimmästä ohjelmiston turvallisuusuhasta Broken Access Controlista. 
- Käytännössä tämä tarkoittaa, että käyttäjä pystyy katselemaan, muokkaamaan tai jopa tuhoamaan tietoja tai tiedostoja, joihin hänellä ei ole käyttöoikeuksia.
- Seuraavaksi annetaan esimerkkejä, millä tavoilla tämä tapahtuu, kuten URL:n muokkaus tai käyttöoikeuksien korotus.
- Miten estää tällaisia hyökkäyksiä.
- Ja lopuksi esimerkkihyökkäyksiä.

  (OWASP)

### Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf

- Tällä sivulla on ohjeet ffuf:n käyttöön (Fuzz Faster U Fool)
- Sitä voidaan käyttää hakemistorakenteiden ja tiedostojen löytämiseen
- Tai alidomainien ja piilotettujen verkkosivujen etsintään
- Lopuksi ohjeet esimerkkimaalin lataukseen ja fuzzaamiseen

  (Karvinen, 2023)

### PortSwigger: Access control vulnerabilities and privilege escalation

- Sivulla kerrotaan Access Controlin heikkouksista, käyttöoikeuksien korotuksesta ja miten estää nämä
- Access control käyttää todennusta, jolla varmistetaan että käyttäjä on kuka hän sanoo olevansa. Session valvonnalla pidetään kirjaa, mitä HTTP pyyntöjä käyttäjä tekee ja lopuksi kulunvalvonta (Access Control) päättää, onko käyttäjällä oikeus suorittaa kyseiset toimenpiteet.
- Seuraavaksi sivulla puhutaan vertikaalisesta, horisontaalisesta ja kontekstista riippuvasta kulunvalvonnasta. Vertikaalinen esim user -> admin eli käyttäjä saa korkeampia oikeuksia kuin hänellä pitäisi olla. Horisontaalisesta annetaan esimerkkinä pankkisovellus, jossa käyttäjillä on samat oikeudet, mutta ainoastaan omalla pankkitilillään.
- Kontekstista riippuvaiset kulunvalvonnat varmistavat, että käyttäjä tekee toimintonsa oikeassa järjestyksessä ja estää väärän järjestyksen hyväksikäyttämisen. Esim. ostoskorin muokkamisen verkkokaupassa maksun jälkeen
- Lopuksi paljon erilaisia esimerkkejä hajonneesta kulunvalvonnasta labratehtävien kanssa

- (PortSwigger)

### Karvinen 2006: Raportin kirjoittaminen

- Tällä sivulla on ohjeet hyvän raportin kirjoittamiseen. Millainen raportin pitää olla ja mitä se ei saa olla
- Hyvä raportti on toistettava, täsmällinen, helppolukuinen ja viittaa lähteisiin
- Raportissa ei saa sepittää, plagioida tai käyttää kuvia luvatta

  (Karvinen, 2006)

# a) Murtaudu 010-staff-only

Latasin ja asensin harjoituksen ohjeiden mukaan. ([Lähde](https://terokarvinen.com/hack-n-fix/)

Kokeilin syöttää eri numeroita, ja tämän jälkeen kirjaimia. Kirjaimia syöttäessä sivu kuitenkin antoi virheen, mutta lähdekoodista pystyi ottamaan pois "number" kentän, jolloin syötettä pystyi muokkaamaan.

<img width="1286" height="846" alt="image" src="https://github.com/user-attachments/assets/0b95e33d-ac43-49eb-9b49-32ed2852b6f0" />

En kuitenkaan ymmärtänyt asiasta kovin paljoa, joten avasin vinkit käyttööni. Edelleen olin aika pihalla asiasta, enkä päässyt eteenpäin joten käytin tässä apuna ChatGPT.

Sieltä sain lopulta neuvot, jossa pääsin muokkaamaan Network-välilehdeltä bodya muotoon pin=123' OR 1=1-- .

Tämä palautti salasanaksi foo.

<img width="374" height="529" alt="image" src="https://github.com/user-attachments/assets/5f5f26ba-f25d-4625-8730-095405401ae9" />

Tämän jälkeen luin vinkeistä, että pitäisi käyttää LIMIT-komentoa etsimään oikea salasana. Lisäsin kyselyn perään LIMIT 2,1 ja tuloksena oli tämä:

<img width="377" height="580" alt="image" src="https://github.com/user-attachments/assets/49afefe5-e223-44b7-a78d-bffeeafcc66c" />

## b) Korjaa 010-staff-only haavoittuvuus lähdekoodista. Osoita testillä, että ratkaisusi toimii.

Muokkasin staff-only.py nanossa näyttämään seuraavalta. [Lähde](https://github.com/kreatiini/Sovellusten-hakkerointi-ja-haavoittuvuudet24/blob/main/h2%20Break%20%26%20Unbreak.md)

<img width="644" height="156" alt="image" src="https://github.com/user-attachments/assets/fe7f9c2f-a9e5-452a-8406-d2428435918f" />

Kokeilin sen jälkeen samaa syötettä ja tuloksena oli (not found)

<img width="755" height="702" alt="image" src="https://github.com/user-attachments/assets/ce1cafa4-988c-4aaf-abd3-55250764016d" />

## c) Ratkaise dirfuzt-1 artikkelista Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf.

Asensin ffuf ohjeiden mukaan ja latasin muutkin tiedostot. Sitten oli aika kokeilla ffuf käyttöä.

    ffuf -w common.txt -u http://127.0.0.2:8000/FUZZ

Tämä palautti todella monta tulosta, joten rajataan hieman lisäämällä -fs 132. joka rajaa koon 132 sivut pois.

<img width="931" height="596" alt="image" src="https://github.com/user-attachments/assets/e74ce988-6c3c-4594-8cd7-361386190ce7" />

Sitten avasin 127.0.0.2:8000/admin

<img width="568" height="230" alt="image" src="https://github.com/user-attachments/assets/b9d840ac-abce-4c4f-b763-b7796171ab61" />

## d) Murtaudu 020-your-eyes-only

Asensin paketit ohjeiden mukaan ja ajoin

    ffuf -w common.txt -u http://127.0.0.1:8000

Tämä palautti ainoastaan admin-console sivun. Menin sivulle ja se pyysi kirjautumaan sisään. Loin tunnuksen ja palasin sivulle kirjautumaan sisään, ja tulos on tässä:

<img width="819" height="473" alt="image" src="https://github.com/user-attachments/assets/72d1e904-3193-4f31-a83b-cb4683948fae" />

## e) Korjaa 020-your-eyes-only haavoittuvuus. Osoita testillä, että ratkaisusi toimii.

Tässä kohtaa en tiennyt yhtään, mistä korjaus pitäisi aloittaa. Tässä kohtaa käytin annettua [walkthrough](https://askdatdude.github.io/diary/entries/diary.html?entry=SH24-002&week=)
ja muokkasin hats/views.py tiedostoa sen mukaan. 

<img width="926" height="507" alt="image" src="https://github.com/user-attachments/assets/810f998c-1fcd-4d99-ba8d-3e816e249c8d" />

Käynnistin serverin uudelleen ja nyt tuloksena oli 403 Forbidden.

<img width="776" height="254" alt="image" src="https://github.com/user-attachments/assets/e76b1aaf-8fc5-4cc3-a9a6-622bfd9732fa" />


## Lähteet

OWASP. A01 Broken Access Control. Luettavissa: https://owasp.org/Top10/A01_2021-Broken_Access_Control/ Luettu 29.8.2025

Terokarvinen.com. Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf. Luettavissa https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/ Luettu 29.8.2025

PortSwigger. PortSwigger: Access control vulnerabilities and privilege escalation Luettavissa: https://portswigger.net/web-security/access-control Luettu 29.8.2025

Terokarvinen.com. Karvinen 2006: Raportin kirjoittaminen. Luettavissa: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/ Luettu 29.8.2025

ChatGPT. Network-välilehden käyttö ja SQL-injektio. https://chat.openai.com

GitHub. https://github.com/kreatiini/Sovellusten-hakkerointi-ja-haavoittuvuudet24/blob/main/h2%20Break%20%26%20Unbreak.md

Walkthrough. https://askdatdude.github.io/diary/entries/diary.html?entry=SH24-002&week=





