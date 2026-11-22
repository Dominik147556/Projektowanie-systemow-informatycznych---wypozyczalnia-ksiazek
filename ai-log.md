# Dziennik uzycia AI - Lab 1

> **Uwaga:** ponizszy wywiad to przygotowana przez AI **symulacja przykladowa**, a nie zapis faktycznie przeprowadzonego wywiadu zespolu. Pytania i decyzje nalezy zweryfikowac podczas cwiczenia. "Klient-AI" nie zastepuje prawdziwego klienta.

## 1. Symulacja wywiadu: bibliotekarka zarzadzajaca wypozyczeniami
**Prompt:** "Jestes kierowniczka niewielkiej biblioteki. Projektujemy system wypozyczania fizycznych ksiazek. Odpowiadaj tylko na zadane pytania, czasem niekonsekwentnie, nie proponuj technologii. Po 10 pytaniach ocen luki."

1. **Jak dzis wyglada wypozyczanie?** - Czytelnik wybiera ksiazke, bibliotekarz zapisuje wydanie i termin zwrotu.
2. **Co najbardziej przeszkadza w obecnym procesie?** - Trudno sprawdzic, kto ma egzemplarz i kiedy wroci.
3. **Czy rezerwowac mozna kazda ksiazke?** - Tylko dostepna, ale dobrze byloby tez zapisac sie na zajeta.
4. **Co, jesli dwie osoby rezerwuja ostatni egzemplarz rownoczesnie?** - Tylko jedna moze otrzymac potwierdzenie.
5. **Jak dlugo czytelnik ma na odbior?** - Zwykle dwa dni, ale przy swietach moze byc inaczej.
6. **Co, jesli ksiazka nie wroci w terminie?** - Chcemy widziec opoznienie i wysylac przypomnienie.
7. **Czy wolno przedluzac wypozyczenia?** - Tak, chyba ze ktos juz czeka. Nie jestem pewna liczby przedluzen.
8. **Co zrobic z uszkodzona albo zagubiona ksiazka?** - Trzeba ja wylaczyc z dostepnych egzemplarzy i zapisac przyczyne.
9. **Kto moze wydac ksiazke?** - Tylko pracownik biblioteki; czytelnik sam moze ja zarezerwowac.
10. **Co, jesli e-mail z powiadomieniem nie dotrze?** - Sama rezerwacja musi pozostac wazna; pracownik powinien widziec status powiadomienia.

**Ocena symulowanego klienta:** Nie zapytano o limit wypozyczen na osobe, sposob potwierdzania tozsamosci przy odbiorze, usuwanie danych po zamknieciu konta, dni wolne i zasady naliczania oplat. Odpowiedz o czasie odbioru jest niejednoznaczna - wymaga decyzji wlasciciela procesu.

## 2. Co wniosla symulacja AI-klienta
- Kolejka na niedostepny tytul (R-08) - zrodlo: klient-AI; do potwierdzenia.
- Zasada braku podwojnej rezerwacji (R-03, NF-06) - zrodlo: klient-AI; do potwierdzenia.
- Przedluzanie tylko bez kolejki (R-07) - zrodlo: klient-AI; do potwierdzenia.
- Oznaczanie egzemplarzy zagubionych (R-10) - zrodlo: klient-AI; do potwierdzenia.
- Niezaleznosc rezerwacji od dostarczenia e-maila - zrodlo: klient-AI; do potwierdzenia.

## 3. AI jako lowca luk - trzy historyjki Must
Ponizsze propozycje sa przykladowym wynikiem analizy AI. Przy kazdej historyjce podano 15 potencjalnych przypadkow i decyzje; **D** = dopisac kryterium, **N** = rozwazyc nowa historyjke, **O** = odrzucic w obecnym zakresie.

### R-03 Rezerwacja
1. Dwoch czytelnikow klika jednoczesnie - D, wyscig.
2. Czytelnik klika dwukrotnie - D, duplikat.
3. Polaczenie zrywa sie po zapisie - D, niepewny wynik.
4. Konto zostalo zablokowane - D, brak uprawnien.
5. Egzemplarz oznaczono jako zagubiony - D, zmiana statusu.
6. Rezerwacja wygasla podczas potwierdzania - D, uplyw czasu.
7. Czytelnik ma juz rezerwacje tego egzemplarza - D, duplikat.
8. Bibliotekarz wydal ksiazke bezposrednio - D, zmiana dostepnosci.
9. Biblioteka jest zamknieta w terminie odbioru - N, kalendarz.
10. Czytelnik ma zalegle zwroty - N, polityka blokad.
11. Rezerwacja dotyczy tytulu bez egzemplarzy - D, brak zasobu.
12. E-mail nie dociera - D, awaria integracji.
13. Uzytkownik rezerwuje 1000 ksiazek - N, limity.
14. Czytelnik chce wysylki kurierem - O, poza zakresem.
15. Czytelnik chce wypozyczyc e-book - O, poza zakresem.

### R-04 Wydanie
1. Ten sam egzemplarz wydawany dwukrotnie - D, duplikat.
2. Rezerwacja juz wygasla - D, stan nieaktualny.
3. Konto czytelnika zablokowane - D, uprawnienia.
4. Czytelnik podaje bledny identyfikator - D, identyfikacja.
5. Ksiazka fizycznie zaginela z polki - D, rozbieznosc.
6. Termin wypada w swieto - N, kalendarz.
7. Brak dostepu do systemu - N, procedura awaryjna.
8. Bibliotekarz klika "Wydaj" dwa razy - D, idempotencja.
9. Egzemplarz ma status uszkodzony - D, stan zasobu.
10. Czytelnik przekroczyl limit wypozyczen - N, polityka limitow.
11. Dwie osoby probuja wydac ten sam egzemplarz - D, wspolbieznosc.
12. Rezerwacja nalezy do innej osoby - D, zgodnosc danych.
13. Czytelnik prosi o przedluzenie przed wydaniem - O, niewlasciwy etap.
14. Bibliotekarz chce wydac e-book - O, poza zakresem.
15. Uzytkownik ma niezweryfikowane konto - D, identyfikacja.

### R-05 Zwrot
1. Zwrot tego samego egzemplarza dwa razy - D, duplikat.
2. Egzemplarz nie figuruje jako wypozyczony - D, niezgodnosc.
3. Zwrot nastepuje po terminie - D, opoznienie.
4. Egzemplarz jest uszkodzony - D, stan.
5. Jest kolejka oczekujacych - D, nastepny czytelnik.
6. E-mail do kolejnej osoby nie dociera - D, integracja.
7. Zwrot rejestruja dwaj pracownicy rownoczesnie - D, wspolbieznosc.
8. Czytelnik oddaje inny egzemplarz tego tytulu - D, identyfikator.
9. Zwrot nastepuje w dniu zamkniecia biblioteki - N, wrzutnia.
10. Ksiazka zostala wczesniej zgloszona jako zagubiona - D, konflikt statusow.
11. Zwrocona ksiazka ma brakujace strony - D, uszkodzenie.
12. Czytelnik zada zwrotu oplaty karta - O, platnosci poza zakresem.
13. Pracownik pomylil egzemplarz - D, korekta operacji.
14. Zwrot zapisano, ale ekran sie zawiesil - D, ponowienie.
15. Ksiazka pochodzi z innej biblioteki - O, poza zakresem.

**Przykladowe dodatkowe kryteria:** R-03: ponowienie zadania z tym samym identyfikatorem nie tworzy drugiej rezerwacji. R-04: wydanie jest zabronione, jesli rezerwacja nalezy do innego czytelnika. R-05: przy aktywnej kolejce zwrot nie ustawia egzemplarza jako swobodnie dostepnego.

## 4. Porownanie i refleksja
**Przykladowe zestawienie, nie wynik pomiaru zespolu:** 10/10 wymagan poczatkowych zachowano w projekcie lub jego rozszerzeniach; 5 obszarow dodano dzieki symulacji; 2 propozycje AI (wysylka kurierem i e-booki) odrzucono jako poza zakresem. Liczby nalezy zaktualizowac po rzeczywistym cwiczeniu.

**Refleksja (3 zdania):** AI pomoglo wskazac konflikty rownoczesnych rezerwacji, problemy z kolejka i sytuacje awaryjne, ktore latwo przeoczyc przy opisie podstawowych funkcji. Jednoczesnie proponowalo funkcje wykraczajace poza zakres fizycznej wypozyczalni, wiec nie kazda sugestie nalezy uznawac za wymaganie. Nadal trzeba uzgodnic z prawdziwym interesariuszem limity wypozyczen, terminy odbioru i zasady postepowania z zagubionymi ksiazkami.
