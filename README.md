Repozitorijum za materijale koji podržavaju izradu projekta iz predmeta "Projektovanje softvera". Materijale treba koristiti u paraleli dok se radi na projektu pošto definišu faze rada. Na primer, za prvu nedelju prvog sprinta je potrebno uraditi jedan zadatak koji se sastoji od šest koraka. Materijali definišu smernice za svaki od tih šest koraka, pa ćeš pročitati smernice prvog koraka, primeniti ih na projektnom zadatku, preći na smernice za drugi korak i tako dalje.

# Početak projekta
U prvoj nedelji predmeta je potrebno da tvoj tim uradi nekoliko pripremnih zadataka. Većinu zadataka (sve sem poslednjeg) mogu da urade 2 člana tima koji će organizovati tim u prve tri nedelje predmeta (takozvani Scrum masteri). Bitno je da ostali članovi tima prihvate pozivnice koje dobiju i urade poslednji korak.

1. Kreiranje Discord servera u koji ćete dodati sve članove tima.
2. Kreiranje Trello table i pozivanje ostalih članova tima da se pridruže (detalji ispod).
3. Kreiranje GitHub organizacije, prateći sledeće [uputstvo](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/creating-a-new-organization-from-scratch).
4. Dodavanje svih članova tima na organizaciju, kao i nastavnički nalog _psw-ftn_.
5. Kreiranje 2 repozitorijuma, jedan za serversku aplikaciju (back-end) i jedan za klijentrsku aplikaciju (front-end). Repozitorijum za serversku aplikaciju treba da kreirate spram [templatea](https://github.com/psw-ftn/tourism-be). Slično treba uraditi za klijentrsku aplikaciju, koja koristi [ovaj template](https://github.com/psw-ftn/tourism-fe). Repozitorijum se pravi spram templatea putem zelenog tastera "Use this template", gde je kod kreiranja bitno da odaberete vašu organizaciju (a ne lični nalog) za kreiranje repozitorijuma.
6. Definisanje `development` grane za oba repozitorijuma i njihov push na centralni repozitorijum. Kada krene razvoj, feature grane će se izvlačiti iz `development` grane prateći standardan git workflow.
7. Kloniranje novo-kreiranih repozitorijuma kod sebe lokalno.

## 2. Kreiranje Trello table

Trello tabla predstavlja alat za praćenje i upravljanje radom na projektu. Njena struktura treba da odgovara potrebama projekta koji se razvija. Definisanje strukture podrazumeva kreiranje, imenovanje i raspored lista kartica na tabli. Tipična sturktura table koju ćemo mi koristiti podrazumeva sledeće liste:

- Backlog (Kolona koja sadrži kartice koje opisuju zahteve koje bismo želeli da rešimo)
- To-Do (Kolona koja sadrži kartice na kojima ćemo raditi u narendih par nedelja (takozvani "sprint"))
- In Progress (U ovoj koloni se nalaze kartice na kojima se trenutno radi)
- Review (Kartice koje su na reviziji od strane drugih članova tima treba smestiti u ovu kolonu)
- Done (Kartice koje su potpuno završene treba smestiti u ovu kolonu)

Šablon Trello table na osnovu kog se može napraviti tabla tvog tima se nalazi [ovde](https://trello.com/b/AejlmzUU/example-board). Prilikom kreiranja table možeš da analiziraš koje mogućnosti nudi jedna kartica (npr. labele, dodeljivanje članova tima, definisanje roka, opisa, komentara...).

# Snažan zalet
Timovi koji žele sebi da olakšaju ostatak prvog segmenta projekta mogu da se upoznaju sa serverskom i klijentskom aplikacijom.

Za upoznavanje serverske aplikacije, potrebno je rešiti **korak 0.** u [sledećem dokumentu](https://github.com/psw-ftn/supportive-information/blob/master/s1/w1/back-end.md#0-organizacija-i-pokretanje-projekta), što će rezultovati lokalnim pokretanjem aplikacije.

Za upoznavanje klijentrske aplikacije, potrebno je rešiti **korak 0.** u [sledećem dokumentu](https://github.com/psw-ftn/supportive-information/blob/master/s1/w1/front-end.md#0-organizacija-i-pokretanje-projekta), što će rezultovati lokalnim pokretanjem aplikacije.
