---
editor_options: 
  markdown: 
    wrap: 72
---

# Lab_14

### **Porównanie: Delta Lake vs Apache Iceberg**

| Kryterium | Delta Lake | Apache Iceberg |
|------------------------|------------------------|------------------------|
| **Zarządzanie metadanymi** | Transakcje ACID, log JSON | Lepsze zarządzanie metadanymi |
| **Kompatybilność** | Głównie Spark, dobrze wspierany w Databricks | Szersza kompatybilność |
| **Wydajność przy dużych zbiorach** | Dobra, ale przy wielu plikach bywa słaba | Lepsza przy petabajtach danych |
| **Operacje time travel** | Tak, oparty na logach | Tak, oparty na snapshotach |
| **Integracja z Azure** | Natywna z Databricks | Wymaga integracji |

**Delta Lake** bardziej optymalny, jeśli:

-   korzystasz z Azure Databricks
-   zależy Ci na prostocie i wsparciu technicznym
-   dane nie przekraczają skali petabajtowej

**Apache Iceberg** bardziej optymalny, jeśli:

-   chcesz wieloplatformowego silnika
-   potrzebujesz bardzo skalowalnego i wydajnego formatu
-   planujesz rozproszony system poza Databricks

------------------------------------------------------------------------

### **Krytyka architektury medalionu**

1.  **Złożoność architektury** - Trzy warstwy danych wymagają
    zbudowania i utrzymania większej liczby pipeline’ów.
2.  **Powielanie danych** - Te same dane są kopiowane między warstwami, co
    zwiększa zużycie storage’u.
3.  **Większe koszty przechowywania** - Każda warstwa wymaga osobnej
    przestrzeni dyskowej – to mnoży koszty.
4.  **Opóźnienia przetwarzania** - Dane nie są dostępne od razu – muszą
    przejść przez wszystkie warstwy.
5.  **Ryzyko niespójności danych** - Różne wersje danych mogą się pojawić
    w różnych warstwach, np. przez błędne transformacje.
6.  **Złożona synchronizacja** - Pipeline’y między warstwami muszą być
    zsynchronizowane co do wersji i czasu.
7.  **Wysoki próg wejścia** - Nowe osoby w zespole muszą zrozumieć każdą
    warstwę i jej rolę.
8.  **Nadmierna liczba plików** - Trzy kopie danych powodują bałagan w
    katalogach i nazwach plików.
9.  **Nadmierna transformacja danych** - Często dane są niepotrzebnie
    przetwarzane w każdej warstwie.
10. **Utrudnione debugowanie** - Błędy w Gold są trudniejsze do
    prześledzenia wstecz przez trzy warstwy.
11. **Zwiększone wymagania ETL/ELT** - Każda warstwa wymaga osobnych
    transformacji i kodu.
12. **Trudności w zarządzaniu jakością danych** - Trzeba monitorować
    jakość na każdym etapie oddzielnie.
13. **Nieoptymalne dla danych strumieniowych** - Architektura lepiej
    pasuje do batch processing niż streamingu.
14. **Wydłużony czas dostępu do danych analitycznych** - Analitycy muszą
    czekać, aż dane dotrą do warstwy Gold.
15. **Problemy z wersjonowaniem danych** - Trzeba śledzić wersje tych
    samych danych w różnych warstwach.
16. **Wysoka złożoność testowania** - Każda warstwa wymaga osobnych testów
    jakości i integralności.
17. **Trudne zarządzanie schematami** - Schematy mogą się zmieniać między
    warstwami – trzeba je synchronizować.
18. **Overengineering dla małych projektów** - Małe organizacje nie
    potrzebują tylu warstw – to marnotrawstwo zasobów.
19. **Złożony monitoring i alerting** - Trzeba monitorować błędy i procesy
    w wielu miejscach naraz.
20. **Brak elastyczności** - Tradycyjna struktura Bronze–Silver–Gold nie
    pasuje do każdego przypadku i ogranicza eksperymentowanie.
