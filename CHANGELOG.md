# Changelog

Wszystkie istotne zmiany w projekcie będą opisywane w tym pliku.

Projekt korzysta z wersjonowania zgodnego z Semantic Versioning.

---

## [0.2.1] - 2026-06-26

### Dodano

- Sensor "Cycles" - wyświetlanie licznika cykli w WWW
- Obsługa on_boot - przywrócenie stanu po restarcie ESP
- Ikony dla elementów interfejsu (mdi:power-socket-eu, mdi:timer-sync)
- Preferences z flash_write_interval: 5min - optymalizacja Flash pamięci

### Naprawiono

- Reset phase_start po wyjściu z harmonogramu (zapobiega przeskakiwaniu timera)
- Przycisk fizyczny oznaczony jako internal (nie pokazuje się w Home Assistant)
- Logika obsługi stanu po starcie urządzenia

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

- Sensor "Status" (Running / Stopped / Out of schedule)
- Sensor "Remaining" - pozostały czas (HH:MM)
- Sensor "Cycles" - licznik cykli (już w 0.2.1)

### 1.0.0

- Pierwsze stabilne wydanie
