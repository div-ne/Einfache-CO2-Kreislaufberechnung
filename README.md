# CO2 Kreislaufberechnung

## Funktionen

- Berechnung eines **CO2-Kreislaufs** auf Basis von **Kälteleistung**, **Wärmeleistung** oder **Verdichtervolumenstrom**.
- Auslegung für **subkritischen** und **transkritischen** Betrieb, abhängig vom gewählten bzw. berechneten Gaskühlerdruck.
- Ausgabe der **Kreislaufpunkte** mit Temperatur, Druck, spezifischer Enthalpie, Dichte, spezifischer Entropie und Dampfqualität.
- Optionale **Rohrleitungsdimensionierung** für Heissgas-, Flüssigkeits- und Saugleitung mit den Varianten „minimaler Druckverlust“ und „minimaler Durchmesser“.
- Export aller berechneten Ergebnisse als **CSV-Datei**, bestehend aus Systemdaten, Kreislaufpunkten und optional Rohrleitungsdimensionierung.
- Integrierte **Anleitung** mit Kurzbeschreibung der Anwendung und Hinweis auf die verwendete Rohrreibungszahl-Logik.

## Oberfläche

Die Oberfläche ist im Stil der einfachen Kreislaufberechnung aufgebaut: Eingabefelder stehen links, die Systemdaten werden rechts ausgegeben und die weiteren Ergebnistabellen darunter dargestellt.

Die App zeigt Titel und Versionsnummer im Kopfbereich an; in der aktuellen CO2-Version ist die Version auf **0.9.3V** gesetzt.

## Eingabeparameter

Folgende Eingaben stehen in der App zur Verfügung:

- Projektname
- Eingabemodus
- Kälteleistung, Wärmeleistung oder Verdichtervolumenstrom, abhängig vom gewählten Modus
- Gaskühleraustrittstemperatur
- Verdampfungstemperatur
- Gaskühlerdruck, automatisch oder manuell
- Verdampferüberhitzung
- Saugleitungsüberhitzung
- Aktivierung der Rohrleitungsdimensionierung
- Rohrleitungsoptimierung nach Druckverlust oder Durchmesser
- Leitungslängen für Heissgas-, Flüssigkeits- und Saugleitung

Die aktuell gesetzten Standardwerte sind unter anderem `Projekt`, `Gaskühleraustrittstemperatur = 35 °C`, `Verdampfungstemperatur = -10 °C`, `Verdampferüberhitzung = 6 K`, `Saugleitungsüberhitzung = 9 K`, `Heissgasleitungslänge = 5 m`, `Flüssigkeitsleitungslänge = 2.5 m` und `Saugleitungslänge = 3 m`.

## CO2-spezifische Berechnung

Die Anwendung verwendet **CO2** als festes Arbeitsmedium und bestimmt den Prozessbereich anhand des Hochdruckniveaus automatisch als **subkritisch** oder **transkritisch**.

Der Gaskühlerdruck kann entweder automatisch über die hinterlegte Näherungsfunktion bestimmt oder manuell vorgegeben werden.

Zusätzlich wird der erkannte Prozessbereich in den **Systemdaten** ausgegeben.

## Rohrleitungsdimensionierung

Die Rohrleitungsberechnung verwendet hinterlegte Kupferrohrabmessungen und bewertet je Leitung Strömungsgeschwindigkeit, Jacobs-Geschwindigkeit, Druckverlust, Außenmantelfläche und Innenvolumen.

Die Variante **minimaler Druckverlust** wählt die größte zulässige Rohrgröße innerhalb des jeweiligen Druckverlustkriteriums, während **minimaler Durchmesser** die kleinste zulässige Rohrgröße unter demselben Grenzwert auswählt.

Für die **Rohrreibungszahl** wird die funktionierende Logik aus der einfachen Kreislaufberechnung verwendet, damit der bekannte Fehler aus der alten CO2-Datei nicht übernommen wird.

## CSV-Export

Über den Button **„CSV herunterladen“** wird eine Auswertungsdatei mit Semikolon als Trennzeichen und UTF-8-BOM erzeugt, damit sich die Datei in Tabellenprogrammen wie Excel in der Regel direkt sauber öffnen lässt.

Die CSV enthält in der **ersten Zeile** den Programmtitel und die Versionsnummer.

Danach folgen die Abschnitte:

- Systemdaten
- Kreislaufpunkte
- Rohrleitungsdimensionierung, sofern aktiviert

## Technische Basis

Die Anwendung basiert auf **Streamlit** für die Oberfläche, **CoolProp** für Stoffdaten und thermodynamische Zustandsgrößen, **NumPy** und **Pandas** für Berechnung und Datenaufbereitung sowie **SciPy** für numerische Lösungsverfahren mit `brentq`.

## Hinweise

Die Anwendung ist für schnelle Überschlagsrechnungen und die kompakte Darstellung thermodynamischer Zustände eines CO2-Kreislaufs gedacht.

Für die Ergebnisqualität sind plausible Eingabedaten entscheidend; insbesondere bei manuell gesetztem Gaskühlerdruck, bei Grenzbereichen zwischen subkritischem und transkritischem Betrieb sowie bei der Rohrleitungsdimensionierung sollten die Eingaben fachlich passend zur betrachteten Anlage gewählt werden.
