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
| Licznik cykli | ✅ |
| Strona WWW | ✅ |
| Home Assistant | ✅ |
| OTA | ✅ |
| Praca bez HA | ✅ |
| Zapamiętywanie ustawień | ✅ |
| Pozostały czas | 🚧 |
| Status (Running/Stopped) | 🚧 |

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

Fizyczny przycisk na gniazdku przełącza tryb automatyczny.

---

# Roadmap

- [x] Utworzenie projektu
- [x] Konfiguracja ESPHome
- [x] Cykliczny timer ON/OFF
- [x] Harmonogram godzin z minutami
- [x] Licznik cykli
- [ ] Sensor "Status" (Running/Stopped/Out of schedule)
- [ ] Sensor "Remaining" (pozostały czas)
- [ ] Wydanie v1.0

---

# Licencja

Projekt udostępniony na licencji MIT.

Szczegóły znajdują się w pliku **LICENSE**.
