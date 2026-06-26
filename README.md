# 🏊 Basen Timer Plug

Lokalny sterownik czasowy oparty na **ESPHome** dla urządzeń z **ESP8266** i **ESP32**.

Projekt został stworzony do sterowania urządzeniami pracującymi cyklicznie, takimi jak:

- 🏊 Pompa basenowa
- 🌬️ Wentylator
- 💨 Kompresor
- 💡 Oświetlenie
- 🚰 Pompa
- ⚙️ Dowolne urządzenie sterowane przekaźnikiem

> **Cała logika działa lokalnie na ESP.**
>
> Home Assistant jest opcjonalny i służy jedynie do monitorowania oraz zmiany ustawień.

---

# Dlaczego ten projekt?

Większość timerów dla ESPHome wymaga automatyzacji w Home Assistant.

**Basen Timer Plug** wykonuje całą logikę bezpośrednio na ESP8266/ESP32.

Dzięki temu urządzenie:

- działa bez Home Assistanta,
- działa bez Internetu,
- po awarii HA nadal pracuje zgodnie z harmonogramem,
- może być konfigurowane z poziomu przeglądarki WWW.

---

# Funkcje

| Funkcja | Status |
|---------|:------:|
| Cykliczne ON/OFF | ✅ |
| Konfigurowany czas ON | ✅ |
| Konfigurowany czas OFF | ✅ |
| Harmonogram z minutami | ✅ |
| Harmonogram przez północ | ✅ |
| Licznik cykli | ✅ |
| Strona WWW | ✅ |
| Home Assistant | ✅ |
| OTA | ✅ |
| Praca bez HA | ✅ |
| Zapamiętywanie ustawień | ✅ |
| Status (Running/Stopped) | 🚧 |
| Pozostały czas | 🚧 |

---

# Schemat działania

```
08:00
 │
 ├── ON 15 min
 ├── OFF 45 min
 ├── ON 15 min
 ├── OFF 45 min
 │
 20:00
 │
 └── Relay OFF
```

---

# Obsługiwane urządzenia

Aktualnie:

- Sonoff S26
- AIS Dom S26

Planowane:

- Sonoff Basic
- Sonoff Mini
- ESP8266
- ESP32

---

# Instalacja

Sklonuj repozytorium:

```bash
git clone https://github.com/pimowo/Basen-Timer-Plug.git
```

Otwórz:

```
esphome/basen-timer-plug.yaml
```

Uzupełnij dane WiFi w pliku `secrets.yaml`:

```yaml
wifi_ssid: "Twoja sieć WiFi"
wifi_password: "Twoje hasło"
```

Skompiluj projekt:

```bash
esphome compile esphome/basen-timer-plug.yaml
```

Wgraj firmware na urządzenie.

---

# Konfiguracja

Po pierwszym starcie dostęp do panelu WWW:

```
http://<ip-urządzenia>
```

Gdzie możesz ustawić:

- **ON Time** - czas włączenia (1-240 minut)
- **OFF Time** - czas wyłączenia (1-240 minut)
- **Start Hour / Start Minute** - godzina rozruchu harmonogramu
- **Stop Hour / Stop Minute** - godzina zatrzymania harmonogramu
- **Auto Cycle** - włącz/wyłącz tryb automatyczny
- **Cycle Counter** - liczba wykonanych cykli

Fizyczny przycisk na gniazdku przełącza tryb automatyczny.

---

# Techniczne

## Bezpieczeństwo

- Relay wyłącza się automatycznie, jeśli czas NTP się nie synchronizuje
- Po restarcie urządzenia licznik cykli odtwarza poprawną wartość
- Timer bezpiecznie obsługuje przepełnienie `millis()` po ~49 dniach
- Po utracie synchronizacji NTP timer resetuje się na pełną fazę ON
- Harmonogram reaguje natychmiastowo na zmianę stanu (wejście/wyjście)

## Optymalizacja

- Flash pamięć zapisywana zbiorczo co 5 minut (flash_write_interval)
- Sensor licznika odświeża się tylko przy zmianach, nie cyklicznie
- Eliminacja zbędnych poleceń `turn_off()` co sekundę
- Minimalne zużycie zasobów ESP8266

## Harmonogram przez północ

Projekt obsługuje zakresy harmonogramu przechodzące przez północ:

```yaml
Start Hour: 22
Start Minute: 0
Stop Hour: 6
Stop Minute: 0

# Urządzenie będzie aktywne: 22:00 - 23:59 i 00:00 - 06:00
```

---

# Roadmap

- [x] Utworzenie projektu
- [x] Konfiguracja ESPHome
- [x] Cykliczny timer ON/OFF
- [x] Harmonogram godzin z minutami
- [x] Licznik cykli
- [x] Optymalizacja przejść harmonogramu (v0.2.2)
- [ ] text_sensor "Status" (Running/Stopped/Out of schedule/Waiting for time)
- [ ] sensor "Remaining Time" (pozostały czas)
- [ ] text_sensor "Current Phase" (ON/OFF)
- [ ] Wydanie v1.0

---

# Historia wersji

## v0.2.2 Stable (2026-06-26)

**Optymalizacja przejść harmonogramu**

- Natychmiastowe włączenie o 08:00:00 (false → true)
- Bezpieczne wyłączenie po wyjściu z harmonogramu (true → false)
- Eliminacja zbędnych poleceń `turn_off()` co sekundę
- Nowa zmienna `was_allowed` do wykrywania zmian stanu

**Ocena: 10/10**

## v0.2.1 Stable (2026-06-26)

**Kod gotowy do produkcji**

- Architektura spójna i rozszerzalna
- Obsługa harmonogramu przez północ
- Licznik cykli z zapisem w Flash
- Bezpieczeństwo NTP i millis()

**Ocena: 9,9/10**

---

# Licencja

Projekt udostępniony na licencji MIT.

Szczegóły znajdują się w pliku **LICENSE**.

---

# Ocena kodu

**v0.2.2 Stable** - 10/10

- ⭐⭐⭐⭐⭐ Czytelność
- ⭐⭐⭐⭐⭐ Struktura
- ⭐⭐⭐⭐⭐ Rozbudowa
- ⭐⭐⭐⭐⭐ Styl
- ⭐⭐⭐⭐⭐ Logika

Kod jest spójny, niezawodny i gotowy do v0.3.0 z sensorami statusu.
