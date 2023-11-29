U sklopu druge nedelje želimo da proširimo naše razumevanje DDD-a sa tri taktička šablona, gde će članovi tima birati sa kojim šablonom žele da uđu u koštac. Šabloni u pitanju su _aplikativni servisi_, _domenski servisi_ i _event sourcing_. Pre raspodele posla, članovi tima treba da se upoznaju sa osnovnom idejom svakog koncepta kroz sledeće materijale:

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

Kada testiramo pametne aplikativne servise, kompleksno rešenje nam je da napravimo testne verzije spoljašnjih sistema. Ovo rešenje ima smisla za spoljašnji sistem koji se baš često koristi, kao što je baza podataka. Dato rešenje je previše komplikovano za spoljašnji sistem koji samo par funkcionalnosti koristi. U tom slučaju nam je interesantno da uvedemo _test double_. Šta je test double i kako se implementira u testu prikazuje **[sledeća playlista]()**. Naš zadatak prilikom testiranje funkcije gde uvodimo _test double_ je da:

1. Odredimo servis koji treba zameniti sa lažnom implementacijom,
2. Utvrdimo da li je potreban _stub_ ili _mock_ i
3. Implementiramo odabrani _test double_ u _arrange_ sekciji testa.

TODO: Proveri video materijale

# Domenski servisi
Koncept domenskih servisa je istaknut u videu na početku. U opštem slučaju će domenski servisi biti pametne funkcionalne klase koje sabiraju poslovnu pamet koja ne pripada ni jednom agregatu. Primer ovakve klase je klasa koja implementira algoritam za kalkulaciju statistika ili uvezivanje rezultata više agregata kako bi se sračunala neka napredna informacija.

Domenski servisi pripadaju u domenskom sloju i generalno su jednostavniji za rukovanje, iako im logika može biti složena. Domenski servis možemo testirati putem jediničnih testova, gde direktno instanciramo i koristimo servis i proveravamo da li za sve kombinacije daje dobre rezultate.

# Event sourcing
TODO