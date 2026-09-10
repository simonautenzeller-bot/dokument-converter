# Formatwerkstatt

Statischer Bulk-Konverter fuer Dokumente und Bilder. Die Website besteht aus einer flachen
Dateistruktur und kann direkt mit GitHub Pages veroeffentlicht werden.

## Zwei Werkzeuge in einer App

Auf der Startseite waehlt man oben per zwei grossen Kacheln den Modus:

- **📄 Dokumente** - PDF, Word (.docx), TXT, Markdown, HTML, RTF ineinander umwandeln.
- **🖼️ Bilder** - SVG, PNG, JPG und WEBP ineinander umwandeln (inkl. Groessenskalierung).

Beide Modi teilen sich dieselbe Bedienung: Datei(en) ablegen, Zielformat waehlen, auf
"Jetzt umwandeln" klicken. Die Oberflaeche ist bewusst reduziert (grosse Schrift, wenige
Schritte, kein Fachjargon), damit auch ungeuebte Nutzer sie auf einen Blick verstehen;
seltener benoetigte Optionen stecken eingeklappt unter "⚙ Weitere Einstellungen".

## GitHub Pages

1. Das Repository zu GitHub pushen.
2. Unter **Settings > Pages** bei **Build and deployment** die Option **Deploy from a branch** waehlen.
3. Den Branch `main` und den Ordner `/(root)` auswaehlen und speichern.
4. Die von GitHub angezeigte Pages-URL oeffnen. `index.html` leitet direkt zum Konverter weiter.

## Dateien

- `index.html`: GitHub-Pages-Einstieg im Repository-Root.
- `dokument-konverter.html`: Vollstaendiges Tool fuer Mehrfachauswahl und Konvertierung.

Die Seite verwendet externe Browser-Bibliotheken per HTTPS-CDN. Deshalb muss sie fuer die
Konvertierung online geladen werden; ein Build-Schritt und ein Server sind nicht erforderlich.

## Speicherort beim Download

Beim Klick auf "Jetzt umwandeln" fragt das Tool in Chrome/Edge per "Speichern unter"-Dialog
(File System Access API) nach Ordner und Dateiname, bevor die Konvertierung startet. In Browsern
ohne diese API (z. B. Firefox, Safari) faellt das Tool automatisch auf den normalen Download
zurueck; die Datei landet dann ohne Rueckfrage im Standard-Download-Ordner des Browsers. Bei
mehreren Dateien auf einmal wird automatisch ein ZIP-Archiv gespeichert.

## Notenblaetter, Scans und andere PDFs ohne Text-Layer

PDF-Text wird per pdf.js aus dem eingebetteten Text-Layer gelesen. Musiknoten, Scans und
sonstige Grafiken haben keinen brauchbaren Text-Layer, weshalb dabei nur einzelne Textzeilen
(z. B. Titel oder Liedtext) uebrig bleiben und die eigentliche Notation verloren geht.

Die Checkbox **"Notenblätter & Scans: PDF-Seiten als Bild einbetten"** im Konverter umgeht das:
Jede PDF-Seite wird mit pdf.js in einen Canvas gerendert und als Bild in die Zieldatei (.docx,
.pdf oder .html) eingebettet. Das Layout bleibt dadurch pixelgenau erhalten, ist im Ergebnis aber
nicht mehr editierbar (keine echte Notenerkennung/OMR). Fuer .txt, .md und .rtf ist das Verfahren
nicht sinnvoll; dort wird weiterhin der Text-Layer extrahiert.

## Songtexte mit Akkorden (Chord Sheets)

Liedtexte mit Gitarrenakkorden (z. B. "G", "C", "em", "D") ueber den Textzeilen sind kein
Notenbild, sondern echter Text - pdf.js liest Akkorde und Text korrekt aus, aber der Standard-
Export verwirft dabei alle Zeilenumbrueche und die horizontale Ausrichtung, wodurch die Akkorde
nicht mehr ueber dem passenden Wort stehen.

Die Checkbox **"Songtexte mit Akkorden: Zeilenumbrüche & Ausrichtung beibehalten"** behaelt
Zeilenumbrueche bei und rekonstruiert die horizontale Position jedes Worts ueber Leerzeichen
(wie ein klassisches Text-Chord-Chart), gesetzt in der normalen Dokumentschrift (Georgia) statt
einer Schreibmaschinenschrift. Zeilen, die nur aus Akkord-Symbolen bestehen (z. B. "G", "Em",
"D7"), werden automatisch erkannt und fett + blau (14pt Liedtext, 10pt Akkorde) hervorgehoben -
genau wie in handformatierten Chord-Sheets in Word ueblich. Das Ergebnis ist normaler,
vollstaendig editierbarer Text - Akkorde bleiben dabei ungefaehr ueber der richtigen Silbe stehen.
Gilt fuer .docx (mit Formatierung) sowie .html (mit Formatierung), .txt und .md (als Codeblock,
ohne Formatierung, da reiner Text keine Farben/Fett kennt); .rtf faellt auf den normalen
Fließtext zurueck.