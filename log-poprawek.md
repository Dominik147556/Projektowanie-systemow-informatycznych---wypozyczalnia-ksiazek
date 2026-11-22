# BookFlow - log poprawek modelu - Lab 2

> Ponizsze wpisy dokumentuja proponowane poprawki podczas przygotowania szkicu AI. Nie sa recenzja rzeczywistego sasiedniego zespolu.

| Nr | Diagram | Co zmieniono wzgledem wstepnego szkicu | Dlaczego |
|---|---|---|---|
| 1 | C4 poziom 1 | Dodano kierownika biblioteki | Wystepuje jako aktor w wymaganiach Lab 1. |
| 2 | C4 poziom 1 | Oznaczono poczte jako system zewnetrzny | Dostarczanie e-maili jest poza granica BookFlow. |
| 3 | C4 poziom 2 | Rozdzielono API, kolejke i pracownika powiadomien | Awaria poczty nie moze cofnac rezerwacji. |
| 4 | Sekwencja rezerwacji | Dodano sprawdzenie aktywnego konta | R-03 wymaga aktywnego czytelnika. |
| 5 | Sekwencja konfliktu | Dodano atomowa kontrole zajecia egzemplarza | NF-06 wymaga najwyzej jednej aktywnej rezerwacji. |
| 6 | Maszyna stanow | Rozdzielono rezerwacje zrealizowana od wypozyczenia | Wydanie egzemplarza zamyka rezerwacje, a rozpoczyna wypozyczenie. |
| 7 | Maszyna stanow | Dodano wygasniecie i anulowanie | Model musi uwzgledniac nieodebrana rezerwacje i jej zakonczenie. |

## Recenzja krzyzowa - do uzupelnienia po zajeciach
Wymagana jest rzeczywista wymiana repozytoriow, zalozenie 3 issues innemu zespolowi i odpowiedz na otrzymane uwagi. Tego etapu nie wykonano.

| Issue | Link | Uwaga otrzymana lub wyslana | Decyzja | Commit |
|---|---|---|---|---|
| 1 | [uzupelnic] | [uzupelnic] | [uzupelnic] | [uzupelnic] |
| 2 | [uzupelnic] | [uzupelnic] | [uzupelnic] | [uzupelnic] |
| 3 | [uzupelnic] | [uzupelnic] | [uzupelnic] | [uzupelnic] |

## Kontrola szesciu pytan
1. Czy strzalki sa nazwane? Tak - w szkicach.
2. Czy nazwy pochodza z domeny? Tak - rezerwacja, egzemplarz, wydanie, zwrot.
3. Czy granica systemu jest jawna? Tak - w C4.
4. Czy diagramy sa zgodne z kryteriami? R-03 i NF-06 - tak, do zatwierdzenia.
5. Czy pokazano bledy? Tak - konflikt i nieaktywne konto.
6. Czy nowa osoba zrozumie model? Opisy pod diagramami to ulatwiaja; do potwierdzenia podczas recenzji.
