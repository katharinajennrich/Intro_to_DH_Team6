Readme zur Dokumentation von Forschungsdatensätzen

Ersteller Readme:				Baumann, Noah

Erstellungsdatum Readme:			2025-06-18
______________________________

Titel des Forschungsdatensatzes:		Berliner Nahverkehrsnetz 1946-1989: Transkribierte Fahrplandaten aus dem geteilten Berlin
						Berlin Public Transport Network 1946-1989: Transcribed Timetable Data from Divided Berlin

Ort der Datenerhebung:				Berlin, Deutschland

Version:					1.0
Versionenänderungen:				-

Herausgeber:					Baumann, Noah; Humboldt-Universität zu Berlin
Herausgeber Identifier:			https://explore.gnd.network/gnd/1220138-8
______________________________

Ersteller 1 des Datensatzes:			Baumann, Noah
Ersteller 1 Identifier:			https://orcid.org/0009-0004-6368-3061
Ersteller 1 Affiliation:			Humboldt-Universität zu Berlin

______________________________

Projektname:					Verkehrsgeschichte des geteilten Berlin: Netzwerkanalyse des öffentlichen Nahverkehrs 1946-1989
						Transport History of Divided Berlin: Network Analysis of Public Transit 1946-1989

______________________________

Kontext der Datenerhebung:			Dieser Datensatz dokumentiert die Entwicklung des öffentlichen
						Nahverkehrsnetzes in Berlin während der Teilung der Stadt (1946-1989).
						Die Daten basieren auf der systematischen Transkription von 36
						historischen Fahrplanbüchern der Berliner Verkehrsbetriebe (BVG), die im
						BVG-Archiv und in der Wilhelm-Grimm-Zentrum-Bibliothek archiviert sind.
						Ab 1955 wurden getrennte Fahrplanbücher für Ost- und West-Berlin
						veröffentlicht, was die administrative Teilung der Stadt und ihrer
						Verkehrssysteme widerspiegelt.

						Die transkribierten Daten umfassen folgende Zeitpunkte:
						- Gesamtberlin: 1946, 1951
						- Ost-Berlin: 1956, 1960, 1961, 1964, 1967, 1971, 1976, 1980, 1982, 1984, 1989
						- West-Berlin: 1956, 1960, 1961, 1964, 1967, 1971, 1976, 1980, 1982, 1984, 1989

						Fahrplanbücher für Ost-Berlin aus den Jahren 1961 bis 1970 wurden im
						Jacob-und-Wilhelm-Grimm-Zentrum unter der Signatur Pol. 1788:F8
						gefunden. Alle anderen Fahrplanbücher wurden im BVG-Archiv eingesehen,
						dort gibt es keine Signatur.

						Die Auswahl der Jahre erfolgte als repräsentative Stichprobe mit
						mindestens einem Datenpunkt pro Fünf-Jahres-Zeitraum, ergänzt um
						Perioden von besonderem historischen Interesse wie die frühen 1960er
						Jahre (Bau der Berliner Mauer) und die frühen 1980er Jahre
						(Wohnungsbauerweiterung in Ost-Berlin). Diese Auswahl wird in folgenden
						Versionen des Datensatzes ergänzt.

Datenumfang:					Der Datensatz umfasst:
						- 19.758 Stationseinträge über alle Jahre
						- 2.099 Linieneinträge
						- 28.982 eindeutige Verbindungen

Abstract:					Dieser Datensatz dokumentiert die Entwicklung des öffentlichen Nahverkehrsnetzes in Berlin während der 
						Teilung der Stadt (1946-1989) basierend auf 36 historischen Fahrplanbüchern der Berliner Verkehrsbetriebe 
						(BVG) aus dem BVG-Archiv und der Wilhelm-Grimm-Zentrum-Bibliothek.
						
						Die Daten umfassen 19.758 Stationseinträge, 2.099 Linieneinträge und 28.982 Verbindungen über repräsentative 
						Zeitpunkte mit mindestens einem Datenpunkt pro Fünf-Jahres-Zeitraum. Ab 1955 spiegeln getrennte Datensätze 
						für Ost- und West-Berlin die administrative Teilung wider.
						
						Struktur: Drei relationale CSV-Tabellen (UTF-8):
						- stations.csv: Stationsdaten mit Geolokation (WGS84), Name, Typ, bedienende Linien
						- lines.csv: Liniendaten mit Verkehrsmitteltyp, Fahrzeit, Frequenz (7:30 Uhr werktags), Start/Ziel
						- line_stops.csv: Haltestellenreihenfolge je Linie
						
						Normalisierungen: Kreuzungsnamen wurden bei Bus-/Straßenbahnhaltestellen ergänzt (Format "X Ecke Y"). 
						S-Bahn-Daten aus Reichsbahn-Quellen ergänzt. Geolokalisierung durch Wikidata, historische Karten und 
						Distanzvalidierung.
						
						Einschränkungen: Bus-/Straßenbahnhaltestellen nur selektiv erfasst (als "wichtig" eingestuft, ab 1975 
						West-Berlin vollständig). Frequenzdaten nur für 7:30 Uhr werktags.

Schlagwörter:					Berliner Mauer, Kalter Krieg, Öffentlicher Nahverkehr, Verkehrsgeschichte, Stadtentwicklung, 
						BVG, DDR, Netzwerkanalyse, Historische Geodaten, Geteiltes Berlin

Methode der Datenerhebung: 			Die Transkription erfolgte manuell aufgrund der Komplexität der
						historischen Fahrplanbuch-Layouts. Dabei wurden folgende
						Normalisierungen vorgenommen:

						Stationsnamen: Bei Bus- und Straßenbahnhaltestellen wurden in
						einigen Fällen Kreuzungsnamen zur eindeutigen Geolokalisierung ergänzt.
						Das Format "X Ecke Y" bezeichnet dabei X als den originalen
						Haltestellennamen aus dem Fahrplanbuch und Y als die querenden Straße
						gemäß dem Linienverlauf. Straßenbezeichnungen wurden standardisiert
						("Straße", "Allee", "Chaussee").

						Vollständigkeit der Stationen: Während U-Bahn- und S-Bahn-Stationen
						vollständig erfasst sind, enthalten die Fahrplanbücher für Straßenbahn-
						und Buslinien nur als "wichtig" eingestufte Haltestellen. Die
						Definition von "wichtig" variierte zwischen Jahren und
						Verwaltungszonen. Ab 1975 sind in West-Berliner Fahrplanbüchern alle
						Haltestellen verzeichnet.

						S-Bahn-Daten: Da die S-Bahn von der Reichsbahn und nicht von der BVG
						betrieben wurde, mussten diese Informationen aus zusätzlichen
						Reichsbahn-Quellen ergänzt werden.

						Geolokalisierung: Die Koordinatenbestimmung erfolgte durch:
						- Abgleich mit Wikidata-Einträgen (primär für U-Bahn, S-Bahn und teils
						  für Straßenbahn)
						- Historische Karten und Linienverlaufsbeschreibungen
						- Kreuzungsanalyse für Bus- und Straßenbahnhaltestellen
						- Validierung durch Distanzprüfungen zwischen aufeinanderfolgenden
						  Stationen (sowohl auf zu geringe als auch zu große Abstände)
						- Visuelle Überprüfung der Koordinaten

Beschreibung der Datenstruktur:			Der Datensatz besteht aus drei relationalen CSV-Tabellen (UTF-8 kodiert)
						und stellt die transkribierte Grundlage vor weiterführenden
						Netzwerkmodellierungen dar:

						stations.csv - Stationsdaten:
						- stop_id (String): Eindeutige ID im Format JAHR+NUMMER
						- stop_name (String): Stationsname (ggf. mit Kreuzungsinformation)
						- typ (String): Verkehrsmitteltyp der bedienenden Linie
						- standort (String): Koordinaten im WGS84-Format (Latitude,Longitude)
						- in_linien (String): Liste der bedienenden Linien
						- wikidata_id (String): Wikidata-ID (falls vorhanden)

						lines.csv - Liniendaten:
						- line_id (String): Eindeutige ID im Format JAHR+NUMMER
						- jahr (Integer): Jahr des Fahrplanbuchs
						- linien_name (String): Linienbezeichnung
						- typ (String): Verkehrsmittel (straßenbahn, u-bahn, s-bahn,
						  autobus, omnibus, oberleitungsbus, fähre)
						- dauer (min) (Float): Fahrzeit zwischen Endstationen in Minuten
						- ost_west (String): Verwaltungszone (ost, west, both/unknown)
						- frequenz (Float): Taktfrequenz um 7:30 Uhr werktags in Minuten
						- länge (km) (Float): Streckenlänge in Kilometern
						- start (String): Anfangshaltestelle
						- ziel (String): Endhaltestelle

						line_stops.csv - Haltestellenreihenfolge:
						- line_id (String): Referenz zur Linie
						- stop_order (Integer): Position der Haltestelle auf der Linie
						- stop_id (String): Referenz zur Station

Datenqualität und Einschränkungen:		1. Unvollständige Haltestellenerfassung: Für Bus- und
						   Straßenbahnlinien sind nur ausgewählte Haltestellen dokumentiert,
						   wobei die Auswahlkriterien zwischen Jahren und Regionen variieren.

						2. Zeitliche Einschränkung: Die Frequenzdaten beziehen sich
						   ausschließlich auf 7:30 Uhr an Werktagen. Tages-, Wochen- und
						   Saisonvariationen sind nicht erfasst.

						3. Statische Darstellung: Die Daten repräsentieren den geplanten
						   Idealzustand ohne temporäre Umleitungen oder Baumaßnahmen.

						4. Geolokalisierungsgenauigkeit: Die Koordinaten von Bus- und
						   Straßenbahnhaltestellen basieren teils auf Kreuzungsschätzungen und
						   können von den exakten historischen Positionen abweichen.

Nutzungshinweise:				Dieser Datensatz stellt die transkribierte Grundlage dar, mit
						Neugruppierungen und Geodaten-Erweiterungen. Weitere
						Netzwerkmodellierungen werden mit diesem Datensatz durchgeführt und auf
						Zenodo publiziert. Der Datensatz eignet sich für:
						- Historische Verkehrsanalysen
						- Netzwerkevolutionsstudien
						- Zugänglichkeitsuntersuchungen
						- Vergleichende Stadtentwicklungsforschung
						- Verbindungen mit anderen geo-temporalen Daten

						Für weiterführende Netzwerkanalysen empfiehlt sich die Transformation in
						geeignete Graphenstrukturen. Dazu werden weitere Dokumente hier in
						kurzer Zeit veröffentlicht.

______________________________

Dateiliste:					stations.csv - Stationsdaten (stop_id, stop_name, typ, standort, in_linien, wikidata_id)
						lines.csv - Liniendaten (line_id, jahr, linien_name, typ, dauer (min), ost_west, frequenz, länge (km), start, ziel)
						line_stops.csv - Haltestellenreihenfolge (line_id, stop_order, stop_id)
						README.txt - Diese Datei

Dateiformate: 					.csv, .txt

______________________________

Anmerkungen: 					Erstellt im Rahmen des FAIRDATA Fellowship des Deutschen Museums. Dank an das BVG-Archiv und die 
						Wilhelm-Grimm-Zentrum-Bibliothek für den Zugang zu den historischen Fahrplanbüchern. Dieser Datensatz 
						bildet die Grundlage für weiterführende Netzwerkanalysen im Rahmen einer Dissertation zur Berliner 
						Verkehrsgeschichte.