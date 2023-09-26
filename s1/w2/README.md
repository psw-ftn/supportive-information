# Analiza sajtova za uzor i definisanje zahteva
U okviru ovog zadatka potrebno je analizirati web aplikacije koje će služiti kao uzor za dizajniranje vašeg projekta. Analiza treba da obuhvati vizuelni i funkcionalni aspekt web aplikacija. Cilj ovog zadatka je da steknete uvid u efikasan dizajn i HCI principe koje možete primeniti prilikom izrade vašeg projekta.<br>
Preuzmite <a href="https://github.com/psw-ftn/supportive-information/blob/master/s1/w2/Design_HCI_analysis.xlsx" target="_blank">tabelu</a> i popunite je tokom analize. U nastavku teksta će biti istaknuto šta je tačno potrebno istražiti, a u zagradama će biti naznačeno u kojoj koloni tabele treba popuniti odgovarajuće informacije.


## 1. Odabir relevantnih web aplikacija
Potrebno je odabrati minimum dve web aplikacije koje imaju sličan domen i ciljnu publiku kao vaš projekat. Aplikacije treba da budu dovoljno kompleksne i bogate funkcionalnostima kako biste mogli izvršiti kvalitetnu analizu. Zabeležiti sledeće podatke:
- Naziv aplikacije (Upisati informaciju u koloni <i>Title</i>)
- Link do aplikacije (<i>Link</i>)
- Opis čemu aplikacija služi (<i>Description</i>)

## 2. Analiza početne stranice (landing page)
Analiza početne stranice web aplikacije uključuje:
<ol type="a">
  <li>Analizu dizajna i rasporeda vizuelnih elemenata</li>
  <ul>
    <li>Analiziraj odabranu paletu boja i načine na koje boje utiču na predstavljanje sadržaja korisniku. (<i>Color scheme</i>)</li>
    <li>Prouči fontove korišćene za naslove, podnaslove i paragrafe. Razmotri na koji način fontovi utiču na bolji prikaz sadržaja. (<i>Fonts</i>)</li>
    <li>Analiziraj organizaciju sadržaja (raspored po kolonama i redovima) i razmak između sadržaja. Ispitaj šta je postignuto datim rasporedom. (<i>Layout</i>)</li>
  </ul>
  <li>Analizu menija i navigacije</li>
  <ul>
    <li>Istraži lokaciju i dizajn korisničkih menija, kao i opcije koje se nude u njima. (<i>Menu</i>)</li>
    <li>Analiziraj na koji način se korisnik kreće kroz aplikaciju i kako se usmerava na važne informacije i funkcionalnosti (navigation bar, buttons, links...). (<i>Navigation</i>)</li>
  </ul>
  <li>Analizu sadržaja</li>
  <ul>
    <li>Prouči jasnoću teksta i da li dobro prenosi poruku stranice. (<i>Headlines and subheadlines</i>)</li>
    <li>Analiziraj koji je sadržaj prikazan pomoću slika i snimaka, kao i koja je prednost u odnosu na korišćenje teksta za prikaz datih informacija. (<i>Images and visuals</i>)</li>
  </ul>
  <li>Analizu angažovanja korisnika</li>
   <ul>
    <li>Identifikuj interaktivne elemente (sliders, forms, tooltips) i za šta se koriste. (<i>Interactive elements</i>)</li>
    <li>Prouči na koji način aplikacija motiviše korisnike da izvrše akcije poput registracije ili kupovine. (<i>Actions encouragement</i>)</li>
  </ul>
</ol>

<br><br><br><br>
# Revizija koda
Za razvoj softvera na ovom projektu koristićemo model grananja "Feature branching". Ovaj način razvoja softvera potencira kreiranje nove grane za svaku funkcionalnost softvera (feature). U nastavku su nabrojane grane koje je potrebno koristiti:
- main (master) - glavna grana na kojoj se uvek mora nalaziti stabilna verzija softvera
- development (dev) - kreirana iz main grane i spaja se sa njom na kraju sprinta
- feature grane - kreirane iz development grane i spajaju se sa njom kako se koja funkcionalnost završi

<br>
Razvoj softvera u toku sprinta se sastoji od nekoliko koraka:
<ol type="a">
  <li>Implementacija funkcionalnosti: Svaki član tima kreira novu granu za svaku novu funkcionalnost koju će implementirati. Ove grane se nazivaju feature grane (npr. feature/login) i napravljene su iz development grane. Sav kod vezan za pojedinačnu funkcionalnost se nalazi na odgovarajućoj feature grani.</li>
  <li>Spajanje feature grana sa development granom: Kada je funkcionalnost završena, feature grana se spaja sa development granom. Svaki član tima treba da vodi računa da na development granu spoji testiranu i do kraja implementiranu funkcionalnost.</li>
  <li>Spajanje development grane sa main granom (više detalja ispod)</li>
</ol>

### c. Spajanje development grane sa main granom
Na kraju sprinta, kada su sve završene funkcionalnosti sa feature grana spojene sa development granom, potrebno je spojiti development granu sa main granom. Pošto na main grani uvek treba da bude stabilna verzija softvera, potrebno je uraditi reviziju koda na development grani pre nego što se ona spoji sa main granom. U nastavku slede koraci koje je potrebno ispuniti:
<ol>
    <li>Potrebno je preuzeti kod sa development grane na lokalni računar.</li>
    <li>Pokrenuti sve napisane testove.</li>
    <li>Pokrenuti softver i ručno testirati funkcionalnosti kako bi se uverili da sve funkcionalnosti rade kako je očekivano. Prilikom testiranja funkcionalnosti potrebno je konsultovati se sa odgovarajućom korisničkom pričom tj. karticom na Trello tabli. Proveriti da li su ispunjeni svi navedeni kriterijumi (acceptance criteria) koji su navedeni.</li>
    <li>Za svaku uočenu grešku je potrebno kreirati karticu na Trello tabli koja adresira ovaj problem. Jasno imenovati problem i detaljno opisati kako se problem manifestuje. Revizija koda se ponavlja kada se problem reši.</li>
    <li>Kada revizori koda ustanove potpunu ispravnost softvera, development grana se može spojiti sa main granom.</li>
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
