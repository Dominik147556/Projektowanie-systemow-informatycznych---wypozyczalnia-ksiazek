# BookFlow - wymagania v0.1

> Dokument roboczy. Wersja 0 ponizej jest **przykladowa propozycja do samodzielnego opracowania bez AI**, a nie zapisem rzeczywistej pracy zespolu. Wymagania z symulacji klienta wymagaja potwierdzenia.

## 1. Temat, cel i granica systemu
System obslugi fizycznych egzemplarzy ksiazek w jednej bibliotece. W granicach: katalog i status egzemplarzy, konta czytelnikow, rezerwacje, kolejka, wypozyczenia, zwroty, przedluzenia i powiadomienia. Poza granica: dostarczanie wiadomosci przez usluge pocztowa, platnosci online, zakup ksiazek, e-booki i integracje miedzybiblioteczne.

## 2. Aktorzy i systemy zewnetrzne
| Typ | Aktor / system | Potrzeba lub rola |
|---|---|---|
| Czlowiek | Czytelnik | Wyszukac ksiazke, zarezerwowac egzemplarz, sprawdzic termin zwrotu. |
| Czlowiek | Bibliotekarz | Wydac i przyjac egzemplarz oraz odnotowac jego stan. |
| Czlowiek | Administrator | Zarzadzac uprawnieniami i kontami pracownikow. |
| Czlowiek | Kierownik biblioteki | Sprawdzic zalegle zwroty i obciazenie zbiorow. |
| Zewnetrzny | Usluga poczty e-mail | Dostarcza powiadomienia; jej awaria nie moze anulowac wypozyczenia. |

## 3. Wersja 0 - bez AI (przykladowa, do zastapienia wlasna)
1. Czytelnik moze przeszukac katalog po tytule.
2. Czytelnik moze filtrowac katalog po autorze.
3. Czytelnik widzi, czy egzemplarz jest dostepny.
4. Czytelnik moze zarezerwowac dostepna ksiazke.
5. Bibliotekarz moze wydac zarezerwowany egzemplarz.
6. Bibliotekarz moze zarejestrowac zwrot ksiazki.
7. Czytelnik widzi liste swoich wypozyczen.
8. Czytelnik widzi terminy zwrotu.
9. Bibliotekarz moze dodawac egzemplarze do katalogu.
10. Administrator moze blokowac konta uzytkownikow.

## 4. Historyjki uzytkownika (MoSCoW)

### R-01 Wyszukiwanie ksiazki (Must)
Jako czytelnik chce wyszukac ksiazke po tytule, aby szybko znalezc interesujaca mnie pozycje.
- **Zakladajac**, ze w katalogu jest ksiazka "Atlas chmur", **gdy** wpisuje "Atlas", **wtedy** otrzymuje ja w wynikach.
- **Blad:** Zakladajac, ze nie ma pasujacych pozycji, gdy wpisuje nieznany tytul, wtedy widze komunikat "Brak wynikow".

### R-02 Sprawdzanie dostepnosci (Must)
Jako czytelnik chce sprawdzic status konkretnego egzemplarza, aby wiedziec, czy moge go wypozyczyc.
- Zakladajac, ze egzemplarz jest na polce, gdy otwieram szczegoly ksiazki, wtedy widze status "Dostepny".
- **Blad:** Zakladajac, ze egzemplarz jest wypozyczony, gdy otwieram szczegoly, wtedy widze "Niedostepny" i nie moge go bezposrednio zarezerwowac jako dostepnego.

### R-03 Rezerwacja egzemplarza (Must)
Jako czytelnik chce zarezerwowac dostepny egzemplarz, aby odebrac go w bibliotece.
- Zakladajac, ze jestem aktywnym czytelnikiem i egzemplarz jest dostepny, gdy wybieram "Rezerwuj", wtedy system tworzy jedna aktywna rezerwacje z terminem odbioru.
- **Blad:** Zakladajac, ze inna osoba zarezerwowala egzemplarz chwile wczesniej, gdy zatwierdzam rezerwacje, wtedy system odrzuca probe bez tworzenia drugiej aktywnej rezerwacji.

### R-04 Wydanie ksiazki (Must)
Jako bibliotekarz chce zarejestrowac wydanie egzemplarza, aby ustalic termin jego zwrotu.
- Zakladajac, ze czytelnik ma wazna rezerwacje, gdy potwierdzam wydanie, wtedy rezerwacja zmienia status na zrealizowana, a wypozyczenie ma termin zwrotu za 21 dni.
- **Blad:** Zakladajac, ze egzemplarz ma juz aktywne wypozyczenie, gdy probuje go wydac ponownie, wtedy system blokuje operacje.

### R-05 Rejestracja zwrotu (Must)
Jako bibliotekarz chce potwierdzic zwrot egzemplarza, aby zaktualizowac jego dostepnosc.
- Zakladajac, ze egzemplarz jest wypozyczony, gdy rejestruje zwrot, wtedy wypozyczenie zostaje zamkniete, a egzemplarz trafia do dostepnych albo do obslugi kolejki.
- **Blad:** Zakladajac, ze zwrot zostal juz zarejestrowany, gdy ponawiam operacje, wtedy system nie tworzy drugiego zwrotu.

### R-06 Moje wypozyczenia (Should)
Jako czytelnik chce widziec wlasne wypozyczenia i terminy, aby planowac zwroty.
- Zakladajac, ze mam dwie wypozyczone ksiazki, gdy otwieram "Moje konto", wtedy widze oba tytuly i daty zwrotu.

### R-07 Przedluzenie terminu (Should)
Jako czytelnik chce raz przedluzyc wypozyczenie o 14 dni, aby dokonczyc lekture.
- Zakladajac, ze termin nie minal, nie ma kolejki i nie przedluzalem ksiazki, gdy wybieram "Przedluz", wtedy termin rosnie o 14 dni.
- Zakladajac, ze inna osoba oczekuje na egzemplarz, gdy probuje przedluzyc, wtedy system odmawia i podaje powod.

### R-08 Kolejka oczekujacych (Should)
Jako czytelnik chce zapisac sie do kolejki na wypozyczona ksiazke, aby dostac szanse jej odbioru.
- Zakladajac, ze wszystkie egzemplarze tytulu sa wypozyczone, gdy dolaczam do kolejki, wtedy system pokazuje moja pozycje.
- Zakladajac, ze jestem juz w kolejce, gdy ponownie klikam "Dolacz", wtedy nie powstaje duplikat.

### R-09 Powiadomienie o terminie (Should)
Jako czytelnik chce dostac przypomnienie 3 dni przed zwrotem, aby uniknac opoznienia.
- Zakladajac, ze mam aktywne wypozyczenie i poprawny adres e-mail, gdy do terminu pozostaja 3 dni, wtedy system zleca wyslanie jednego przypomnienia.

### R-10 Oznaczenie utraty egzemplarza (Could)
Jako bibliotekarz chce oznaczyc egzemplarz jako zagubiony, aby nie byl oferowany do rezerwacji.
- Zakladajac, ze egzemplarz ma status "Zagubiony", gdy czytelnik przeglada katalog, wtedy nie moze go zarezerwowac.

### R-11 Raport przeterminowanych zwrotow (Could)
Jako kierownik biblioteki chce wyswietlic liste zaleglych wypozyczen, aby planowac kontakt z czytelnikami.
- Zakladajac, ze sa wypozyczenia po terminie, gdy uruchamiam raport, wtedy widze identyfikator wypozyczenia i liczbe dni opoznienia.

### R-12 Zarzadzanie kontami bibliotekarzy (Should)
Jako administrator chce nadawac i odbierac role bibliotekarza, aby kontrolowac dostep do operacji wydania i zwrotu.
- Zakladajac, ze konto ma role czytelnika, gdy probuje zarejestrowac wydanie, wtedy operacja jest zabroniona.

## 5. Wymagania niefunkcjonalne
| ID | Obszar | Mierzalne wymaganie | Weryfikacja |
|---|---|---|---|
| NF-01 | Wydajnosc | 95% wyszukiwan konczy sie w czasie ponizej 2 s przy 100 jednoczesnych uzytkownikach i katalogu 50 000 egzemplarzy. | Test obciazeniowy. |
| NF-02 | Dostepnosc | Dostepnosc uslugi co najmniej 99,5% miesiecznie, z wylaczeniem uzgodnionych okien serwisowych. | Monitoring miesieczny. |
| NF-03 | Bezpieczenstwo | Konto blokuje logowanie na 15 min po 5 nieudanych probach w ciagu 10 min. | Test bezpieczenstwa. |
| NF-04 | Dostepnosc cyfrowa | Kluczowe sciezki: wyszukiwanie, rezerwacja i konto spelniaja WCAG 2.2 AA (0 krytycznych naruszen w audycie). | Audyt WCAG i test klawiatury. |
| NF-05 | Prywatnosc | Po 30 dniach od zamkniecia konta dane kontaktowe sa usuwane lub anonimizowane, o ile nie zachodzi obowiazek dalszego przechowywania. | Test retencji i przeglad polityki danych. |
| NF-06 | Integralnosc | Przy 1000 rownoleglych probach rezerwacji tego samego egzemplarza powstaje najwyzej 1 aktywna rezerwacja. | Test wspolbieznosci. |

## 6. Pytania otwarte do potwierdzenia z klientem
- Czy termin wypozyczenia wynosi 21 dni dla wszystkich czytelnikow?
- Czy rezerwacja wygasa po 48 godzinach od powiadomienia?
- Czy uzytkownik moze miec maksymalnie 5 aktywnych wypozyczen?
- Czy zagubienie ksiazki wiaze sie z oplata? (platnosci online sa poza zakresem.)
- Czy przypomnienia e-mail wymagaja osobnej zgody, czy wynikaja z obslugi konta?
