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
- on_boot nie wymusza włączenia relay - decyzję podejmuje interval

## Optymalizacja

- Flash pamięć zapisywana zbiorczo co 5 minut (flash_write_interval)
- Sensor licznika odświeża się tylko przy zmianach, nie cyklicznie
- Minimalne zużycie zasobów ESP8266

---

# Roadmap

- [x] Utworzenie projektu
- [x] Konfiguracja ESPHome
- [x] Cykliczny timer ON/OFF
- [x] Harmonogram godzin z minutami
- [x] Licznik cykli
- [ ] text_sensor "Status" (Running/Stopped/Out of schedule/Waiting for time)
- [ ] sensor "Remaining Time" (pozostały czas)
- [ ] text_sensor "Current Phase" (ON/OFF)
- [ ] Wydanie v1.0

---

# Licencja

Projekt udostępniony na licencji MIT.

Szczegóły znajdują się w pliku **LICENSE**.

---

# Ocena kodu

**v0.2.1 Stable** - 9,9/10

- ⭐⭐⭐⭐⭐ Czytelność
- ⭐⭐⭐⭐⭐ Struktura
- ⭐⭐⭐⭐⭐ Rozbudowa
- ⭐⭐⭐⭐⭐ Styl
- ⭐⭐⭐⭐⭐ Logika

Kod jest spójny i gotowy do rozwijania. Następny krok: v0.3.0 z sensorami statusu.
