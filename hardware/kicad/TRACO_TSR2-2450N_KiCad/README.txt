TRACO TSR 2-2450N – KiCad-Projektbibliothek
============================================

Enthalten:
- TRACO_TSR2N.kicad_sym
- TRACO_TSR2N.pretty/Converter_DCDC_TRACO_TSR-2-2450N_THT.kicad_mod

Bibliotheken einbinden
----------------------
1. Den gesamten entpackten Ordner in den KiCad-Projektordner kopieren.
2. Schaltplaneditor: Einstellungen -> Symbolbibliotheken verwalten -> Projektspezifische Bibliotheken -> vorhandene Bibliothek hinzufügen.
   Datei: TRACO_TSR2N.kicad_sym
   Empfohlener Name: TRACO_TSR2N
3. PCB-Editor: Einstellungen -> Footprint-Bibliotheken verwalten -> Projektspezifische Bibliotheken -> vorhandene Bibliothek hinzufügen.
   Ordner: TRACO_TSR2N.pretty
   Bibliotheksname muss TRACO_TSR2N sein, damit die Footprint-Zuordnung im Symbol direkt stimmt.
4. Im Schaltplan mit A nach TSR_2-2450N suchen und platzieren.

Pinbelegung
-----------
Pin 1: +VIN  -> +12V
Pin 2: GND   -> GND
Pin 3: +VOUT -> +5V

Empfohlene Beschaltung für das Bewässerungsboard
-------------------------------------------------
Eingang nahe am Wandler:
- 100 nF Keramikkondensator zwischen +12V und GND
- 22 uF / mindestens 25 V Elektrolytkondensator zwischen +12V und GND

Ausgang nahe am Wandler bzw. FireBeetle:
- 100 nF Keramikkondensator zwischen +5V und GND
- 47 uF / mindestens 10 V Elektrolytkondensator zwischen +5V und GND

FireBeetle:
- +5V an den VCC-Pin anschließen, nicht an 3V3.
- GND gemeinsam verbinden.
- Beim Programmieren über USB die externe 12-V-Versorgung am sichersten abschalten.

Layout
------
- Wandler und Kondensatoren dicht zusammen platzieren.
- +5V-Leiterbahn für bis zu 2 A etwa 1 mm oder breiter ausführen, bei längeren Wegen breiter.
- GND-Fläche verwenden.
- Wandler und andere Bauteile nicht direkt an die Antennenseite des FireBeetle setzen.
- Der Footprint wurde nach dem TRACO-Datenblatt vom 19.02.2025 erstellt: 14.0 x 7.6 mm, Raster 2.54 mm, Pins 1-2-3.
