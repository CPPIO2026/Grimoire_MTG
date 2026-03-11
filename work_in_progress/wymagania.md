# Wymagania — Grimoire MtG

Skaner i deckbuilder do kart Magic: The Gathering

---

## 1. Ograniczenia

| ID | Ograniczenie |
|----|-------------|
| C-01 | Choć Flutter wspiera iOS i Androida jednocześnie, testowanie i budowanie wersji iOS wymaga komputera Mac oraz konta Apple Developer Program — zespół nie dysponuje takim sprzętem, więc weryfikacja na iOS nie jest gwarantowana w pierwszej iteracji. |
| C-02 | Skanowanie kart wymaga dostępu do kamery urządzenia — na wersji webowej funkcja skanowania nie jest dostępna. |
| C-03 | Dane o kartach MtG pochodzą z zewnętrznego API Scryfall — aplikacja jest zależna od jego dostępności i limitów zapytań. |
| C-04 | Rozpoznawanie kart opiera się na Google ML Kit, którego skuteczność zależy od jakości zdjęcia i oświetlenia. |
| C-05 | Aplikacja wymaga połączenia z internetem do synchronizacji danych, wyszukiwania kart i pobierania cen. |
| C-06 | Projekt realizowany jest w ramach kursu uczelnianego przez zespół trzyosobowy, co ogranicza zakres funkcjonalności w pierwszej iteracji. |

---

## 2. Wymagania systemowe

| ID | Wymaganie |
|----|-----------|
| SYS-01 | Backend oparty na Node.js z frameworkiem Express, udostępniający REST API. |
| SYS-02 | Baza danych MySQL przechowująca konta użytkowników, kolekcje kart i decki. |
| SYS-03 | Frontend mobilny w technologii Flutter (Android). |
| SYS-04 | Frontend webowy w technologii Flutter Web. |
| SYS-05 | Integracja z Scryfall API do wyszukiwania i pobierania metadanych kart. |
| SYS-06 | Integracja z Google ML Kit do rozpoznawania tekstu na kartach (wersja mobilna). |
| SYS-07 | Kontrola wersji za pomocą repozytorium GitHub. |
| SYS-08 | Testy jednostkowe w Jest, testy funkcjonalne w Postman/Newman. |

---

## 3. Wymagania funkcjonalne

Wymagania zapisane w formie historyjek użytkownika z priorytetami MoSCoW:

- **M** — Must have (konieczne)
- **S** — Should have (powinno być)
- **C** — Could have (mile widziane)
- **W** — Won't have this time (nie w tej iteracji)

| ID | Priorytet | Historyjka użytkownika |
|----|-----------|----------------------|
| FR-01 | M | Jako użytkownik chcę założyć konto i zalogować się, aby mieć dostęp do swojej kolekcji i decków. |
| FR-02 | M | Jako użytkownik chcę ręcznie wyszukać kartę po nazwie i dodać ją do swojej kolekcji, aby katalogować posiadane karty. |
| FR-03 | M | Jako użytkownik mobilny chcę zeskanować kartę kamerą telefonu, aby szybko dodać ją do kolekcji bez ręcznego wpisywania. |
| FR-04 | M | Jako użytkownik chcę tworzyć decki, dodając do nich karty z mojej kolekcji lub z wyszukiwarki, aby planować swoje talie. |
| FR-05 | M | Jako użytkownik chcę przeglądać swoją kolekcję z listą posiadanych kart, aby widzieć, czym dysponuję. |
| FR-06 | M | Jako użytkownik chcę przeglądać swoje decki i ich zawartość, aby zarządzać taliami. |
| FR-07 | S | Jako użytkownik webowy chcę filtrować karty w kolekcji po kolorze, typie, koszcie many i edycji, aby szybko znajdować potrzebne karty. |
| FR-08 | S | Jako użytkownik chcę, aby moje dane (kolekcja, decki) były zsynchronizowane między wersją mobilną i webową, aby móc korzystać z obu platform wymiennie. |
| FR-09 | S | Jako użytkownik chcę edytować istniejący deck (dodawać i usuwać karty), aby dostosowywać talię do aktualnych potrzeb. |
| FR-10 | S | Jako użytkownik chcę po zeskanowaniu karty od razu dodać ją do wybranego decku, aby przyspieszyć proces budowania talii. |
| FR-11 | S | Jako użytkownik chcę widzieć profil ze swoją kolekcją i listą decków, aby mieć przegląd całości. |
| FR-12 | S | Jako użytkownik chcę dodawać notatki do kart w kolekcji (np. stan karty, uwagi), aby przechowywać dodatkowe informacje. |
| FR-13 | C | Jako użytkownik chcę widzieć statystyki decku (mana curve, rozkład kolorów, liczba kart wg typu), aby ocenić zbalansowanie talii. |
| FR-14 | C | Jako użytkownik chcę sortować kolekcję według różnych kryteriów (nazwa, edycja, kolor, wartość), aby łatwiej ją przeglądać. |
| FR-15 | C | Jako użytkownik chcę widzieć aktualną wycenę rynkową kart w mojej kolekcji, aby znać jej łączną wartość. |
| FR-16 | C | Jako użytkownik chcę sprawdzić legalność karty w wybranym formacie turniejowym (Standard, Modern, Commander), aby budować legalne decki. |
| FR-17 | C | Jako użytkownik chcę eksportować deck do pliku tekstowego lub udostępnić go linkiem, aby dzielić się taliami z innymi graczami. |
| FR-18 | W | Jako użytkownik chcę usuwać karty z kolekcji, aby utrzymywać ją w aktualnym stanie. |
| FR-19 | W | Jako użytkownik chcę skanować wiele kart w trybie seryjnym (bez zatwierdzania każdej z osobna), aby masowo katalogować dużą kolekcję. |
| FR-20 | W | Jako użytkownik chcę porównać dwa decki obok siebie z podświetleniem różnic, aby łatwo analizować warianty tej samej talii. |
| FR-21 | W | Jako użytkownik chcę otrzymywać powiadomienia push, gdy cena karty z mojej kolekcji przekroczy ustawiony próg, aby nie przegapić okazji do sprzedaży. |

---

## 4. Wymagania niefunkcjonalne

| ID | Wymaganie | Sposób weryfikacji |
|----|-----------|-------------------|
| NFR-01 | Rozpoznanie karty ze skanu powinno trwać nie dłużej niż 3 sekundy od momentu zrobienia zdjęcia. | Pomiar czasu od wykonania zdjęcia do wyświetlenia wyniku na próbie 20 różnych kart. |
| NFR-02 | Skuteczność rozpoznawania nazwy karty ze skanu powinna wynosić co najmniej 85% przy dobrym oświetleniu. | Test na zbiorze 50 kart w kontrolowanych warunkach; zliczenie poprawnych rozpoznań. |
| NFR-03 | Aplikacja webowa powinna załadować widok kolekcji (do 500 kart) w czasie poniżej 2 sekund. | Pomiar czasu ładowania strony narzędziem Lighthouse lub DevTools przy kolekcji 500 kart. |
| NFR-04 | Hasła użytkowników muszą być przechowywane w formie zahashowanej (bcrypt lub równoważny algorytm). | Inspekcja bazy danych — sprawdzenie, że hasła nie są przechowywane w postaci jawnej. |
| NFR-05 | Komunikacja między klientem a serwerem musi odbywać się przez HTTPS. | Sprawdzenie nagłówków odpowiedzi serwera i certyfikatu TLS. |
| NFR-06 | Interfejs mobilny musi być użyteczny na ekranach o szerokości od 360px wzwyż. | Test ręczny na urządzeniach/emulatorach o rozdzielczości 360px, 390px i 412px. |
| NFR-07 | Interfejs webowy musi być responsywny i użyteczny na ekranach od 768px wzwyż. | Test ręczny w przeglądarce przy szerokościach 768px, 1024px i 1440px. |
| NFR-08 | System powinien obsługiwać co najmniej 50 jednoczesnych użytkowników bez zauważalnej degradacji wydajności. | Test obciążeniowy (np. k6 lub Artillery) symulujący 50 równoległych sesji. |
| NFR-09 | Kod źródłowy musi być objęty testami jednostkowymi pokrywającymi co najmniej 60% logiki backendowej. | Raport pokrycia kodu generowany przez Jest (--coverage). |

---

*Grimoire MtG — Pryncypałki — Zadanie: Wymagania*