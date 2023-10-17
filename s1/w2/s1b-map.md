Za rad sa mapama koristićemo:

- `Leaflet` biblioteku za mape.
- `Nominatim API` api za geocoding i reverse geocoding.
- `Open Eleveation API` api za nadmorsku visinu.
- `Leaflet Routing Machine` biblioteku za rutiranje.
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

```code
"architect": {
        "build": {
          "builder": "@angular-devkit/build-angular:browser",
          "options": {
            "outputPath": "dist/psw-map",
            "index": "src/index.html",
            "main": "src/main.ts",
            "polyfills": "src/polyfills.ts",
            "tsConfig": "tsconfig.app.json",
            "assets": [
              "src/favicon.ico",
              "src/assets"
            ],
            "styles": [
              "./node_modules/leaflet/dist/leaflet.css",
              "src/styles.css"
            ],
            "scripts": []
          },
          "configurations": {
```

### c. Uvezivanje HTML i TS dela

map.component.html:  
```code
<div class="map-frame">
  <div id="map"></div>
</div>
```

map.component.ts:  
```code
import { Component, AfterViewInit } from '@angular/core';
import * as L from 'leaflet';

@Component({
  selector: 'app-map',
  templateUrl: './map.component.html',
  styleUrls: ['./map.component.css'],
})
export class MapComponent implements AfterViewInit {
  private map: any;

  constructor(private mapService: MapService) {}

  private initMap(): void {
    this.map = L.map('map', {
      center: [45.2396, 19.8227],
      zoom: 13,
    });

    const tiles = L.tileLayer(
      'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      {
        maxZoom: 18,
        minZoom: 3,
        attribution:
          '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
      }
    );
    tiles.addTo(this.map);
  }

  ngAfterViewInit(): void {
    this.initMap();
  }
}

```

Iskoristili smo AfterViewInit lifecycle hook koji se pozove tek kada je čitav pogled inicijalizovan i u okviru njega inicijalizovali mapu. Mapa je uvezana sa HTML-om preko id (koji se zove map) i inicijalizovana je na određene koordinate (45,2; 19.8) i zoom level (13). Potom su povučeni OpenStreetMap layer-i i uvezani za našu mapu.  

Sve što je potrebno dalje uraditi jeste ugraditi xp-map element negde u aplikaciji. Nemoj zaboraviti da u okviru SharedModule-a eksportuješ MapComponent i da importuješ SharedModule u onaj modul gde želiš da ga iskoristiš. Takođe da bi proverili da li se renderuje mapa možemo dodati visinu kroz CSS što možeš videti na sledećoj slici.  

map.component.css:  
```code
.map-frame {
  border: 2px solid black;
}

#map {
  height: 600px;
}
```
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

```code
  ngAfterViewInit(): void {
    let DefaultIcon = L.icon({
      iconUrl: 'https://unpkg.com/leaflet@1.6.0/dist/images/marker-icon.png',
    });

    L.Marker.prototype.options.icon = DefaultIcon;
    this.initMap();
  }
```

### b. Registrovanje funkcije.

Na slici ispod je predstavljena funkcija koja registruje reakciju na 'click' mape tj. definiše callback funkciju koja će se aktivirati kada se klikne na mapu. Na klik mape ćemo preuzeti geografsku širinu i dužinu a potom pomoću L.Marker-a dodati pin na našu mapu. Dodatno pozovi this.registerOnClick() u okviru initMap() funkcije nakon kreiranja mape.

```code
  registerOnClick(): void {
    this.map.on('click', (e: any) => {
      const coord = e.latlng;
      const lat = coord.lat;
      const lng = coord.lng;
      console.log(
        'You clicked the map at latitude: ' + lat + ' and longitude: ' + lng
      );
      new L.Marker([lat, lng]).addTo(this.map);
    });
  }
```

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

```code
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root',
})
export class MapService {
  constructor(private http: HttpClient) {}

  search(street: string): Observable<any> {
    return this.http.get(
      'https://nominatim.openstreetmap.org/search?format=json&q=' + street
    );
  }

  reverseSearch(lat: number, lon: number): Observable<any> {
    return this.http.get(
      `https://nominatim.openstreetmap.org/reverse?format=json&lat=${lat}&lon=${lon}&<params>`
    );
  }
}
```

Pozive funkcija možeš videti na slici ispod.  

```code
  search(): void {
    this.mapService.search('Strazilovska 19, Novi Sad').subscribe({
      next: (result) => {
        console.log(result);
        L.marker([result[0].lat, result[0].lon])
          .addTo(this.map)
          .bindPopup('Pozdrav iz Strazilovske 19.')
          .openPopup();
      },
      error: () => {},
    });
  }

  registerOnClick(): void {
    this.map.on('click', (e: any) => {
      const coord = e.latlng;
      const lat = coord.lat;
      const lng = coord.lng;
      this.mapService.reverseSearch(lat, lng).subscribe((res) => {
        console.log(res.display_name);
      });
      console.log(
        'You clicked the map at latitude: ' + lat + ' and longitude: ' + lng
      );
      const mp = new L.Marker([lat, lng]).addTo(this.map);
      alert(mp.getLatLng());
    });
  }
```

## 3. Nadmorska visina

Kako bi dobili nadmorsku visinu na osnovu geofraske širine i dužine možemo iskoristiti <a href="https://open-elevation.com/">Open Elevation API </a> (proučiti dodatno dokumentaciju). Primer funkcije je na slici ispod.  

```code
getElevation(): Observable<any> {
    return this.http.get('https://api.open-elevation.com/api/v1/lookup?locations=10,10|20,20|41.161758,-8.583933')
}
```

## 4. Rutiranje

Za ovaj zadatak potrebno je:

<ol type="a">
  <li>Instairati Leaflet Routing Machine biblioteku.</li>
  <li>Kreirati nalog i API key na MapBox-u.</li>
  <li>Napisati funkciju za rutiranje.</li>
</ol>

### a. Instaliranje biblioteke

Biblioteka se instaliraju sledećim komandama:  
1. <b>npm i leaflet-routing-machine</b>
2. <b>npm i @types/leaflet-routing-machine</b>.

Potom je potrebno u angluar.json u okviru styles dela postaviti putanju do leaflet-routing stilova ("./node_modules/leaflet-routing-machine/dist/leaflet-routing-machine.css"). Kao u koraku 0.b

### b. Nalog i API KEY

Možeš ispratiti sledeći sajt - https://www.mapbox.com/.

### c. Funkcija za rutiranje  

Preko L.Routing.control možemo napraviti željenu rutu, waypoints predstavlja niz geografskih širina i dužina dok router specifira koji ćemo routing engine koristiti. U ovom slučaju koristimo mapbox kome smo prosledili api key i da želimo rutu za pešačenje, takođe možemo proslediti profil za automobil ili bicikl (pogledaj mapbox dokumentaciju).  

Dodatno preko eventa 'routesfound' možemo izvući informacije o distanci i potrebnom vremenu za rutu.

```code
  setRoute(): void {
    const routeControl = L.Routing.control({
      waypoints: [L.latLng(57.74, 11.94), L.latLng(57.6792, 11.949)],
      router: L.routing.mapbox('TVOJ_MAPBOX_API_KEY', {profile: 'mapbox/walking'})
    }).addTo(this.map);

    routeControl.on('routesfound', function(e) {
      var routes = e.routes;
      var summary = routes[0].summary;
      alert('Total distance is ' + summary.totalDistance / 1000 + ' km and total time is ' + Math.round(summary.totalTime % 3600 / 60) + ' minutes');
    });
  }
```

Rezultat:  

![image](https://github.com/psw-ftn/supportive-information/assets/57589408/44ef0ef8-efaf-4d27-a114-db1ae544678b)

# Uvezivanje mapa sa komponentama za kreiranje i izmenu ključnih tačaka i objekata
Ne zaboravi da je, pored integracije mapa, neophodno iskoristiti ovu komponentu prilikom:

1. Kreiranja i izmene ključnih tačka, gde korisnik bira tačku na mapi umesto da ručno unosi geografsku širinu i dužinu.
2. Kreiranje i izmene objekata, gde korisnik bira tačku na mapi umesto da ručno unosi geografsku širinu i dužinu.
3. Prikaz svih ključnih tačaka jedne ture.

Za tačku 1. i 2. je u serverskoj aplikaciji potrebno sitno proširenje domenskog modela (i tabele u bazi, da li ručno ili kroz migracije), a većina rada će biti na klijentskoj aplikaciji.
Za tačku 3. će u serverskoj aplikaciji verovatno trebati proširiti postojeće servise (a možda i domenski model), tako da dobave ključne tačke za određenu turu.
