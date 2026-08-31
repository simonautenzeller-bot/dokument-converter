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