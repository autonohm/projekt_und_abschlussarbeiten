# Zentrales Repository für Abschluss- und Projektarbeiten des Labors Mobile Robotik

Die Themen werden unter https://autonohm.github.io/projekt_und_abschlussarbeiten/ veröffentlicht.

## Anleitung für das hinzufügen eines neuen Themas

0. ~~[Quarto](https://quarto.org/docs/get-started/) installieren.~~ *Update: Eine lokale Quarto Installation ist nicht mehr notwendig. Die HTML-Seite wird nun von Github Actions gerendert.*
1. Neues Dokument auf Basis des [tex-Templates](2025_99_template.tex) anlegen.
2. tex-Dokument kompilieren und das PDF im Ordner `build` ablegen.
3. tex-Dokument in `index.qmd` verlinken.
4. ~~`quarto render .` ausführen~~ *Falls eine lokale Quarto Installation vorhanden ist, kann die Seite für Preview-Zwecke lokal gerendert werden (aber bitte das html nicht aus versehen einchecken).* 
5. Pushen. Die Änderungen dann über Github Actions gepublisht.
