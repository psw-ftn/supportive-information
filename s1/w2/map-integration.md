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

Sve što je potrebno dalje uraditi jeste ugraditi <xp-map></xp-map> element negde u aplikaciji. Nemoj zaboraviti da u okviru SharedModule-a eksportuješ MapComponent i da importuješ SharedModule u onaj modul gde želiš da ga iskoristiš. Takođe da bi proverio da li se renderuje mapa dodaj joj visinu kroz CSS što možeš videti na sledećoj slici.  

map.component.css:  
![image](https://github.com/psw-ftn/supportive-information/assets/57589408/3a18aeba-b740-44e2-a23d-2bec9d01d350)






