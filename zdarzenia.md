# BookFlow - event storming - Lab 2

> Przykladowa propozycja zdarzen do przeprowadzenia i zatwierdzenia przez zespol bez AI. Nie jest zapisem rzeczywistej sesji na karteczkach.

## Granica
Obslugujemy fizyczne egzemplarze ksiazek w jednej bibliotece. E-mail jest usluga zewnetrzna. Platnosci online i e-booki sa poza zakresem.

## Os zdarzen
| Kolejnosc | Kto wywoluje | Polecenie | Zdarzenie (czas przeszly) |
|---|---|---|---|
| 1 | Bibliotekarz | Dodaj egzemplarz | Egzemplarz dodany do katalogu |
| 2 | Czytelnik | Wyszukaj ksiazke | Ksiazka odnaleziona w katalogu |
| 3 | Czytelnik | Sprawdz dostepnosc | Dostepnosc egzemplarza sprawdzona |
| 4 | Czytelnik | Zarezerwuj egzemplarz | Rezerwacja zlozona |
| 5 | System | Potwierdz dostepnosc | Rezerwacja potwierdzona |
| 6 | System | Zlec potwierdzenie | Powiadomienie o rezerwacji zlecone |
| 7 | Bibliotekarz | Wydaj egzemplarz | Egzemplarz wydany |
| 8 | System | Utworz wypozyczenie | Wypozyczenie zarejestrowane |
| 9 | System | Ustal termin zwrotu | Termin zwrotu ustalony |
| 10 | Czytelnik | Przedluz wypozyczenie | Wypozyczenie przedluzone |
| 11 | System | Zlec przypomnienie | Przypomnienie o zwrocie zlecone |
| 12 | Bibliotekarz | Przyjmij zwrot | Zwrot egzemplarza zarejestrowany |
| 13 | System | Zamknij wypozyczenie | Wypozyczenie zamkniete |
| 14 | System | Zwolnij egzemplarz | Egzemplarz udostepniony do rezerwacji |

## Scenariusze alternatywne
| Kto | Polecenie | Zdarzenie |
|---|---|---|
| Czytelnik | Zarezerwuj zajety egzemplarz | Rezerwacja odrzucona z powodu konfliktu |
| Czytelnik | Dolacz do kolejki | Czytelnik dodany do kolejki |
| System | Przydziel zwrocony egzemplarz | Egzemplarz przydzielony osobie z kolejki |
| System | Wygas nieodebrana rezerwacje | Rezerwacja wygasla |
| Bibliotekarz | Oznacz utrate | Egzemplarz oznaczony jako zagubiony |
| System | Zlec e-mail | Wysylka powiadomienia nie powiodla sie |

## Pytania otwarte (czerwone karteczki)
1. Czy rezerwacja ma termin odbioru 48 godzin? Do potwierdzenia.
2. Czy mozna zarezerwowac ksiazke bez logowania? Proponowane: nie.
3. Czy kolejka dotyczy tytulu czy konkretnego egzemplarza? Do uzgodnienia.
4. Co zrobic, gdy usluga e-mail nie dziala? Proponowane: zachowac rezerwacje i ponowic wysylke.
5. Kto moze anulowac rezerwacje po jej potwierdzeniu? Do uzgodnienia.
6. Czy wypozyczenie bez rezerwacji jest dozwolone przy ladzie biblioteki? Do uzgodnienia.

## Do wykonania na zajeciach
Przeprowadzic event storming bez AI, uzgodnic nazwy i kolejnosc, zrobic zdjecie tablicy i zaktualizowac te tabele.
