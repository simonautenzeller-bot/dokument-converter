# Formatwerkstatt

Statischer Bulk-Konverter fuer Textdokumente. Die Website besteht aus einer flachen
Dateistruktur und kann direkt mit GitHub Pages veroeffentlicht werden.

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
(wie ein klassisches Text-Chord-Chart), gesetzt in einer Schreibmaschinenschrift (Consolas). Das
Ergebnis ist normaler, vollstaendig editierbarer Text - Akkorde bleiben dabei ungefaehr ueber der
richtigen Silbe stehen. Gilt fuer .docx, .txt, .md (als Codeblock) und .html (als `<pre>`); .rtf
faellt auf den normalen Fließtext zurueck.