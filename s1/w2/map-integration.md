Za rad sa mapama koristićemo:

- `Leaflet` biblioteku za mape.
- `Nominatim API` api za geocoding i reverse geocoding.
- `Open Eleveation API` api za nadmorsku visinu.
- `MapBox` engine za rutiranje.

Postepeno ćete integrisati potrebne stvari za mapu kako budete razvijali projekat. Ova stranica sadrži smernice za integraciju mape u Angular projekat gde ćemo videti:

<ol start="0">
  <li>Kako da integrišemo mapu.</li>
  <li>Kako da postavimo markere na mapu.</li>
  <li>Kako da radimo geocoding i reverse geocoding.</li>
  <li>Kako da dobavimo informacije o nadmorskoj visini.</li>
  <li>Kako da kreiramo rute.</li>
</ol>

## 0. Integracija mape

Za ovaj zadatak potrebno je:

<ol type="a">
  <li>Kreirati novu komponentu za mapu.</li>
  <li>Instalirati potrebne biblioteke i podesiti angular.json.</li>
  <li>Povezati HTML i TS deo.</li>
</ol>

### a. Kreiranje komponente

Kako je mapa deljena komponenta (koristiće je npr. i TourExecutionModule i TourAuthoringModule) možemo je smestiti u okviru SharedModule-a. Komponentu kreiraš tako što se pozicioniraš u okviru shared foldera (modula) i pokreneš komandu ng g c map.

### b. Instaliranje biblioteka

Nakon kreiranja komponente gde ćemo smestiti mapu potrebno je instalirati biblioteku za renderovanje mape. Instaliraćemo dve biblioteke sledećim komandama:  
1. <b>npm i leaflet</b>
2. <b>npm i @types/leaflet</b>.

Potom je potrebno u angluar.json u okviru styles dela postaviti putanju do leaflet stilova ("./node_modules/leaflet/dist/leaflet.css").

![image](https://github.com/psw-ftn/supportive-information/assets/57589408/8df11610-22aa-4e30-ba2d-c8b300022d27)

### c. Uvezivanje HTML i TS dela

map.component.html:  
![image](https://github.com/psw-ftn/supportive-information/assets/57589408/46b9c51d-988a-495b-9358-a7457cd48391)

map.component.ts:  
![image](https://github.com/psw-ftn/supportive-information/assets/57589408/bb33adbd-e5eb-42b7-9126-32a885caef37)

Iskoristili smo AfterViewInit lifecycle hook koji se pozove tek kada je čitav pogled inicijalizovan i u okviru njega inicijalizovali mapu. Mapa je uvezana sa HTML-om preko id (koji se zove map) i inicijalizovana je na određene koordinate (45,2; 19.8) i zoom level (13). Potom su povučeni OpenStreetMap layer-i i uvezani za našu mapu.  

Sve što je potrebno dalje uraditi jeste ugraditi xp-map element negde u aplikaciji. Nemoj zaboraviti da u okviru SharedModule-a eksportuješ MapComponent i da importuješ SharedModule u onaj modul gde želiš da ga iskoristiš. Takođe da bi proverio da li se renderuje mapa dodaj joj visinu kroz CSS što možeš videti na sledećoj slici.  

map.component.css:  
![image](https://github.com/psw-ftn/supportive-information/assets/57589408/3a18aeba-b740-44e2-a23d-2bec9d01d350)  

Rezultat:

![image](https://github.com/psw-ftn/supportive-information/assets/57589408/928e917f-1ccd-4401-b600-b950de045b70)


## 1. Postavljanje markera na mapu  

Za ovaj zadatak potrebno je: 

<ol type="a">
  <li>Registrovati slike markera.</li>
  <li>Registrovati funkciju za postavljanje markera na mapu.</li>
</ol>

### a. Registrovanje slike markera.
Kako bi postavili markere na mapu treba da prvo registrujemo sliku markera (ovaj korak je isto potrebno uraditi u okviru AfterViewInit dela i pre inicijalizacije mape).  

![image](https://github.com/psw-ftn/supportive-information/assets/57589408/963471e2-f954-4c47-9c57-c31a5f965dc8)

### b. Registrovanje funkcije.

Na slici ispod je predstavljena funkcija koja registruje reakciju na 'click' mape tj. definiše callback funkciju koja će se aktivirati kada se klikne na mapu. Na klik mape ćemo preuzeti geofrasku širinu i dužinu a potom pomoću L.Marker-a dodati pin na našu mapu.

![image](https://github.com/psw-ftn/supportive-information/assets/57589408/1c08bb13-e35a-4c06-8874-904993019996)

Rezultat:

![image](https://github.com/psw-ftn/supportive-information/assets/57589408/60d18f0d-b769-455f-9ed0-b6fee4f86769)

## 2. Geocoding, reverse geocoding

Za ovaj zadatak potrebno je:

<ol type="a">
  <li>Kreirati servis koji će koristiti mapa.</li>
  <li>Dodati funkcije u servis za komunikaciju sa Nominatim API-em.</li>
</ol>

### a. Dodavanje servisa.

Kako bi dodali servis možemo se pozicionirati u okviru map foldera i pokrenuti komandu ng g s map.

### b. Dodavanje funkcije u servis.

Nominatim API nam omogućuje da na osnovu naziva ulice (npr. Stražilovska 19) dobijemo geofrasku širinu i dužinu. Obrati pažnju da ako kao vrednost parametra pošalješ samo "Stražilovska 19" dobićeš kao odgovor niz vrednosti geofraskih širina i dužina sa obzirom da ova ulica postoji u mnogim gradovima u Srbiji. Na tebi je da smisliš najbolje rešenje za korisnika kako bi minimizovao ovakve greške (npr. jedno od rešenja je da se zahteva i unos grada - Stražilovska 19, Novi Sad). Takođe Nominatim API nam omogućuje i obrnutu pretragu tj. na osnovu geofraske širine i dužine možemo dobiti naziv ulice (ovo je korisno kako bi na osnovu klika na mapi dobili naziv ulice). Obe funkcije su na slici ispod.  
Obrati pažnju da funkcija vraća any, ovo nije poželjna praska u TypeScript-u ali je uredu kao privremeno rešenje dok nismo sigurno koji nam podaci trebaju od eksternog API-a. Svakako napravi interfejs/klasu u svom deljenom modelu koji će prihvatiti samo one podatke koje ćeš koristiti od eksternog API-a.

![image](https://github.com/psw-ftn/supportive-information/assets/57589408/c2f4f9ff-a5e7-492a-a50c-d9e28f56999a)  

Pozive funkcija možeš videti na slici ispod.  

![image](https://github.com/psw-ftn/supportive-information/assets/57589408/ce4923ab-d451-4c68-be52-13b2a80e58c0)

## 3. Nadmorska visina

Kako bi dobili nadmorsku visinu na osnovu geofraske širine i dužine možemo iskoristiti <a href="https://open-elevation.com/">Open Elevation API </a> (proučiti dodatno dokumentaciju). Primer funkcije je na slici ispod.  

![image](https://github.com/psw-ftn/supportive-information/assets/57589408/d4b76b98-c625-4df6-8328-cb1bd5fd174e)


## 4. Rutiranje











