U sklopu četvrtog sprinta želimo da proširimo naše razumevanje DDD-a sa tri taktička šablona, gde će članovi tima birati sa kojim šablonom žele da uđu u koštac. Šabloni u pitanju su _aplikativni servisi_, _domenski servisi_ i _event sourcing_. Pre raspodele posla, članovi tima treba da se upoznaju sa osnovnom idejom svakog koncepta kroz sledeće materijale:

- Aplikativni i domenski servisi - [video](https://youtu.be/Y8I4THKo9HA).
- Event sourcing - [video](https://youtu.be/cTMG3QB7Lys).

**Napomena**: Tim može da zameni kartice koje mi predlažemo sa karticama koje će uvesti, spram procene tima, vrednije funkcionalnosti u proizvod. Međutim, neophodno je da nove kartice podrazumevaju ugradnju jednog od tri šablona navedenih iznad.

# Aplikativni servisi
Koncept aplikativnih servisa je istaknut u videu iznad. Aplikativne servise delimo u dve kategorije:

1. Koordinatore koji interaguju sa drugim aplikativnim servisima i domenskim klasama. Tipični primeri ovakvih klasa su `Service` klase, koje smeštamo u `Core/UseCases` u našoj arhitekturi.
2. Pametne funkcionalne klase koje enkapsuliraju tehničku pamet. Poznati primeri ovakvih klasa su `Repository` klase, koje sabiraju pamet rada sa skladištem podataka ili objektno-relacionim maperom. Drugi primeri su klase koje rešavaju bezbednosne zahteve, šalju email, SMS ili viber poruke, brinu o keširanju, itd.

### 1. Dizajniranje i implementacija pametnog aplikativnog servisa
Za naš zadatak su interesantne pametne klase koje ne rešavaju odgovornost repozitorijuma. Kada dizajniramo ovakav servis, treba da razumemo:

1. Šta je tačno odgovornost tog servisa? Koju logiku će sadržati?
2. Gde u arhitekturi treba definisati taj servis.

Za drugu dilemu su nam validne opcije `Core/UseCases` ili `Infrastructure` paketi. Tehnička logika ne treba da postoji u `Core/Domain`, dok nam je globalni `API` projekat rezervisan za kontrolere (koji su tehnički aplikativni servisi). Da bismo odlučili gde ćemo da smestimo aplikativni servis treba da razmislimo o:

- Da li servis treba da interaguje sa eksternim sistemom (npr. mail ili SMS serverom, skladištem podataka, drugom aplikacijom)? Ako da, logiku za rad sa eksternim sistemom smeštamo u infrastrukturni sloj. Da bi servis mogao da se pozove od strane koordinatorskih servisa, potrebno je da `Core/UseCases` definiše interfejs, koji će infrastrukturni servis da implementira?
- Da li servis sadrži tehničku pamet koja koristi isključivo mogućnosti programskog jezika i radnog okvira (u našem slučaju .NETa bez dodatnih biblioteka)? U tom slučaju možemo da smestimo aplikativni servis u `Core/UseCases`.

Potrebno je razmisliti gde ćemo tačno u okviru `Core/UseCases` da smestimo novi interfejs ili klasu, gde tom prilikom razmatramo ko sve koristi datu novinu i spram toga donosimo odluku.

### 2. Testiranje pametnog aplikativnog servisa
Jedinični testovi su nam korisni da dubinski istestiramo elemente domenskog sloja - agregate i domenske servise. Integracioni testovi  pokrivaju aplikativne servise i pružaju nam veću sigurnost da kompletne funkcionalnosti rade zato što pokrivaju kompletnu interakciju objekata.

Problem nastaje kada integracioni testovi testiraju funkcionalnosti koje pozivaju pametne aplikativne servise koji se nalaze u infrastrukturnom sloju. Naime, takvi servisi interaguju sa sistemima koji su van naše aplikacije, što može dovesti do neželjenog opterećenja spoljašnjih sistema. Na primer, ako pokrenemo 20 puta tokom razvoja testove koji šalju email ili viber poruku korisnicima, brzo ćemo prebaciti naš sistem u _Spam_ direktorijum. Ako svaki test prlja produkcionu bazu sa testnim podacima, lako ćemo napraviti sebi problem. Zbog ovoga smo i uveli koncept testne baze, kako bismo izbegli rad sa produkcionom bazom koju i regularna upotreba aplikacije koristi.

Kada testiramo pametne aplikativne servise, kompleksno rešenje nam je da napravimo testne verzije spoljašnjih sistema. Ovo rešenje ima smisla za spoljašnji sistem koji se baš često koristi, kao što je baza podataka. Dato rešenje je previše komplikovano za spoljašnji sistem koji samo par funkcionalnosti koristi. U tom slučaju nam je interesantno da uvedemo _test double_.

_Test double_ predstavlja lažnu implementaciju klase koja se koristi prilikom testiranja. Kod integracionih testova ćemo uvesti lažne implementacije za klase koje direktno interaguju sa eksternim sistemom koji ne želimo da aktiviramo pri testiranju. Kod jediničnih testova se lažne implementacije koriste kada želimo da izolujemo neku jedinicu ponašanja sistema koju testiramo. Dve vrste lažnih implementacija su nam interesantne:

- _Stub_, gde uvodimo lažnu implementaciju za klasu koja čita podatke iz eksternog sistema (npr. repozitorijum), sa idejom da funkcija koju testiramo dobije podatke od lažne implementacije, a ne od stvarnog skladišta podataka. Za _stub_ nam je bitno da glavna funkcija može da se izvrši bez interakcije sa eksternim sistemom i nije nam bitno da proverimo da li i na koji način se _stub_ aktivirao. **[Sledeći video](https://www.youtube.com/watch?v=iQJ448L5sdE)** prikazuje kako se _stub_ implementira u .NET tehnologiji.
- _Mock_, gde uvodimo lažnu implementaciju za klasu koja aktivira eksterne sisteme (npr. SMS server), sa idejom da proverimo da li funkcija koju testiramo bi stvarno aktivirala taj sistem kada ne bi bili testni uslovi. Dakle, za _mock_ nam je bitno da proverimo da li su funkcije lažne implementacije pozvane (u okviru _assert_ sekcije). **[Sledeći video](https://www.youtube.com/watch?v=Qn2rYN6vNHo)** prikazuje kako se _mock_ implementira u .NET tehnologiji.

Naš zadatak prilikom testiranje funkcije koja interaguje sa eksternim sistemima koje ne želimo da aktiviramo podrazumeva da:

1. Odredimo servis koji treba zameniti sa lažnom implementacijom,
2. Utvrdimo da li je potreban _stub_ ili _mock_ i
3. Ako je _stub_, implementiramo ga u _arrange_ sekciji, a ako je _mock_, postavimo ga u _arrange_ sekciji i ispitujemo ga u _assert_ sekciji testa.

# Domenski servisi
Koncept domenskih servisa je istaknut u videu na početku. U opštem slučaju će domenski servisi biti pametne funkcionalne klase koje sabiraju poslovnu pamet koja ne pripada ni jednom agregatu. Primer ovakve klase je klasa koja implementira algoritam za kalkulaciju statistika ili uvezivanje rezultata više agregata kako bi se sračunao nekakav podatak.

Domenski servisi pripadaju u domenskom sloju i generalno su jednostavniji za rukovanje, iako im logika može biti složena. Sve potrebne podatke domenski servis dobija od aplikativnog servisa koji vrši ulogu koordinatora.

Domenski servis možemo testirati putem jediničnih testova, gde direktno instanciramo i koristimo servis i proveravamo da li za sve kombinacije daje dobre rezultate.

# Event sourcing
Koncept event sourcinga je istaknut u videu iznad. Da bismo uveli event sourcing u projekat, pre nego što implementiramo bilo koji konkretan event sourced agregat, potrebno je da uvedemo dve roditeljske klase:

- `EventSourcedAggregate` je klasa koja će naslediti `Entity` i koja će biti nasleđena od strane korena agregata koji trebaju da podrže event sourcing. Ovde ćemo centralizovati opštu logiku za upravljanje domenskim događajima.
- `DomainEvent` je klasa koju će naslediti svaki konkretan domenski događaj. Ona sadrži opšte podatke koji su interesantni svakom događaju, poput identifikatora korena agregata, tipa agregata na koji se događaj odnosi i vremenskog trenutka kada je događaj nastao.

Navedene klase ćemo smestiti u `BuildingBlocks.Core.Domain`, pošto su relevantne za sve naše module. Poslednje pitanje koje treba ispitati je kako ćemo skladištiti listu domenskih događaja. U složenijem softverskom rešenju bismo potencijalno uveli dodatno skladište podataka namenjeno čuvanju domenskih događaja. Za naš slučaj je dovoljno da iskoristimo postojeću bazu podataka.

Sa postavljenom infrastrukturom možemo da implementiramo konkretne agregate koji trebaju da podrže event sourcing. Kako izgleda kod koji implementira sve ove celine analiziramo u **[ovom videu](https://www.youtube.com/watch?v=PjI42va62aU)**, dok **[ovaj video](https://www.youtube.com/watch?v=CsxvOFhpmRg)** sagledava opšti dizajn interakcije servisa i event sourced agregata i razmatra kako se domenski događaji formiraju i skladište u ozbiljnijim sistemima.
