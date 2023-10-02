Druga nedelja prvog sprinta ima više različitih zadataka, gde će deo tima rešavati jedne, a ne druge. Zadatak koji si preuzeo na sebe diktira smernice koje trebaš da pratiš:

- **Integracija biblioteke za crtanje mapa** - TODO
- **Razgovor sa budućim korisnicima aplikacije** - TODO
- **Analiza sajtova za uzor i definisanje zahteva** - [link](https://github.com/psw-ftn/supportive-information/blob/master/s1/w2/s1d-landing-page.md).
- **Revizija i retrospektiva sprinta** - TODO.

<br><br><br><br>
# Testiranje konačnog softvera
Za razvoj softvera na ovom projektu koristićemo model grananja "Feature branching". Ovaj način razvoja softvera potencira kreiranje nove grane za svaku funkcionalnost softvera (feature). U nastavku su nabrojane grane koje je potrebno koristiti:
- `main` (master) - glavna grana na kojoj se uvek mora nalaziti stabilna verzija softvera
- `development` - kreirana iz `main` grane i spaja se sa njom na kraju sprinta
- feature grane - kreirane iz `development` grane i spajaju se sa njom kako se koja funkcionalnost završi

<br>
Razvoj softvera u toku sprinta uključuje implementaciju feature grana i njihovu reviziju pre nego što se spajaju na development. Pred kraj sprinta je potrebno spojiti `development` na `main`, no bitno je dobro istestirati sistem pre toga. Pošto na `main` grani uvek treba da bude stabilna verzija softvera, potrebno je:
<ol>
    <li>Preuzeti kompletno sabran kod sa development grane na lokalni računar.</li>
    <li>Pokrenuti sve napisane testove.</li>
    <li>Pokrenuti softver i ručno testirati funkcionalnosti kako bi se uverili da sve funkcionalnosti rade kako je očekivano. Prilikom testiranja funkcionalnosti držati otvorenu konzolu od browsera kako bi se uočile greške.</li>
    <li>Za svaku uočenu grešku je potrebno kreirati karticu na Trello tabli koja adresira ovaj problem. Data kartica zavodi _bug_ koji tim treba odmah da reši ako blokira funkcionalnost ili će moći da reši u kasnijim sprintovima ako predstavlja sitan problem. Jasno imenovati problem i detaljno opisati kako se problem manifestuje.</li>
    <li>Kada tim ustanovi potpunu ispravnost softvera, development grana se može spojiti sa main granom putem *pull request* mehanizma.</li>
</ol>


<br><br><br><br>
# Retrospektiva sprinta
Retrospektiva je vreme da tim razmisli o prošlom sprintu, identifikuje šta je prošlo dobro ili loše, i isplanira šta bi se moglo poboljšati u narednom sprintu. Kroz retrospektivu tim postaje kohezivniji, efikasniji i svaki njegov član unapređuje svoju ekspertizu.<br>
Potrebno je popuniti izveštaj za retrospektivu, koji možete preuzeti <a href="https://github.com/psw-ftn/supportive-information/blob/master/s1/w2/Sprint review template.pptx" target="_blank">ovde</a>. U nastavku teksta će biti opisano kako ga popuniti.

<ol type="a">
  <li>Priprema za retrospektivu: Pre retrospektive svaki član tima treba da pregleda sve korisničke priče i zadatke na kojima je radio tokom sprinta. Podsetite se šta je postignuto i sa kojim izazovima ste se susreli. Ova priprema je neophodna kako bi se popunio izveštaj koji zahteva da se za svakog člana navedu korisničke priče na kojima je radio, procenjeni i stvarni poeni koje priča nosi, i interesantni aspekti vezani za korisničku priču. Svi članovi tima treba da pošalju Scrum masteru ove informacije kako bi se mogao popuniti prvi deo izveštaja koji se odnosi na svakog člana i korisničke priče na kojima je radio.</li>
  <li>Planiranje retrospektive: Isplanirajte vreme i mesto sastanka za retrospektivu na kojoj treba da učestvuju svi članovi tima.</li>
  <li>Retrospektiva (više detalja ispod) </li>
  <li>Plan za unapređenje: Jasno istaknite isplanirana unapređenja na mesto koje je dostupno svim članovima tima. Možete dodati na svoju Trello tablu posebnu kolonu ili kartice koje ističu plan koji imate, kako bi svi članovi tima imali podsetnik na čemu je to potrebno raditi osim implementacije projekta.</li>
</ol>

### c. Retrospektiva
Retrospektiva treba da bude organizovana tako da svi članovi tima podele svoja iskustva. Podstaknite aktivno učestvovanje svih članova tako što će svi podeliti svoja zapažanja. Retrospektiva treba da bude konstruktivna, pri čemu treba izbegavati da se krive pojedinci. Drugi deo izveštaja koji se odnosi na ceo tim je potrebno popuniti sledećim informacijama:

<ol>
  <li>Šta je dobro urađeno u sprintu? Identifikujte i proslavite uspehe i dostignuća. Prepoznavanje dostignuća podiže moral i motivaciju tima.</li>
  <li>Šta je loše urađeno u sprintu? Identifikujte probleme u okviru tima, stvari koje su vas kočile u implementaciji i izazove sa kojima ste se suočili tokom sprinta. Važno je da članovi tima iskreno podele negativna iskustva, kako bi se pronašla rešenja za identifikovane probleme i kako se ti problemi ne bi iznova ponavljali.</li>
  <li>Koji je plan za unapređenje narednog sprinta?</li>
  <ul>
    <li>Fokusirajte se na identifikaciju rešenja koja su delotvorna za rešavanje problema koji su se pojavili tokom sprinta.</li>
    <li>Zajednički dajte prioritet identifikovanim problemima i predlozima za poboljšanje. Skoncentrišite se na promene koje mogu imati najveći uticaj u narednom sprintu.</li>
    <li>Kada razgovarate o poboljšanjima, uverite se da su ona specifična, ostvariva i relevantna.</li>
  </ul>
</ol>
