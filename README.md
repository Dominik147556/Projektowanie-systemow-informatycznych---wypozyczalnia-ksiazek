# BookFlow - system wypozyczania ksiazek

Projekt semestralny - Projektowanie systemow informatycznych, Laboratoria 1 i 2.

**Sklad:** Adam Kilisz, Dominik Chachuła, Łukasz Nowak, Dawid Oblonczek
**Temat:** Internetowy system obslugi wypozyczen ksiazek w bibliotece.

## Cel
Umozliwic czytelnikom sprawdzanie dostepnosci egzemplarzy, skladanie rezerwacji i kontrole terminow zwrotu, a bibliotekarzom obsluge wydan i zwrotow.

## Zakres pierwszej wersji
Katalog, rezerwacje, wypozyczenia, zwroty, przedluzenia, kolejka oczekujacych, powiadomienia i obsluga utraconych egzemplarzy. Platnosci online, e-booki i rekomendacje AI sa poza zakresem.

## Pliki
- `docs/wymagania.md` - aktorzy, wersja 0, historyjki, wymagania niefunkcjonalne.
- `docs/ai-log.md` - przykladowa symulacja wywiadu, analiza luk i refleksja; wymaga weryfikacji przez zespol.

## Do wykonania przez zespol
1. Uzupelnic sklad i loginy.
2. Zweryfikowac przykladowa wersje 0 z wlasnymi pomyslami przed uzyciem AI oraz przeprowadzic wlasny wywiad.
3. Uzgodnic wymagania z prowadzacym (temat wlasny wymaga akceptacji).
4. Umiescic pliki w repozytorium i nadac tag `v0.1-wymagania`.

## Laboratorium 2 - modelowanie
- `docs/zdarzenia.md` - propozycja osi zdarzen i pytania otwarte; do przeprowadzenia bez AI.
- `docs/architektura.md` - C4 poziom 1 i 2, dwie sekwencje, maszyna stanow w Mermaid.
- `docs/log-poprawek.md` - poprawki szkicu AI i miejsce na rzeczywista recenzje krzyzowa.

## Oddanie Lab 2
Po recenzji i zatwierdzeniu diagramow wykonaj:
```bash
git add -A
git commit -m "Lab 2: model C4, sekwencje i stany"
git tag v0.2-model
git push && git push --tags
```
Wymagane sa rowniez 3 rzeczywiste issues dla innego zespolu i odpowiedzi na otrzymane uwagi.
