# ESPhome_basics

Gemeinsames Package für alle eigenen ESPHome-Geräte (`.basics.yaml`).

> [!WARNING]
> **Sicherheit & Haftung / Safety & liability** – Privates Hobbyprojekt, bereitgestellt «wie besehen», Nutzung **auf eigene Gefahr**.
> Dieses Package bestimmt API, OTA, WLAN, Fallback-AP und Webserver **aller** eingebundenen Geräte. Eine unsichere Konfiguration (schwache Passwörter, Webserver ohne Authentifizierung, offener Fallback-AP) kann Fremden Zugriff auf Geräte geben, die Lasten, Heizung oder Fahrzeugfunktionen schalten.
> Secrets nie ins Repository einchecken.
> Details: [DISCLAIMER.md](DISCLAIMER.md) (DE/EN).

## Einbindung
Datei nach `/config/esphome/.basics.yaml` legen, im Gerät:

```yaml
substitutions:
  name: mein-geraet

packages:
  basics: !include .basics.yaml
```

`${name}` wird für den Fallback-AP verwendet.

## Inhalt
| Block | Zweck |
|---|---|
| `ota`, `api` | Verschlüsselte HA-API; OTA mit leerem `encryption:` = verschlüsselt und Pflicht, nutzt den API-Key (ab ESPHome 2026.9) |
| `wifi` | WLAN, kein Powersave, 17 dB, Fallback-AP, `reboot_timeout: 0s` |
| `web_server` | v3, lokal, Port 80 |
| `logger` | Level DEBUG |
| `debug` | Reset Reason, Heap Free, Heap Max Block, Loop Time (300 s) |
| `sensor` | WiFi Signal (60 s) |
| `time` | Zeit von Home Assistant |
| `button` | Restart |

## Voraussetzung
ESPHome **2026.9 oder neuer** (wegen `ota: encryption:`). Ältere Versionen melden
`[encryption] is an invalid option for [ota.esphome]`.

## Secrets
Benötigt `wifi_ssid`, `wifi_password`, `fallback_password`, `api_encryption_key` (siehe `secrets.yaml.example`).

## Geräte
- [mpu6050](https://github.com/CzarofAK/mpu6050) – WOMO-Nivelliersensor
- [smartebl](https://github.com/CzarofAK/smartebl) – Smart EBL

## Lizenz

MIT, siehe [LICENSE](LICENSE). Nutzung auf eigene Gefahr – siehe [DISCLAIMER.md](DISCLAIMER.md).
