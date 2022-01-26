# Home Assistant Migration Plan (+ Voice Assistant)

Projektin tarkoituksena on päivittää henkilökohtainen Home Assistant -instanssini konttiin ja muuntaa nykyinen järjestelmä IaC:n avulla täysin(tai mahdollisimman) deklaratiiviseksi.

## Nykyinen tilanne:
Lähes kaikki älykotiin liittyvät palvelut pyörivät CentOS 7 -virtuaalikoneella. Koneella on käyttäjä homeassistant ja suurin osa ohjelmista pyörii systemd palveluina ja binäärit sekä konfiguraatio sijaitsee polussa /home/homeassistant/. Home Assistant on tällä hetkellä docker-kontissa ja konfiguraatio sijaitsee sijainnissa /home/homeassistant/.homeassistant joka on liitetty konttiin. 

## Toivottu lopputulos:
Olisi hyvä että kaikki palvelut siirrettäisiin kontteihin helpompaa ylläpitoa ja toimivuutta varten. Suurin osa ohjelmistosta on jo saatavilla kontteina, puuttuvat ohjelmistot olisi hyvä kontittaa itse. Palvelimena otan käyttöön Ubuntu 20.04 LTS sillä olen jo automatisoinut kyseisen käyttöjärjestelmän provisioinnin.

## Suunnitelma vaiheista:

### Palveluiden kartoitus
Home Assistant -järjestelmäni on riippuvainen useasta erillisestä palvelusta kuten Mosquitto Broker, Node-Red sekä Zigbee2MQTT. Näiden palveluiden inventointi ja konfiguraatioiden löytäminen olisi ensisijainen tehtävä.

### Konttien saatavuuden selvitys ja puutteiden tunkkaaminen
Kun palvelut on kartoitettu, on aika selvittää mistä ohjelmistoista ylläpidetään jo konttikuvia. Mikäli tarjonnassa on puutetta, koitetaan halutut ohjelmistot kontittamaan omin toimin. Mikäli tämä osoittautuu mahdottomaksi, harkitaan ohjelmiston asentamista “perinteisesti”.

### Konttien konfigurointi sekä docker-compose
Palvelut keskustelevat keskenään varsin paljon ja hyvän virtuaaliverkon pystyttäminen on siksi tärkeätä. Liikenteen ajaminen hostin läpi on turhan tökeröä. Orkestrointiin on hyvä käyttää docker-composea jolla voidaan konttien väliset yhteydet ja konfiguraatiot määrittää deklaratiivisesti.

### Dockerin sekä docker-composen asennus palvelimelle Ansiblella
Kun meillä on toimiva järjestelmä dockerin avulla, kirjoitetaan Ansiblella playbook joka asentaa dockerin, docker-compose projektin sekä käynnistää sen. 

### Powerpoint presentaation sekä dokumentaation väsääminen
Esittelyä varten olisi hyvä tehdä powerpoint joka käsittelee tässä dokumentissa kuvattuja asioita sekä myös näyttää miten prosessi sujui. Koska projekti tullaan julkaisemaan vapaalla lisenssillä(Todennäköisesti MIT tai GPLv3), olisi kiva tehdä projektista mahdollisimman helposti lähestyttävä. Dokumentaatioksi tulee ainakin git README, ehkä jopa pieni wiki.

## Suunniteltu aikataulu:
Työt pitävät minua aika kiireisenä tällä viikolla (viikko 3, 2022). Siksi oletan aloittavani projektin viikolla 4. Kolmanneksi viimeinen tunti on viikolla 9 ja kokisin että tämä on ehdoton takaraja. Viikko 8 on hiihtoloma joten tavoittelisin saavani projektin valmiiksi viikon 7 tunnille esitettäväksi. Aikaa projektille olisi näin 2,5 viikkoa ja jos projekti veisikin odotettua enemmän aikaa, olisi minulla vielä 2 viikkoa lisäaikaa hiihtoloman mukaanlukien.

Työvaiheita on 5 joten työtahti voidaan laskea tähän tapaan: 5/2,5 = 2
Näin minun olisi siis tarkoitus suorittaa 2 vaihetta per viikko joka tuntuu itselle täysin kohtuulliselta.

## Lopputoteamukset
Projekti vaikuttaa itselle hauskalta ja myös tarpeelliselta sillä tämä on jotain mitä olen halunnut nyt pitempään jo toteuttaa. Toivon että se tulee myös inspiroimaan kanssaopiskelijoita. 

Alustava suunnitelma todennäköisesti muuttuu ja ehdotukset sekä ideat ovat aina tervetulleita. Mikäli aikataulussa tai toteutuksessa on yleisesti jotakin parannettavaa otan palautetta mieluusti vastaan.
