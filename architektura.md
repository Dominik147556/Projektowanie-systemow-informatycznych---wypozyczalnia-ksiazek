# BookFlow - architektura v0.2

> Modele sa propozycja AI oparta na wymaganiach Lab 1. Nie stanowia zatwierdzonej architektury ani wyboru technologii.

## 1. C4 - poziom 1 - kontekst

```mermaid
flowchart LR
    C([Czytelnik]) -->|wyszukuje i rezerwuje ksiazki| BF[BookFlow - system wypozyczen]
    B([Bibliotekarz]) -->|wydaje i przyjmuje egzemplarze| BF
    A([Administrator]) -->|zarzadza uprawnieniami| BF
    K([Kierownik biblioteki]) -->|przeglada raporty zaleglosci| BF
    BF -->|zleca wysylke powiadomien| E[[Zewnetrzna usluga e-mail]]
    E -->|zwraca wynik dostarczenia| BF
```

**Granica systemu:** BookFlow odpowiada za katalog, rezerwacje, wypozyczenia, zwroty i przygotowanie powiadomien. Dostarczenie e-maila jest poza granica systemu.

## 2. C4 - poziom 2 - kontenery

```mermaid
flowchart LR
    C([Czytelnik]) -->|korzysta z interfejsu| WEB[Aplikacja web - interfejs]
    B([Bibliotekarz]) -->|obsluguje wydania i zwroty| WEB
    A([Administrator]) -->|zarzadza kontami| WEB
    K([Kierownik biblioteki]) -->|otwiera raporty| WEB
    subgraph BF[BookFlow - granica systemu]
        WEB -->|zadania i odpowiedzi| API[API - logika biblioteki]
        API -->|odczyt i zapis| DB[(Baza danych - katalog i operacje)]
        API -->|zlecenia powiadomien| Q[Kolejka zadan]
        Q -->|pobiera zlecenia| W[Pracownik powiadomien]
    end
    W -->|wysyla wiadomosci| E[[Zewnetrzna usluga e-mail]]
    E -->|wynik wysylki| W
```

**Role kontenerow:** aplikacja web wyswietla dane i przyjmuje akcje, API egzekwuje zasady i kontroluje konflikty, baza przechowuje stan, kolejka oddziela wysylke od operacji, pracownik powiadomien kontaktuje sie z usluga e-mail. Nazwy technologii zostana wybrane w Lab 3.

## 3. Diagram sekwencji - rezerwacja dostepnego egzemplarza (R-03, Must)

```mermaid
sequenceDiagram
    actor C as Czytelnik
    participant W as Aplikacja web
    participant A as API
    participant D as Baza danych
    participant Q as Kolejka powiadomien
    C->>W: Wybiera dostepny egzemplarz i klika Rezerwuj
    W->>A: Zada utworzenia rezerwacji
    A->>D: Sprawdz aktywne konto i dostepnosc oraz zablokuj egzemplarz
    D-->>A: Konto aktywne i egzemplarz wolny
    A->>D: Zapisz jedna rezerwacje z terminem odbioru
    D-->>A: Rezerwacja zapisana
    A->>Q: Zlec e-mail potwierdzajacy
    Q-->>A: Zlecenie przyjete
    A-->>W: Rezerwacja potwierdzona
    W-->>C: Pokaz potwierdzenie i termin odbioru
```

**Kryterium:** jedna aktywna rezerwacja dla dostepnego egzemplarza i aktywnego czytelnika. Zlecenie e-mail nie jest warunkiem waznosci rezerwacji.

## 4. Diagram sekwencji - konflikt rezerwacji (R-03, Must)

```mermaid
sequenceDiagram
    actor C as Czytelnik
    participant W as Aplikacja web
    participant A as API
    participant D as Baza danych
    C->>W: Wybiera egzemplarz i klika Rezerwuj
    W->>A: Zada utworzenia rezerwacji
    A->>D: Sprawdz konto i atomowo zajmij egzemplarz
    alt Egzemplarz zarezerwowany przez inna osobe
        D-->>A: Konflikt - egzemplarz niedostepny
        A-->>W: Odrzuc rezerwacje - konflikt
        W-->>C: Pokaz komunikat o niedostepnosci
    else Konto nieaktywne
        D-->>A: Brak uprawnien do rezerwacji
        A-->>W: Odmowa rezerwacji
        W-->>C: Pokaz powod odmowy
    else Egzemplarz dostepny
        D-->>A: Blokada przyznana
        A->>D: Zapisz rezerwacje
        D-->>A: Zapis zakonczony
        A-->>W: Rezerwacja potwierdzona
        W-->>C: Pokaz termin odbioru
    end
```

**Kryterium:** przy rownoczesnych probach nie powstaja dwie aktywne rezerwacje tego samego egzemplarza. Niepowodzenie nie tworzy rezerwacji.

## 5. Maszyna stanow - rezerwacja egzemplarza

```mermaid
stateDiagram-v2
    [*] --> Zlozona: czytelnik rezerwuje
    Zlozona --> Potwierdzona: egzemplarz dostepny i konto aktywne
    Zlozona --> Odrzucona: konflikt lub konto nieaktywne
    Potwierdzona --> Zrealizowana: bibliotekarz wydaje egzemplarz
    Potwierdzona --> Anulowana: uprawniona osoba anuluje
    Potwierdzona --> Wygasla: mija termin odbioru
    Odrzucona --> [*]
    Zrealizowana --> [*]
    Anulowana --> [*]
    Wygasla --> [*]
```

**Zabronione przejscia:** Zrealizowana -> Potwierdzona oraz Wygasla -> Zrealizowana. Po wydaniu ksiazki cykl rezerwacji sie konczy, a dalsza obsluga dotyczy wypozyczenia.

## 6. Trzy zalozenia AI
1. Czytelnik ma aktywne konto przed utworzeniem rezerwacji (zgodne z R-03).
2. Zapis rezerwacji i kontrola konfliktu sa jedna operacja atomowa (wniosek z NF-06).
3. Powiadomienia sa zlecane asynchronicznie, aby awaria e-mail nie anulowala rezerwacji (zgodne z granica Lab 1).

## 7. Trzy pytania bez odpowiedzi w wymaganiach
1. Jaki jest ostateczny termin odbioru rezerwacji i kto moze go zmieniac?
2. Czy anulowanie przez bibliotekarza wymaga podania powodu?
3. Jak dokladnie przydzielac zwrocony egzemplarz osobom w kolejce na tytul?

## 8. Weryfikacja diagramow
- Aktorzy z Lab 1: czytelnik, bibliotekarz, administrator, kierownik - uwzglednieni.
- Usluga e-mail jest oznaczona jako zewnetrzna.
- Strzalki maja opisy czynnosci lub danych.
- Sciezka glowna i blad rezerwacji odpowiadaja R-03 i NF-06.
- Diagramy sa na poziomie systemu i kontenerow - bez klas i tabel.
- Skladnia Mermaid wymaga sprawdzenia w podgladzie GitHub lub mermaid.live.
