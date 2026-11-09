# Home Assistant und Bewässerungsautomatisierung

## Systemarchitektur

Home Assistant OS wird in einer virtuellen Maschine auf einem lokalen Server betrieben. Der Bewässerungs-ESP32 verbindet sich derzeit per WLAN und MQTT mit dem Broker. Über MQTT-Discovery werden die Ventile und Sensorwerte als Entitäten in Home Assistant eingebunden.

## Umgesetzte Konfiguration

Die [Bewässerungs-Konfiguration](bewaesserung.yaml) umfasst:

- Globale Schalter für Automatik, das Überspringen des aktuellen Tages, Regensperre und Durchflussüberwachung
- Zeitpläne für jedes Ventil mit Wochentagen, Startzeit und Laufzeit
- Begrenzung der parallel aktiven Ventile (Standard: drei; einstellbar von eins bis vier)
- Maximale Laufzeit (Standard: 60 Minuten)
- Regenprognose für die nächsten sechs Stunden, Auswertung des Regensensors und Regennachlauf
- Durchfluss- und Lecküberwachung mit Benachrichtigungen
- Status- und Warnmeldungen für die Konfiguration
- Skripte für den manuellen Start und das gemeinsame Abschalten der Ventile

Die manuelle Steuerung und die Zeitpläne sind softwareseitig eingerichtet. Eine vollständige Prüfung aller Ventile und Schutzfunktionen unter realen Bewässerungsbedingungen steht noch aus.

## Bekannte Einschränkungen und geplante Verbesserungen

Einige Funktionen sind bereits in der YAML konfiguriert, müssen aber noch geprüft oder erweitert werden:

- Zeitplanverarbeitung: Die Zeitplan-Automation arbeitet mit `mode: queued`. Dadurch werden gleichzeitig anstehende Starts nacheinander abgearbeitet. Das Verhalten bei mehreren zeitgleichen Bewässerungsanforderungen ist noch zu testen.
- Begrenzung aktiver Ventile: Die Prüfung erfolgt derzeit in den vorgesehenen Zeitplan- und Startskripten. Ein direktes Schalten eines MQTT-Ventilschalters umgeht diese Prüfung. Eine Absicherung unabhängig vom gewählten Schaltweg ist als Erweiterung vorgesehen.
- Laufzeitbegrenzung: Die bisherige Abschaltlogik liegt in Home Assistant. Ergänzend ist eine unabhängige Laufzeitbegrenzung direkt auf dem ESP32 geplant, damit die Ventile auch bei einer unterbrochenen Serververbindung sicher abgeschaltet werden können.
- Durchflussüberwachung: Die Erkennung von fehlendem oder unerwartetem Durchfluss ist konfiguriert. Die Kalibrierung des Sensors sowie eine verbesserte Behandlung ungültiger Messwerte und Alarmmeldungen stehen noch aus.
- Neustart- und Ausfallszenarien: Das Verhalten bei einem Neustart von Home Assistant, bei Verbindungsabbrüchen und bei unterbrochenen Timern soll systematisch getestet werden.
- Entitäten und Templates: Vor einer Übernahme auf ein anderes Home-Assistant-System müssen die verwendeten Entitäts-IDs und Wetterdatenquellen geprüft werden.

Die vollständige Konfiguration ist unter [bewaesserung.yaml](bewaesserung.yaml) abgelegt. Die hier beschriebenen geplanten Verbesserungen sind noch nicht als umgesetzt zu verstehen.
