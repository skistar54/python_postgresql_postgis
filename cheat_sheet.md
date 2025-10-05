# 📘 Praktische Aufgaben – Spickzettel (Cheat Sheet)

## 🗂️ Aufgabenübersicht

### Jupyter Notebooks
| Aufgabe | Ziel | Hauptschritte |
| --- | --- | --- |
| **Python mit PostgreSQL & PostGIS – Einrichtung & Verbindung** | Öffne die Notebook-Tools und verbinde dich sicher mit der Datenbank. | Importiere Hilfsbibliotheken, ignoriere Warnungen, baue den Verbindungsstring auf und teste ihn mit einer einfachen Abfrage. |
| **Datenbankinhalt anzeigen** | Prüfe, welche Tabellen und Spalten bereits vorhanden sind, bevor du eigene Abfragen schreibst. | Führe eine SQL-Abfrage zur Tabellenauflistung aus und hole Spaltennamen sowie Datentypen über `information_schema`. |
| **Gebäude mit vollständiger Adresse** | Sammle Gebäude mit vollständigen Adressdaten in bestimmten Postleitzahlbereichen. | Verwende eine SQL-Abfrage, um Gebäude-Polygone nach Adressfeldern und PLZ zu filtern, lade sie mit GeoPandas und zeige sie an. |
| **Gebäudekarte** | Zeige die gefilterten Gebäude auf einer interaktiven Karte. | Zentriere die Karte auf die Mittelpunkte, füge eine GeoJSON-Schicht mit Popups hinzu und speichere die Karte als HTML. |
| **Cafés** | Finde alle Punkte in der Datenbank, die als Café markiert sind. | Führe eine Abfrage auf `planet_osm_point` mit Shop-Typ `coffee` aus, lade die Ergebnisse mit GeoPandas und zeige die ersten Zeilen. |
| **Cafékarte** | Zeige die Café-Standorte auf einer Basiskarte. | Falls nötig reprojiziere, zentriere die Karte, füge Popups mit Namen hinzu und exportiere die Karte. |
| **Supermärkte beim Bahnhof Winterthur** | Finde Supermärkte im Umkreis von 1 km um den Bahnhof und miss ihre Entfernung. | Verwende `ST_DWithin` und `ST_Distance` um den Bahnhofspunkt, lade die Ergebnisse und sortiere nach Distanz. |
| **Supermarkt-Entfernungskarte** | Visualisiere die Ergebnisse der Winterthurer Supermärkte. | Karte zentrieren, Popups mit Namen und Distanz hinzufügen und als HTML speichern. |
| **Autobahn-Puffer** | Erstelle einen kombinierten Puffer um Autobahnlinien. | Führe eine SQL-Abfrage aus, die einen Puffer in Metern erstellt, vereinigt (`union`), nach WGS84 transformiert und speichert. |
| **Autobahn-Pufferkarte** | Zeige den Autobahnpuffer auf einer interaktiven Karte. | Stelle sicher, dass das Koordinatensystem WGS84 ist, setze die Basiskarte, füge die GeoJSON-Schicht hinzu und speichere sie. |
| **Folium-Layout-Beispiel** | Erstelle eine wiederverwendbare Folium-Kartenvorlage. | Importiere Folium-Plugins, definiere eine `build_map()`-Funktion mit Ebenen, Markern, Clustern und Messwerkzeugen, dann rendern. |

### SQL-Aufgaben (Ordner *SQL*)
| Aufgabe | Ziel | Hauptschritte |
| --- | --- | --- |
| **Gebäude in Zürich 8001** | Liste Gebäude im PLZ-Bereich 8001 mit vollständigen Adressen. | Auswahl aus `planet_osm_polygon`, Filter nach Stadt, Straße und Postleitzahl, Umwandlung der Geometrie in WGS84. |
| **Entfernung zu Grossmünster** | Miss die Entfernung ausgewählter Gebäude zu einem Wahrzeichen. | Verwende `ST_Distance` zwischen Gebäude und Punkt, gib Meter zurück und transformiere die Geometrie. |
| **Distanz St. Gallen – Genf** | Berechne die Stadt-zu-Stadt-Distanz in Kilometern. | Nutze `ST_Distance` auf zwei Geografie-Punkten und konvertiere das Ergebnis in km. |
| **Autobahn-Puffer (Standalone-SQL)** | Erstelle Puffer um Autobahnen und fasse sie zusammen. | Führe separate Abfragen aus, die Linien um 1000 m puffern und vereinigen. |
| **Grünflächen pro Gemeinde** | Fasse Grünflächen innerhalb Zürichs zusammen. | Filtere Polygone nach Landnutzung, schneide sie am Stadtgrenz-Polygon, berechne Fläche in m² und summiere. |
| **Supermarkt-Markenfilter** | Zeige nur Migros und Aldi-Filialen an. | Wähle Supermarkt-Punkte, deren Namen Marken enthalten, und prüfe Adressfelder. |
| **Supermarkt-Puffer** | Erstelle 1 km-Puffer um alle Supermärkte. | Puffere jeden Punkt mit `ST_Buffer` und behalte die Originalgeometrie. |
| **Gebäude innerhalb von Supermarkt-Puffern** | Finde Häuser, die in der Nähe eines Supermarkts liegen. | Erstelle Supermarkt-Puffer, wähle Zürcher Gebäude und schneide sie mit `ST_Intersects`. |
| **Überlappende Supermarkt-Puffer** | Finde überlappende Versorgungsgebiete. | Führe einen Selbst-Join über Pufferschnittpunkte aus und gib gemeinsame Flächen aus. |
| **Supermärkte nahe Autobahnen** | Liste Supermärkte im 1 km-Umkreis einer Autobahn. | Verwende `ST_DWithin`, um Entfernungen zwischen Shops und Linien zu prüfen. |
| **Supermärkte beim Zürich HB** | Miss Entfernungen zum Hauptbahnhof Zürich. | Filtere Supermärkte im 2 km-Umkreis und berechne `ST_Distance`. |

### Erweiterte SQL-Aufgaben (Ordner *SQL_EXTENDED*)
| Aufgabe | Ziel | Hauptschritte |
| --- | --- | --- |
| **Gebäude innerhalb der Stadt Zürich** | Behalte nur Gebäude innerhalb der Stadtgrenze. | Erstelle das Stadtgrenzen-Polygon per CTE und wähle alle Gebäude, die darin liegen. |
| **Wälder innerhalb Zürichs** | Schneide Waldflächen auf die Stadt zu und ermittle ihre Größe. | Verwende `ST_Intersection`, transformiere in metrisches CRS und berechne Hektar. |
| **Hotels & nahe POIs** | Finde Hotels mit Freizeitangeboten im 250 m-Umkreis. | Verwende Stadtgrenzen-CTE, wähle Hotels, puffere sie, finde POIs innerhalb und zähle. |
| **Schweizer Gemeindebezirke** | Hole Grenzen der Schweizer Gemeinden mit Flächenangabe. | Abfrage administrativer Polygone auf Ebene 8 und Berechnung der Fläche in km². |

## ⚙️ Funktions- & Tool-Übersicht
- **pandas** – Liest Tabellen in DataFrames, damit man Ergebnisse wie Tabellen ansehen kann.  
- **geopandas** – Erweiterung von pandas für Geodaten (Geometriespalten direkt aus PostGIS).  
- **folium & Plugins** – Erstellt interaktive Webkarten mit Ebenen, Markern, Clustern und Messwerkzeugen, die als HTML speicherbar sind.  
- **SQLAlchemy (`create_engine`)** – Verbindung zwischen Python und PostgreSQL für SQL-Abfragen direkt aus dem Notebook.  
- **PostGIS-Funktionen** – Räumliche Funktionen wie `ST_Distance` (Entfernung), `ST_Buffer` (Puffer), `ST_Transform` (Koordinatensystem ändern).  
- **pgAdmin** – Web-Tool zum Durchsuchen der Datenbank, Ausführen von SQL und Anzeigen von Geometrien.  
- **osm2pgsql** – Kommandozeilentool zum Import von OpenStreetMap-Daten in die Datenbank.  
- **PostgreSQL + PostGIS-Datenbank** – Speichert Vektorlayer (Gebäude, Straßen, Shops) und ermöglicht räumliche SQL-Abfragen.

> Beispiel: `SELECT ST_Buffer(geom, 1000) FROM my_points;` erstellt einen 1 km-Puffer um jeden Punkt.

## 🧩 Konzeptverbindungen
- **Vektordaten** – Tabellen wie `planet_osm_point` und `planet_osm_polygon` speichern Punkt- und Polygon-Geometrien – passend zu den Vorlesungsinhalten.  
- **Koordinatensysteme & Projektionen** – `ST_Transform` wird verwendet, um zwischen metrischem CRS für Berechnungen und WGS84 für Karten zu wechseln.  
- **Räumliche Joins & Enthaltensein** – Funktionen wie `ST_Intersects` und `ST_Within` zeigen, welche Objekte sich überschneiden oder enthalten sind.  
- **Puffer & Näheanalyse** – `ST_Buffer` und `ST_DWithin` bilden Servicebereiche oder "in der Nähe"-Abfragen ab.  
- **Attributfilter & Zusammenfassungen** – Filterung und Aggregation nach Flächen oder Attributen entsprechen klassischen SQL-Auswertungen.  
- **Kartendarstellung** – Mit Folium werden Karten mit Popups und Messwerkzeugen gestaltet – analog zu den GIS-Konzepten aus der Vorlesung.

---

Behalte diesen Spickzettel griffbereit, während du an den Notebooks arbeitest, damit du die **Ziele**, **Schritte** und **wichtigsten Werkzeuge** jederzeit im Blick hast.
