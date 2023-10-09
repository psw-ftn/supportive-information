Sav softver koji programiramo predstavlja nekakvo *rešenje*. Rešenje podrazumeva da postoji *problem* koji rešavamo. Excel koji sadrži stotine hiljada redova treba agregirati u neku bazu podataka. Ovo je problem. Python skripta koja čita dati Excel, primenjuje agregacionu funkciju i čuva rezultat u bazi podataka je moguće rešenje tog problema.

Ako pogrešno razumemo problem koji rešavamo, nije bitno koliko je kvalitetan naš kod ili upotrebljiv naš korisnički interfejs - pravimo rešenje za pogrešan problem, čime pravimo beskoristan softver. Sa druge strane, kada dobro razumemo problem nije toliko bitno koliko će kvalitetno biti naše rešenje - ako je u razumnoj meri upotrebljivo, biće korisno.

Pošto smo inženjeri, imamo tendenciju da prvo razmišljamo o rešenju pre nego što smo dobro razumeli problem. Formiramo preduzetničke ideje i vizije za naš proizvod tako što prvo zamišljamo sva svojstva našeg softverskog rešenja. Ovo je opasno jer u većini slučajeva (šacometrijski - 99.9%) ne razumemo problem i potrebe korisnika i možemo napraviti složeno softversko rešenje koje nije korisno.

Kroz kurs ćemo razgovarati sa krajnjim korisnicima u nekoliko navrata kako bismo razvili veštine za razumevanje problema koji korisnici imaju, što će nam pomoći da pravimo korisna rešenja.

# Definisanje persone

*Persona* predstavlja sliku našeg krajnjeg korisnika koju imamo na umu kad god pričamo o njihovim potrebama. Primere persona smo videli na uvodnim predavanjima (Ana, David, Vanja), a isto i kada smo istakli različite tipove studenata pre nekog vremena (Alisa, Bob, Džon).

Naše trenutne persone su izuzetno proste i svode se na ime (Ana, David, Vanja) i rolu (Autor, Turista, Administrator) koju imaju. Potrebno je da ih obogatimo detaljima koji će nam pomoći da razumemo perspektivu korisnika, njihove potrebe i probleme, spram kojih ćemo usmeriti razvoj našeg softverskog rešenja u kasnijim sprintovima. Ovo je posebno bitno za persone Autora i Turiste zbog kojih ćemo "dobijati pare", dok su Administratori "naši ljudi".

Da bismo produbili naše persone, potrebno je da:

1. Napravimo inicijalne razgovore sa ljudima iz naše okoline, kako bismo identifikovali bar jednog dobrog kandidata za Autora i bar dva dobra kandidata za Turiste.
2. Definišemo strukturu intervjua koji ćemo održati sa svakim korisnikom.
3. Sprovedemo intervju.
4. Analiziramo zapis intervjua i kreiramo profil za svaku personu.
