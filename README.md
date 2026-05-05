# CoolChain Monitoring RSE

Der Hersteller **Food Solution Hildesheim** produziert Bio-Dönerspieße und bietet seinen Endkunden eine zertifizierte Kühlkette an.  
Die Einhaltung der Kühlkette kann vom Endkunden über einen **QR-Code** überprüft werden.

Dieses Projekt wurde durchgeführt von:

- Alexander Holzenkamp
- Fynn Bremer
- Tom Stoelken

---

## Projektbeschreibung

Dieses Python-Programm überprüft für vorgegebene Transport-IDs, ob die Kühlkette eingehalten wurde.  
Das Projekt baut auf **CoolChainProjekt Phase 1** auf und wurde in **Phase 2** um zusätzliche Funktionen erweitert.

Ziel des Programms ist es, Fehler in der Kühlkette automatisch zu erkennen und verständlich auszugeben.

---

## Projektphase 1

In Phase 1 wurden die grundlegenden Prüfungen der Kühlkette umgesetzt.

Das Programm prüft folgende Kriterien:

### Stimmigkeit je Transportstation

- Jede Transportstation besitzt ein Einchecken und ein Auschecken.
- Die Reihenfolge der Einträge muss zeitlich korrekt sein.
- Die erwartete Reihenfolge lautet: `in → out`.

### Übergaben ohne Kühlung

- Zwischen dem Auschecken aus einer Station und dem Einchecken in die nächste Station dürfen maximal **10 Minuten** liegen.
- Wird diese Zeit überschritten, gilt die Kühlkette als fehlerhaft.

### Gesamttransportdauer

- Die gesamte Transportdauer eines Produkts darf maximal **48 Stunden** betragen.
- Wird diese Grenze überschritten, wird ein Fehler ausgegeben.

---

## Projektphase 2

In Phase 2 wurde das bestehende Programm um drei neue Funktionen erweitert.

### Temperaturüberwachung

Die Temperaturdaten der Kühlstationen werden aus der Tabelle `tempdata` ausgewertet.

- Erlaubter Temperaturbereich: **+2 °C bis +4 °C**
- Temperaturabweichungen werden erkannt und ausgegeben.
- Die Prüfung dient der zusätzlichen Qualitätssicherung während Transport und Lagerung.

### Entschlüsselung verschlüsselter Daten

In Phase 2 liegen bestimmte Stammdaten verschlüsselt vor.  
Das Programm entschlüsselt diese Daten, damit sie weiterverarbeitet werden können.

Verwendete Tabellen:

- `company_crypt`
- `transportstation_crypt`

Verwendetes Verfahren:

- AES-Verschlüsselung
- CBC Mode
- PyCryptodome-Bibliothek

### Wetterdaten bei Übergabefehlern

Wenn eine Übergabe ohne Kühlung länger als 10 Minuten dauert, wird zusätzlich die Außentemperatur am Auslagerungsort abgefragt.

- Datenquelle: **Visual Crossing Weather API**
- Abfrage über Postleitzahl und Zeitpunkt
- Ausgabe der Wetterinformation direkt in der Fehlermeldung

---

## Projektstruktur

Die Projektdateien sind folgendermaßen aufgebaut:

```text
coolchain-monitoring-RSE/
├── src/
│   ├── main.py
│   ├── temperaturueberwachung.py
│   ├── entschluesselung.py
│   ├── wetterdaten_abfrage.py
│   └── Doxyfile
├── docs/
├── README.md
└── Start_Kuehlkette.bat
