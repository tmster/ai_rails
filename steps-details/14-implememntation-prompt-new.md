# Plan implementacji widoku potwierdzenia zaproszenia

Twoim zadaniem jest implementacja kompletnego widoku potwierdzenia zaproszenia w aplikacji Ruby on Rails, zgodnie z dostarczonym planem implementacji. Implementacja powinna obejmować zarówno warstwę frontendową (widoki, komponenty), jak i backendową (kontrolery, modele), z wykorzystaniem najnowszych praktyk Rails oraz Hotwire.

## Przegląd dokumentacji

### Plan implementacji
Plan znajduje się w pliku `.ai/confirmation-implememntation-plan.md` i zawiera szczegółowe informacje o:
- Strukturze routingu
- Wymaganych modelach i ich relacjach
- Kontrolerach i ich akcjach
- Komponentach UI i ich właściwościach
- Widokach i szablonach
- Wymaganiach dotyczących testów

### Konwencje i standardy
Implementacja powinna być zgodna z:
- Konwencjami Ruby on Rails 8.1
- RubyUI Component Framework
- Hotwire (Turbo, Stimulus) dla interaktywności
- Tailwind CSS dla stylowania
- RSpec dla testów

## Podejście implementacyjne

### 1. Konfiguracja i routing (Backend):
- Utwórz niezbędne trasy w `config/routes.rb`
- Skonfiguruj kontroler `ConfirmationsController`
- Zweryfikuj i uzupełnij modele (Invitation, InvitationParticipant, Confirmation)
- Ustaw odpowiednie walidacje i callbacks

### 2. Komponenty UI (Frontend):
- Zaimplementuj wymagane komponenty RubyUI:
  - CardComponent dla głównego kontenera
  - ButtonComponent dla akcji potwierdzenia
  - FlashComponent dla komunikatów
- Zastosuj stylowanie Tailwind zgodnie z wytycznymi

### 3. Widoki i szablony (Frontend):
- Utwórz szablony ERB z wykorzystaniem Hotwire
- Zintegruj komponenty RubyUI
- Zaimplementuj obsługę Turbo Frames
- Dodaj wsparcie dla ARIA i dostępności

### 4. Logika biznesowa (Backend):
- Zaimplementuj akcje kontrolera
- Dodaj obsługę błędów i walidacji
- Skonfiguruj ActiveJob dla retry logic
- Zaimplementuj serwisy pomocnicze

### 5. Interaktywność (Frontend + Backend):
- Dodaj Stimulus kontrolery gdzie potrzebne
- Skonfiguruj Turbo Streams dla aktualizacji w czasie rzeczywistym
- Zaimplementuj obsługę stanu ładowania
- Dodaj animacje i przejścia

### 6. Testy:
- Napisz testy RSpec dla:
  - Modeli
  - Kontrolerów
  - Komponentów
  - Integracji
- Zaimplementuj testy systemowe dla pełnego flow

## Implementacja krok po kroku

Realizuj implementację w małych, zweryfikowanych krokach:

1. Wykonaj pierwsze 3 zadania z aktualnej sekcji
2. Przetestuj zmiany i upewnij się, że wszystko działa
3. Podsumuj wykonane prace
4. Opisz plan na kolejne 3 zadania
5. Zatrzymaj się i poczekaj na feedback
6. Po otrzymaniu akceptacji, kontynuuj z kolejnymi zadaniami

## Standardy implementacji

### Backend:
- Używaj wzorca Repository dla złożonych zapytań
- Implementuj callback'i w modelach dla logiki biznesowej
- Stosuj Service Objects dla złożonej logiki
- Wykorzystuj Active Job dla zadań asynchronicznych
- Implementuj obsługę błędów przez rescue_from

### Frontend:
- Komponenty muszą dziedziczyć po RubyUI::BaseComponent
- Wykorzystuj Phlex do generowania HTML
- Komponenty powinny być bezstanowe
- Używaj Tailwind dla stylowania
- Implementuj pełne wsparcie dla dostępności

### Testy:
- Jeden test na jedną asercję
- Używaj subject dla głównego obiektu testowego
- Preferuj eq zamiast == dla porównań
- Testuj wszystkie edge cases
- Implementuj testy systemowe dla kluczowych ścieżek

## Walidacja implementacji

Po zakończeniu każdej sekcji upewnij się, że:
1. Kod jest zgodny z konwencjami Ruby on Rails
2. Wszystkie komponenty są poprawnie zintegrowane
3. Testy przechodzą i pokrywają kluczową funkcjonalność
4. UI jest responsywne i dostępne
5. Wydajność jest optymalna
6. Obsługa błędów jest kompletna
7. Dokumentacja jest aktualna

## Priorytety podczas implementacji

1. Poprawność działania
2. Zgodność z konwencjami Rails i RubyUI
3. Pokrycie testami
4. Dostępność
5. Wydajność
6. DRY i czystość kodu
7. Dokumentacja
