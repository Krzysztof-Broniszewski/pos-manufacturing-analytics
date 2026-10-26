POS MANUFACTURING ANALYTICS - POWER QUERY DATA CLEANING LAB

Dane są w 100% syntetyczne, ale reprezentują realistyczne błędy w danych operacyjnych.

PLIKI:
FactSalesOrders_DIRTY.csv - główny plik treningowy, separator ;, UTF-8 BOM.
DimCustomer_REFERENCE.csv - poprawny słownik klientów.
DimProduct_REFERENCE.csv - poprawny słownik produktów.

UWAGA: plik zawiera celowe błędy, NIE importuj go do finalnego modelu zamiast prawdziwych tabel.

KOLEJNOŚĆ NAUKI:
1. Import jako nowe zapytanie; wyłącz ładowanie na czas treningu.
2. Zachowaj surową kopię zapytania i utwórz zapytanie robocze przez Odwołanie.
3. Profilowanie całego zbioru: jakość, rozkład, profil, typy.
4. Usuwanie pustych rekordów, identyfikacja duplikatów i konfliktów kluczy.
5. Czyszczenie tekstu: Trim/Clean/normalizacja wartości.
6. Typy liczbowe i daty, formaty regionalne, błędy konwersji.
7. Braki danych: decyzja biznesowa, nie automatyczne zastępowanie zerem.
8. Walidacja biznesowa: ilość, cena, rabat, daty.
9. Walidacja referencyjna: CustomerID i ProductID ze słownikami (merge / anti join).
10. Tabela odrzuconych / wymagających wyjaśnienia rekordów i audyt.
11. Sprawdzenie wyników i dopiero potem model relacyjny oraz DAX.

Nie każda anomalia ma jednoznaczne rozwiązanie. Nie zgaduj brakujących danych.
