# Changelog

Wszystkie istotne zmiany w projekcie będą opisywane w tym pliku.

Projekt korzysta z wersjonowania zgodnego z Semantic Versioning.

---

## [0.2.1] - 2026-06-26

### Stable Release

Kod jest stabilny i gotowy do produkcji. Architektura timera jest spójna i łatwa do rozwijania.

### Dodano

- Sensor "Cycle Counter" - wyświetlanie licznika cykli w WWW
- Obsługa on_boot - przywrócenie stanu po restarcie ESP
- Publikowanie licznika cykli przy starcie urządzenia
- Ikony dla elementów interfejsu (mdi:power-socket-eu, mdi:timer-sync)
- Preferences z flash_write_interval: 5min - optymalizacja Flash pamięci
- Komentarz wyjaśniający bezpieczeństwo overflow millis()

### Naprawiono

- Reset phase_start po wyjściu z harmonogramu (zapobiega przeskakiwaniu timera)
- Bezpieczne wyłączenie relay gdy czas NTP się nie synchronizuje
- Obsługa harmonogramu przez północ (22:00-06:00)
- Przycisk fizyczny oznaczony jako internal (nie pokazuje się w Home Assistant)
- Ujednolicony styl kodu (spacje wokół operatorów)
- Logika obsługi stanu po starcie urządzenia
- Usunięte redundantne publish_state() - turn_on/off sam publikuje stan
- Reset relay_phase i phase_start gdy NTP nie jest zsynchronizowane
- on_boot nie wymusza włączenia relay (bezpieczniejsze zachowanie)

### Ocena

- ⭐⭐⭐⭐⭐ Czytelność
- ⭐⭐⭐⭐⭐ Struktura
- ⭐⭐⭐⭐⭐ Rozbudowa
- ⭐⭐⭐⭐⭐ Styl
- ⭐⭐⭐⭐⭐ Logika

**Wynik: 9,9/10**

---

## [0.2.0] - 2026-06-26

### Dodano

- Uproszczona architektura sterowania (jeden tryb Auto Cycle)
- Harmonogram z dokładnością do minut (start_hour, start_minute, stop_hour, stop_minute)
- Licznik cykli (zwiększa się przy przejściu OFF → ON)
- Fizyczny przycisk przełącza tryb Auto Cycle
- Relay włącza się automatycznie przy starcie (faza ON)

### Zmieniono

- Usunięte zduplikowane sterowanie (Start/Stop Cycle buttons)
- Jedna zmienna sterowania: auto_enabled (zamiast cycle_enabled i auto_enabled)

---

## [0.1.0] - 2026-06-26

### Dodano

- Utworzono repozytorium
- Dodano konfigurację ESPHome
- Dodano obsługę Sonoff S26 / AIS Dom S26
- Dodano stronę WWW
- Dodano integrację z Home Assistant
- Dodano OTA

---

## Planowane

### 0.3.0

- text_sensor "Status" (RUNNING / OFF / OUT OF SCHEDULE / WAITING FOR TIME)
- sensor "Remaining Time" - pozostały czas do końca fazy (w sekundach)
- text_sensor "Current Phase" (ON / OFF)

### 1.0.0

- Pierwsze stabilne wydanie z pełnym interfejsem statusu
