# Hardware und PCB-Entwicklung

## Grundlage
Schaltplan und Leiterplattenlayout der Bewässerungssteuerung wurden mit KiCad erstellt. Die folgende Bauteilübersicht basiert auf der Stückliste (CSV) des aktuellen Leiterplattenprojekts.

| Bauteil | Anzahl | Wert / Typ |
|---|---:|---|
| Mikrocontroller | 1 | DFRobot FireBeetle 2 ESP32-E |
| Leistungstransistoren Q1–Q8 | 8 | IRLZ44N |
| Freilaufdioden D1–D8 | 8 | 1N4007 |
| Gate-Widerstände | 8 | 300 Ω |
| Weitere Widerstände | 10 + 1 + 1 | 10 kΩ, 20 kΩ, 47 kΩ |
| DC/DC-Wandler | 1 | TRACO TSR2-2450N |
| Sicherung | 1 | 5 A |
| Puffer-/Entstörkondensatoren | 6 | 4 × 100 nF, 470 µF / 25 V, 100 µF / 10 V |

Die GPIO-Zuordnung der aktuellen Firmware ist in [firmware/bewaesserung.yaml](../firmware/bewaesserung.yaml) dokumentiert. Frühere Pinbelegungen entsprechen nicht mehr dem aktuellen Stand.

## Sensoren
- RS12-Regensensor: GPIO36, invertiertes Digitalsignal
- YF-B7-Durchflusssensor: GPIO35, Impulsmessung; derzeit 660 Impulse/L als Näherungswert
- NTC-Wassertemperatur: GPIO34, ADC mit Widerstands- und NTC-Umrechnung

## Bilddokumentation

KiCad-Schaltplan

<img src="../docs/images/bew%C3%A4sserung%20PCB%20schaltplan.jpg" alt="Schaltplan der Bewässerungssteuerung" width="540">

Leiterplattenlayout

<img src="../docs/images/bew%C3%A4sserung%20PCB%20desgin.jpg" alt="PCB-Layout in KiCad" width="540">

Teilbestückter Prototyp – Vorderseite

<img src="../docs/images/Bew%C3%A4sserung%20PCB.jpg" alt="Leiterplattenoberseite mit ESP32" width="380">

Leiterplattenrückseite – nachträgliche Anpassung des Regensensorsignals

<img src="../docs/images/bew%C3%A4sserung%20PCB%20backside.jpg" alt="Leiterplattenrückseite mit zusätzlichem Widerstand" width="380">

## Bestückungsstand und Anpassung des Regensensors

Die gefertigte Leiterplatte ist bislang teilweise bestückt. Der FireBeetle-Controller ist montiert; Spannungsversorgung und Sensoranschlüsse sind aufgebaut. Von acht vorgesehenen Ventilstufen ist bislang eine bestückt. Die vollständige Bestückung und die Prüfung unter realen Wasserdrücken stehen noch aus, da die Gartenleitungen und Verteiler noch nicht fertiggestellt sind.

Regensensor RS12: Bei der Inbetriebnahme wurde festgestellt, dass das Ausgangsverhalten des Sensors von der in der Anleitung beschriebenen Open-Collector-Schaltung abweicht. Da diese Abweichung bei den ersten Tests nicht erkannt wurde, war eine Anpassung der bereits gefertigten Leiterplatte erforderlich. Dazu wurde auf der Leiterplattenrückseite ein zusätzlicher Widerstand zwischen Regensignal und GND angebracht. Die Pegelanpassung an den ESP32 erfolgt über einen Spannungsteiler. Die elektrische Funktion dieser Anpassung wurde erfolgreich geprüft. Der zusätzliche Widerstand ist als dauerhafte Lösung vorgesehen; eine erneute Fertigung der Leiterplatte ist derzeit nicht geplant. Die Änderung ist auf dem Foto der Leiterplattenrückseite erkennbar und wurde noch nicht in die KiCad-Dateien übernommen.

## Entwicklungsablauf
1. Anforderungen an die Bewässerungszonen und die Ventillasten festlegen
2. Schaltplan und Bauteilauswahl in KiCad ausarbeiten
3. Leiterplattenlayout für Leistungs- und Sensorsignale erstellen
4. Leiterplatte fertigen lassen, teilweise bestücken und elektrisch prüfen
5. Controller mit ESPHome und Home Assistant verbinden

## Noch ausstehende Arbeiten

- Die restlichen sieben Ventilstufen bestücken und prüfen
- Den Durchflusssensor unter realen Bedingungen kalibrieren
- Die Temperaturmessung kalibrieren
- Die dauerhaft vorgesehene Anpassung des Regensensors in den KiCad-Dateien dokumentieren
- Die gesamte Bewässerung nach Fertigstellung der Gartenleitungen hydraulisch testen
- Die geplanten lokalen Sicherheitsfunktionen ergänzen und erproben

Die geplante ESP-NOW-Verbindung zu einem zusätzlichen Waveshare-ESP mit Ethernet-Anschluss ist in der [Projektübersicht](../README.md) beschrieben. Sie ist noch nicht umgesetzt.

Die KiCad-Quelldateien liegen direkt unter [kicad/](kicad/), darunter [Projekt](kicad/PCB_bewässerung.kicad_pro), [Schaltplan](kicad/PCB_bewässerung.kicad_sch), [PCB-Layout](kicad/PCB_bewässerung.kicad_pcb), Symbol- und Footprint-Bibliotheken sowie die [Originalstückliste](kicad/PCB_bewässerung.csv). Eine ergänzende [vereinfachte Stückliste](kicad/PCB_bewaesserung_BOM.csv) ist ebenfalls enthalten.
