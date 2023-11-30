Poslednja nedelja drugog sprinta podrazumeva tri zadatka:

1. (Svi, raspoređeni u grupe od dva do tri člana tima) Razgovor sa krajnjim korisnicima i isprobavanje softvera.
2. (Svi) Backlog grooming spram svega naučenog o projektu.
3. (Svi) Revizija i retrospektiva sprinta, po uzoru na [prvi sprint](https://github.com/psw-ftn/supportive-information/blob/master/s1/w2/s1e-review-retrospective.md).
<br><br><br><br>
# 1. Isprobavanje softvera sa krajnjim korisnicima
Potrebno je pronaći i razgovarati sa šest do osam stakeholdera (minimum dva autora, ostalo turisti) koje ćemo pustiti da se igraju sa našim softverom. Potrebno je da za svaki razgovor bar dva člana tima budu prisutna, a najviše tri. Ovaj zadatak ima određena preklapanja sa zadatkom definisanja persona iz prvog sprinta.

Potrebno je da:

1. Pronađemo ljude iz naše okoline koji su pogodni za isprobavanje softvera, prateći [prethodne smernice](https://github.com/psw-ftn/supportive-information/blob/master/s1/w2/s1c-customers.md#1-pronalazak-pogodnih-ljudi-za-intervju). Idealno ćemo uključiti četiri korisnika sa kojim smo već ostvarili kontakt i dodati još dva do četiri nova.
2. Definišemo strukturu sesije (detalji ispod).
3. Sprovedemo sesiju, prateći [prethodne smernice](https://github.com/psw-ftn/supportive-information/blob/master/s1/w2/s1c-customers.md#3-sprovo%C4%91enje-intervjua), prilagođene za cilj sesije. **Napraviti fotografiju sa korisnikom**.
4. Dopunimo postojeće mape empatije i definišemo nove korisničke priče. Ne moramo da pravimo nove mape empatije za nove korisnike, već ćemo ažurirati postojeće mape spram novih uvida u stare korisnike. Korisničke priče ćemo izvući iz ideja za unapređenje i razvoj novih funkcionalnosti koje ćemo izvući iz sesije.
<br><br><br><br>

### 1.2 Definisanje strukture sesije
Cilj prvog intervjua je bio da razumemo poglede, iskustva, želje i potrebe naših korisnika, bez da ih opterećujemo detaljima našeg rešenja. Ova sesija produbljuje prethodni cilj, ali podrazumeva i davanje našeg softvera krajnjim korisnicima da se igraju sa njim.

Svaki tim može da definiše strukturu sesije spram svojih ideja, gde u nastavku slede bitni elementi koje bi vredelo uključiti u strukturu:

- Isticanje cilja sesije (kao vežba za projektni zadatak i prilika da se razume perspektiva krajnjeg korisnika za izradu korisnog softverskog rešenja).
- Upoznavanje korisnika sa ciljem aplikacije i koristi koju bi trebala njegova rola (autor ili turista) da izvuče iz nje.
- Najviše vremena odlazi na puštanje korisnika da se igra sa aplikacijom sa što manje smernica. Preporuka je da tim definiše redosled funkcionalnosti koje bi trebao korisnik da prođe, gde za svaku veću funkcionalnost treba istaći korisniku cilj koji želi da postigne kroz aplikaciju. U ovom koraku vredi istaći sledeće:
   - Pripremite početne podatke koji će postojati u aplikaciji koji su realistični i interesantni (npr. formirati `seed.sql` skriptu koja se na dalje može koristiti i za testiranje produkcije). Ovo je posebno bitno za turiste, a za autora treba da pripremimo podatke koji će olakšati rešavanje njegovih zadataka.
   - Bitno je naglasiti korisniku da nije kriv ako se ne snalazi, već da je to nedostatak aplikacije koji treba ispraviti.
   - Idealno će članovi tima samo posmatrati korisnika i beležiti tastere, menije i funkcionalnosti koje nisu dovoljno intuitivne, zadatke koje korisnik previše sporo rešava i ideje za unapređenje svega navedenog. Aktivnije se treba uključiti samo kod neintuitivnih funkcionalnosti poput `Position Simulatora`.
   - Pri definisanju zadataka koje će korisnik rešavati vodite računa o potrebnom vremenu da se reši zadatak, posebno kod autora. Definisanje ture sa 5 ključnih tački zahteva dosta više vremena i mašte nego tura sa 2 tačke. Ne mora svaka funkcionalnost da se prođe sa korisnikom, bitno je proći one koje očekujemo da će se najčešće koristiti.
   - U svakom momentu sesije (uvod, rad sa aplikacijom, završni razgovor) pazite da ne opteretite korisnika sa previše informacija i detalja.
- Posle rada sa aplikacijom, ostaviti dovoljno vremena da se saberu misli i prikupe ideje od korisnika kako bi se sistem mogao unaprediti. Obratiti pažnju na:
   - Deo aplikacije koji im se posebno svideo i zašto (ovo će nam otkriti šta vredi dalje da guramo),
   - Deo aplikacije koji im se nije svideo i zašto (ovo će nam otkriti šta treba preraditi, unaprediti ili napustiti),
   - Dodatne ideje koje imaju šta bi aplikacija mogla da podrži, a što trenutno ne podržava.

# 2. Backlog grooming
Nakon intervjua je potrebno da se ceo tim sastane kako biste sproveli _backlog grooming_ aktivnost putem kog će se definisati posao za naredni sprint. Da biste formirali kvalitetne korisničke priče, potrebno je da dopuniš razumevanje **[estimacije korisničkih priča](https://www.youtube.com/watch?v=xna-heGqXCc&list=PLWTyGVhcibjYc44t_AD6Sg0R4RhwMzRAB)** i analiziraš **[INVEST akronim](https://www.youtube.com/watch?v=nBE-6fMQxvs)** koji spaja sve što smo do sad obrađivali na temu kvalitetnih priča. Kao priprema za sastanak je dodatna preporuka da razmislite u kom pravcu biste želeli da se vaš softver razvija.

Cilj zadatka je da saberete sve što smo naučili o domenu problema i softverskom rešenju koje pravite, kako biste usmerili dalji razvoj softvera i definisali zadatke za naredni sprint. Konkretno, potrebno je da:

- Revidirate ciljeve vaše organizacije, gde je moguće da tim definiše više ciljeva (npr. 1-2 za svaku rolu - šta želi vaša organizacije da postigne za date korisnike). Ciljeve možete definisati kao kartice na Trellu u posebnu listu kartica koje nazivate "Ciljevi".
- Revidirate i dopunite velike Epice iz kojih ćete izvlačiti zahteve za naredni sprint. Svaki epic treba da ima checklistu, gde je svaka stavka checkliste jedna potencijalno veća kartica.
- Izdvojite INVEST kartice iz Epica sa ukupnom vrednošću od 16 do 20 story poena (koristite kartice iz prethodnog sprinta za uzor pri određivanju poena) koje će ceo tim rešavati u narednom sprintu.
