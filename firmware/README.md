# Firmware – ESPHome

Die aktuelle ESPHome-Konfiguration des Bewässerungscontrollers liegt in [bewaesserung.yaml](bewaesserung.yaml). Als Hardware wird ein DFRobot FireBeetle 2 ESP32-E mit dem ESP-IDF-Framework eingesetzt.

## Konfiguration

- Ventilausgänge: GPIO18, GPIO13, GPIO14, GPIO26, GPIO25, GPIO4, GPIO17 und GPIO16
- Neustartverhalten: Alle Ventilausgänge sind mit `ALWAYS_OFF` konfiguriert.
- RS12-Regensensor: GPIO36, invertiertes Digitalsignal mit 1 s Einschalt- und 10 s Ausschaltverzögerung
- Durchflusssensor: GPIO35, `pulse_meter` mit einem vorläufigen Umrechnungsfaktor von 1/660 L pro Impuls; die Kalibrierung steht noch aus
- Temperatursensor: GPIO34, ADC mit 47-kΩ-Referenzwiderstand und einer in der Firmware hinterlegten NTC-Kalibrierreferenz von 50 kΩ
- Kommunikation: WLAN, MQTT-Discovery, OTA-Updates und Fallback-Access-Point

## Geplante Weiterentwicklung

Der Bewässerungscontroller verbindet sich derzeit per WLAN mit dem MQTT-Broker. Um die Abhängigkeit von der eingeschränkten 2,4-GHz-WLAN-Abdeckung der vorhandenen FRITZ!Box zu reduzieren, ist eine ESP-NOW-Verbindung zu einem zusätzlichen Waveshare-ESP mit Ethernet-Anschluss geplant. Dieser soll als Gateway zwischen Bewässerungscontroller und Heimnetz dienen. Die Weiterleitung der MQTT-Daten ist noch nicht implementiert.

Zusätzlich sind eine lokale Begrenzung der Ventillaufzeit und eine Absicherung der gleichzeitig aktiven Ausgänge direkt auf dem Controller vorgesehen. Bisher werden entsprechende Regeln hauptsächlich in Home Assistant umgesetzt.
