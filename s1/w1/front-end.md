Frontend deo aplikacije je izgrađen koristeći:

- `Angular v16` radni okvir za izgradnju single page aplikacija (SPA).

Postepeno ćemo se upoznavati sa radnim okvirom i kroz kurs ćemo sve pametnije stvari moći da radimo sa njim. Ova stranica sadrži smernice za izradu jednostavne funkcionalnosti u klijentskom delu aplikacije, gde ćemo videti:

<ol start="0">
  <li>Kako je organizovan projekat i kako se pokreće.</li>
  <li>Od čega se sastoje komponente i moduli.</li>
  <li>Kako da definišemo komponentu i uvežemo podatke.</li>
  <li>Kako da kreiramo novi entitet i pošaljemo ga serveru.</li>
  <li>Kako da ažuriramo već kreiran entitet i pošaljemo ga serveru.</li>
  <li>Kako da obrišemo postojeći entitet.</li>
</ol>

Nulti i prvi korak ćeš raditi samo jednom u potpunosti, dok ćeš korake 2 do 6 raditi svaki put kad razvijaš novu funkcionalnost. Redosled koraka 2 do 6 ne mora da prati naveden, no dobro je da prvi put ispratiš dati redosled.

## 0. Organizacija i pokretanje projekta

Prvi put kad sedneš da radiš na projektu ćeš morati da kloniraš repozitorijum svog tima na svoju mašinu. Ovde će ti pomoći `git clone` komanda uz URL repozitorijuma tima.
Preporuka je da otvoriš Solution u svom razvojnom okruženju (naša preporuka je Visual Studio Code ili WebStorm) i da ga istražiš pre nego što nastaviš da čitaš. Pogledaj naredni <a href="https://www.youtube.com/watch?v=Puc6bNYfkzg">video</a> u kojem prolazimo sledeće:

1. Klonriranje početnog projekta napisanom u Angular-u (git clone).
2. Instaliranje potrebnih biblioteka za pokretanje projekta (npm install).
3. Kratak pregled strukture projekta.
4. Pokretanje projekta (ng serve).
5. Pregled UI-a projekta.

Napomene:
Kako bi pokretali/kreirali angular projekte na svom računaru potrebno je instalirati sledeći softver:
1. <a href="https://nodejs.org/en">node.js</a> - (provera verzije: node --version)
2. <a href="https://www.npmjs.com/">npm</a> - (provera verzije: npm --version)
3. angular cli - (npm install -g @angular/cli) (provera verzije: ng --version)

Obratiti pažnju na to da Angular framework često zna da prijavljuje grešku bez razloga, najčešće u dodavanju novih modula ili menjanja putanje fajla te je potrebno prekinuti izvršavanje programa i opet pokrenuti komandu ng serve.

Pregled fajlova van src foldera projekta:
1. <b>.editorconfig</b> je fajl koji nam omogućava konfiugraciju našeg editora koda (VSC, WebStorm). Potrebno je da svi u okviru tima imaju identičan .editorconfig kako git ne bi prijavljivao razlike u formatiranju koda (space-ing, indentacija, prelamanje koda itd.).
2. <b>.gitignore</b> sadrži putanje do fajlova koje git ne treba da prati i koji se ne šalju na repozitorijum. Obratiti pažnju da je node_modules (folder koji sadrži sve biblioteke potrebne za pokretanje našeg projekta) takođe u .gitignore stoga je potrebno uvek nakon pull-a projekta pokrenuti npm install kako bi se instalirale sve potrebne biblioteke u okviru node_modules foldera.
3. <b>angular.json</b> - fajl za konfiguraciju Angular projekta (npr. ubacivanje eksternih stilova). Sadrži informacije o arhitekturi projekta, zavisnostima, build i test konfiguracije projekta itd.
4. <b>package-lock.json</b> - sadrži spisak svih instaliranih biblioteke u našem projektu.
5. <b>package.json</b> - sadrži sve potrebne biblioteke za naš projekat pri čemu naglašava koje su dodatno potrebne za dev i za prod.
6. <b>readme</b> - najčešće predstavlja korake koji su potrebni za pokretanje projekta.
7. <b>tsconfig.app.json/tsconfig.json</b> - konfiguracija typescript-a.
8. <b>node_modules</b> - folder u okviru kog su instalirane sve biblioteke za naš projekat.

<b>infrastructure</b> - folderi/moduli vezani za autentifikaciju, rutiranje, stilove(angular-materials).  
<b>shared</b> - deljeni modeli i komponente.
## 1. Od čega se sastoje komponente i moduli?

<b>Definicija komponente:</b>
Komponenta predstavlja osnovnu gradivnu jedinicu svake stranice u Angular aplikaciji. Jednu komponentu čine TypeSrcript, HTML i CSS deo. TypeScript deo vodi računa o podacima koje komponenta renderuje i životnom ciklusu komponente (https://angular.io/guide/lifecycle-hooks), HTML deo daje strukturu pogleda, dok CSS daje stilove pogledu. U daljem tekstu stranicom će se smatrati pogled na UI koji je sastavljen od jedne ili više komponenti.
Komponente se mogu ugrađivati jedne u drugu i rutirati. Na sledećem <a href="https://www.youtube.com/watch?v=nF411IGhZjs">videu</a> pogledaj više o komponentama a možeš baciti pogled i <a href="https://angular.io/guide/component-overview">ovde</a>.  

<b>Definicija modula:</b>
Angular moduli predstavljaju kohezivne celine od kojih se sastoji jedna Angular aplikacija. Moduli nam omogućavaju da grupišemo komponente, direktive i servise koji su povezani. Angular aplikaciju možeš zamisliti kao puzlu gde je svaki deo (modul) potreban kako bi video celu aplikaciju kako funkcioniše. Više o modulima možeš pogledati <a href="https://angular.io/guide/ngmodules">ovde</a>.

## 2. Kako da dodam novu komponentu i uvežem podatke?

Kad god pristupimo rešavanju nove korisničke priče, potrebno je da otvorimo novu granu koju ćemo izvući iz `development` grane. Ovo radimo putem `git branch feat/IME_FEATURA` komande. Nakon kreiranja grane, možemo da uradimo `git checkout feat/IME_FEATURA` i da krenemo sa razvojem.
Većina zadataka u prvoj nedelji podrazumevaju izradu stranica za prikaz entiteta (a potom i za izmenu i brisanje). Za ovaj zadatak je potrebno:

<ol type="a">
  <li>Odabrati dobar modul u koji smeštaš novu komponentu.</li>
  <li>Napraviti novu komponentu.</li>
  <li>Povući podatke sa servera.</li>
  <li>Rutirati komponentu.</li>
</ol>

### a. Izbor modula

U startu počinjemo sa 6 feature-modula:

<b>Administration</b> - slučajevi korišćenja vezani za admina (upravljanje opremom, korisnicima i generalno administriranjem sistema)  
<b>Blog</b> - slučajevi korišćenja vezani za blog (pisanje blogova, ostavljanju komentara na blog)  
<b>Layout</b> - slučajevi korišćenja vezani za sve korisnike (registrovane i neregistrovane) poput navbar-a i home stranice.  
<b>MarketPlace</b> - slučajevi korišćenja vezani za odabir i kupovinu tura (pregledanje, kupovina, čitanje komentara za ture itd.)   
<b>TourAuthoring</b> - slučajevi korišćenja namenjeni za kreiranje i izmenu tura (kreiranje ture, kreiranje tačaka od interesa, dodatnih objekata na mapi itd.)  
<b>TourExecution</b> - slučajevi korišćenja vezani za izvršavanje ture (prikaz napretka u ovkiru jedne ture, otkrivanje tajne, pomeranje pozicije na mapi itd.)  

Izazov je odrediti kom modulu pripada nova komponenta. Odluka se donosi na osnovu toga kom modulu najviše ima smisla da pripada nova komponenta na osnovu opisa modula.

### b. Kreiranje nove komponente

Nova komponenta se kreira tako što se pozicioniraš u folder željenog modula i pokreneš komandu ng g c naziv-komponente. U narednom <a href="https://youtu.be/h2JFDUQnT-w">videu</a> je prikazano kreiranje komponente i uvezivanje podataka. Napomena da je u videu demonstrativno prikazano i kreiranje modula, u početnom projektu u okviru prve dve nedelje nema potrebe da kreiraš novi modul već samo da ubaciš komponentu u neki od postojećih.

### c. Povlačenje podataka sa servera.

Za komunikaciju sa serverom će biti potreban servisni sloj u klijentskoj aplikaciji. Njega možeš kreirati tako što se pozicioniraš u željeni modul i pokreneš komandu ng g s naziv_servisa. Pravimo jedan servis po modulu. Povlačenje podataka sa servera i njihovo renderovanje je predstavljeno u narednom <a href="https://youtu.be/ky-ZQsyyYsE">videu</a>.

### d. Rutiranje komponente.

Kako bi korisnik mogao da pristupi komponenti koju smo napravili trebalo bi je rutirati. U narednom <a href="https://youtu.be/66qT7-ZXXUk">videu</a> možeš pogledati kako se rutira komponenta.  
Dodatno pogledaj <a href="https://github.com/psw-ftn/tourism-fe/blob/main/Explorer/src/app/feature-modules/layout/navbar/navbar.component.html">kod</a> da vidiš kako da preko button-a menjaš trenutnu rutu aplikacije (obrati pažnju na [routerLink]).

