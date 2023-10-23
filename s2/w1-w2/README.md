Prve dve nedelje drugog sprinta su posvećenu razvoju složenih funkcionalnosti. Ovo podrazumeva:

1. Dekompoziciju složenih korisničkih priča na sitnije priče.
2. Planiranje posla na skali od dve nedelje.
3. Dizajniranje i implementacija agregata od više objekata.
4. Jedinično testiranje agregata i integraciono testiranje cele funkcionalnosti.

# 1. Dekompozicija složenih korisničkih priča i planiranje posla
U organizacijama koje prate Scrum radni okvir, _product owner_ rola je zadužena za sprovođenje aktivnosti _backlog grooming_. Ovo je kompozitna aktivnost koja uključuje više koraka, a jedan od tih koraka podrazumeva dekompoziciju velikih ideja za softver u manje korisničke priče. Do razvojnog tima često stižu korisničke priče koje su i dalje krupne i koje vredi usitniti tako da se dobije posao koji se rešava u rasponu od par dana.

Postoji više tehnika za dekompoziciju korisničkih priča, u zavisnosti od prirode same priče. Takođe postoji jedna tehnika koju moramo izbegavati i koja neće proizvesti korisne korisničke priče. Sledeća **[playlista](https://www.youtube.com/watch?v=cGKuogxAmT0&list=PLWTyGVhcibjZvbyNjq2I10K63QreUZIMc)** sabira nekoliko tehnika sa kojim treba da se upoznaš.

Razlaganje korisnički priča na sitnije zadatke smanjuje _rizik_ da se veća funkcionalnost neće implementirati i takođe olakšava identifikaciju spregnutosti između priča, čime lakše možemo da pravimo nezavisne (engl. _independent_) korisničke priče.

Većina korisničkih priča koje smo planirali u drugom sprintu podrazumevaju rad od bar dve čovek-nedelje (pod čovek-nedelja mislimo rad od 5-6 sati u sklopu nedelje od strane jednog studenta). Neke zahtevaju pet takvih nedelja.

Da bismo dekomponovali prethodne priče, tim studenata može da prati sledeći algoritam:

1. Klasterovanje priča oko modula koji će se primarno menjati (Stakeholders, Tours, Blog) i podela velikog tima na manje timove za svaki modul. Ako tim nije siguran kom modulu pripada neka kartica, može da konsultuje **[prethodne materijale za izbor modula](https://github.com/psw-ftn/supportive-information/blob/master/s1/w1/back-end.md#a-izbor-modula)**.
2. U okviru svakog podtima, diskusija kako bi se pojedine korisničke priče mogle razložiti primenom tehnika u video materijalima.
3. Formiranje kartica koje uzimaju najviše 2 čovek-nedelje da se reše.

# 2. Planiranje dvonedeljnog posla
Prost proces planiranja podrazumeva sabiranje zadataka koje treba rešiti, dodeljivanje resursa (ljudi) koji će ih rešiti i organizacija svega na vremenskom toku. Naprednije planiranje podrazumeva i analizu rizika, gde se plan unapređuje tako da se rizici umanje.

Rizik je mogućnost da se nešto loše desi. Kada radimo sa novom tehnologijom, rizik je da se nećemo snaći sa njom za dato vreme. Ako pametno planiramo, takav zadatak ćemo staviti na početak našeg rada kako bismo na vreme videli da li će se rizik ostvariti. Ako se desi (nismo se snašli) možemo da reagujemo i da izdvojimo dodatno vreme za dati posao ili da tražimo pomoć. Ako nespretno planiramo, ostavićemo rizične stvari za poslednji momenat i biti u problemu ako se rizik ostvari.

Plan potreban da se reši zadatak sa malo nepoznanica, od strane jedne osobe i u roku od dva sata je značajno manje _rizičan_ nego plan koji se pravi za projekat na kom radi 20 ljudi 2 godine. Rešavanje zadataka od strane 10 ljudi kroz 2 nedelje ima više rizika.

Sa skupom sitnih korisnička priča, potrebno je da dogovorite ko će šta da radi i u kom redosledu. Dogovor se može rešavati na nivou podtima (stvorenog u koraku 1.1). Pri planiranju, uzmite u obzir sledeće:

1. Postoje tri tipa zavisnosti između kartica koji različito utiču na planiranje:
   1. Dve kartice su _potpuno nezavisne_ kada se rešavaju bez ikakvog uticaja jedna na drugu.
   _Primer_: "ocenjivanje bloga" nema dodira sa "objavljivanjem ture".
   _Uticaj na planiranje_: Dati tip zavisnosti ne utiče na planiranje razvoja.
   2. Dve kartice su _suštinski nezavisne_ kada postoji slaba zavisnost između njih koja se lako može rešiti na početku ili kraju razvoja.
   _Primer_: "simulator pozicije" definiše poziciju turiste koja je potrebna "izvedbi ture". Nakon što je uvedena klasa TouristPosition, moguće je manipulisati podatkom u bazi za potrebe razvoja "izvedbe ture" i pre nego što je kompletan "simulator" gotov).
   _Uticaj na planiranje_: Za dati tip zavisnosti je potrebno iskordinisati pola sata na početku ili kraju razvoja da se integrišu funkcije.
   3. Dve kartice su _zavisne_ kada je potrebno više sati rada da se integrišu ako se rade u paraleli.
   _Uticaj na planiranje_: Prvo pokušavamo da dekomponujemo zavisne priče da se izdvoji što manja smislena celina koja je deljena i da se ona prva implementira. U svakom slučaju sekvenciramo posao da se prvo reši zadatak od kog ostali zavise i **ovakve zadatke treba rešiti u prvoj nedelji**.
2. Smisleno je dodeliti ljudima koji su već radili sa nekim modulom zadatak da nastave da rade sa tim modulom. Na većim projektima se timovi formiraju spram modula modularnog monolita (ili servisa kod mikroservisnih arhitektura).
3. Skroz nove vrste zadataka (npr. integracija sa Google Analytics) unose rizik od nepoznatog i ima smisla da se rade pre nego kasnije (ne nužno cela kartica, ali svakako inicijalna integracija).
4. Čak i poznat posao ima iherentan rizik da će nešto iskočiti. Možemo se prehladiti se može pojaviti neočekivana situacija u privatnom životu koju moramo da rešavamo. Bolje nam je da odvadimo veću količinu posla u periodu kada je mir. Zbog toga vredi da prva nedelja razvoja podrazumeva da se više posla uradi nego što ostane za drugu. Ako se ostvari rizik, imamo dovoljno vremena u drugoj nedelji da radimo na zadacima. 

Uzimajući sve prethodno u obzir, možemo da raspodelimo posao na nivou tima i ugovorimo u kalendaru ključne rokove da izbegnemo konflikte zbog međuzavisnog rada i da stignemo da potražimo pomoć ako se neki rizik ostvari.

# 3. Dizajniranje i implementacija agregata
TODO

# 4. Testiranje agregata
TODO
