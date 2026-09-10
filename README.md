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