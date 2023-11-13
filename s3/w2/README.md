U drugoj nedelji trećeg sprinta svaki član tima radi na razvoju nove funkcionalnosti. Kroz ovu nedelju nam je cilj da podignemo proces razvoja softvera na sledeći stepen zrelosti tako što ćemo primeniti razvoj vođen testovima (engl. _test-driven development_, TDD).

# Razvoj vođen testovima
Do sada smo implementirali testove pred kraj razvoja funkcionalnosti. TDD predstavlja alternativan pristup, gde prvo implementiramo test (koji nužno pada), nakon čega implementiramo funkciju tako da test prolazi. Možemo pogledati sledeće materijale da bolje razumemo:

- [Kako izgleda TDD proces?](https://youtu.be/fuRJA-0wbjo)
- [Kako se TDD integriše u Scrum radni okvir?](https://youtu.be/giztcCGWkTQ)
- (Opciono) [Kako da pišemo kvalitetne testove?](https://www.youtube.com/watch?v=8JlYqN1dhHw&list=PLWTyGVhcibjYJYZZwX2VPt_-ycRBA0U7R)

# Razvoj složenih funkcionalnosti po TDDu
Polazeći od procesa koji smo definisali u [prethodnom sprintu](https://github.com/psw-ftn/supportive-information/tree/master/s2/w1-w2), pratimo sledeći algoritam u ovom:

1. Dekompozicija korisničkih priča i podela posla na članove tima.
2. Sređivanje kartice koja definiše zadatak.
3. Izrada koda za serversku (backend) aplikaciju. **Ovaj deo menjamo**.
4. Izrada koda za klijentsku (frontend) aplikaciju.
5. Otvaranje i dokumentovanje pull requesta.
6. Prepuštanje kolegi da revidira novi kod i odgovaranje na komentare.
7. Zatvaranje pull requesta.

### Razvoj serverske aplikacije vođen testovima
Do sada smo kretali od domenskog sloja kada treba implementirati novu funkcionalnost. Prateći TDD, menjamo razvoj da prati sledeći algoritam:

1. Analiziramo korisničku priču kako bismo identifikovali kakve ulazne podatke treba poslati serverskoj aplikaciji i kakav rezultat se očekuje (da li u obliku _responsa_ ili izmene sadržaja baze). Iz ove perspektive posmatramo kompletnu serversku aplikaciju kao "crnu kutiju", gde nas ne interesuje šta se dešava u njoj već samo šta ulazi i šta izlazi iz nje.
2. Po potrebi definišemo DTO klase za ulazne i izlazne podatke u okviru modula koji treba da ispuni zahtev. Ove klase se mapiraju na očekivanja korisničke priče i potrebno je razmisliti o njihovoj strukturi (koji podaci će biti potrebni da se ispuni zahtev?).
3. Po potrebi pravimo kontroler koji treba da podrži novi zahtev. Definišemo kontrolersku metodu koju hoćemo da testiramo, tako da metoda ima jednu liniju koda: `throw new NotImplementedException();`
4. **Definišemo testnu klasu i test koji poziva novu metodu kontrolera**. U _assert_ sekciji test treba za početak da proveri da li se dobar _response_ dobija kao rezultat poziva operacije. Ako postoji potreba da se proveri sadržaj baze, ovo se definiše kasnije. Definisan test pada pri pokretanju. U ovom momentu **obavezno pravimo test: commit**.
5. Prelazimo na regularnu implementaciju, gde po potrebi definišemo ili proširujemo interfejse servisa, njihove implementacije, domenski model i repozitorijum.
6. Ako proširujemo domenski model sa logikom koju vredi pokriti jediničnim testiranjem, definišemo metodu sa linijom koda: `throw new NotImplementedException();` i definišemo testnu klasu koja će sadržati jedinične testove koji pokrivaju sve varijacije na rezultat nove metode. Zatim implementiramo metodu do momenta kada testovi prolaze. Tada **opciono pravimo feat: commit koji uključuje domensku klasu i test**.
7. Korake 5 i 7 ponavljamo sve dok test iz koraka 4 ne prolazi i ostali testovi ne padaju. U tom momentu možemo proširiti test iz koraka 4 da proverimo da li se u bazi podaci ispravno menjaju.
8. Kada svi testovi prolaze, možemo po potrebi da refaktorišemo novi kod, gde je bitno da se uverimo da testovi prolaze posle svakog refaktorisanja.
9. Na kraju **obavezno pravimo feat: commit**.

**[Sledeći video](https://www.youtube.com/watch?v=4qXWSWx4Ap0)** ilustruje kompletan primer prethodnog procesa za korisničku priču iz domena upravljanja rasporedom prostorije.

**Napomena**: Prethodne smernice su jednostavne u odnosu na prethodne sprintove i mogu da daju iluziju da je sam zadatak jednostavan. To nije slučaj. Prvo, dekompozicija početnih priča je izazovna i vredi pažljivo uraditi taj deo da se izbegnu međuzavisnosti. Drugo, dizajniranje novih agregata nije trivijalno i kroz rad sa njima ćeš utvrditi veštine iz prethodnog sprinta. Treće, rad po TDDu je isprva kontraintuitivan i za očekivati je da će te usporiti.
