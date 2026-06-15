# Neue Ausschreibung veröffentlichen

Erstelle eine neue wissenschaftliche Ausschreibung (Projekt-, Bachelor-, Masterarbeit oder M-APR) basierend auf der folgenden Eingabe und veröffentliche sie automatisch in beiden Repos.

**Eingabe des Nutzers:**
$ARGUMENTS

---

## Schritt 1 — Informationen extrahieren

Leite aus der Eingabe folgende Felder ab (frage nur nach, wenn etwas wirklich fehlt und sich nicht sinnvoll ableiten lässt):

- **Titel** (Deutsch)
- **Typ**: Kombination aus `Projektarbeit`, `Bachelorarbeit`, `Masterarbeit`, `M-APR`
- **Abstract** (Deutsch, 2–4 Absätze)
- **Arbeitspakete** (Deutsch, 4–6 Punkte)
- **Voraussetzungen** (Deutsch, 4–6 Punkte)
- **Ort**: `Labor für mobile Robotik` oder `TTZ Nürnberger Land` oder beides
- **Co-Betreuer** (optional, Name + E-Mail)
- **Startdatum** (falls M-APR, z.B. `WiSe 2026/2027`)

Übernimm folgende Werte immer fest:
- Betreuer: **Prof. Dr. Christian Pfitzner** · christian.pfitzner@th-nuernberg.de
- Repo forschungsgruppe-mobile-robotik (ehem. wissenschaftliche_arbeiten): `c:\Users\Chris\Documents\GitHub\embedded_projects\wissenschaftliche_arbeiten`
- Repo projekt_und_abschlussarbeiten: `c:\Users\Chris\Documents\GitHub\projekt_und_abschlussarbeiten`

---

## Schritt 2 — Slug und Dateinamen ableiten

- **Slug**: `YYYY-MM-kurzname` (aktuelles Jahr, Monat, 3–5 Wörter aus dem Titel, Kleinbuchstaben, Bindestriche, keine Umlaute)
- **LaTeX-Dateiname**: `YYYY_MM_kurzname` (Unterstriche)
- **Tags**: Technische Schlagworte + alle zutreffenden Typen (`Masterarbeit`, `Bachelorarbeit`, `Projektarbeit`, `M-APR`)
- **Categories**: nur die zutreffenden Typen

---

## Schritt 3 — Hugo-Markdown erstellen (forschungsgruppe-mobile-robotik)

Erstelle den Ordner `content/publication/<slug>/` und darin zwei Dateien.

**`index.md`** (Deutsch) — Front-Matter:
```yaml
---
title: '<Titel DE>'
authors:
  - admin
date: '<YYYY-MM-DDT00:00:00Z>'
publishDate: '<YYYY-MM-DDT00:00:00Z>'
publication_types: ['thesis']
publication: "<Typ>, <Ort>"
publication_short: "<Ort kurz>"
abstract: |
  <Abstract DE>
summary: '<1-2 Sätze DE>'
tags:
  - <technische Tags>
  - <Typ-Tags>
categories:
  - <Typ-Tags>
featured: true
url_pdf: ''
url_code: ''
url_dataset: ''
url_poster: ''
url_project: ''
url_slides: ''
url_source: ''
url_video: ''
image:
  caption: ''
  focal_point: 'Smart'
  preview_only: false
projects: []
slides: ''
---
```
Danach: Abschnitte `## Beschreibung`, `## Arbeitspakete`, `## Voraussetzungen`, `## Betreuung` (Tabelle mit Name + E-Mail).

**`index.en.md`** (Englisch) — gleiche Struktur, alle Inhalte professionell ins Englische übersetzt.

---

## Schritt 4 — Commit in forschungsgruppe-mobile-robotik

```
git add content/publication/<slug>/
git commit -m "Neue Ausschreibung: <Titel DE>"
git push origin main
```

---

## Schritt 5 — LaTeX-Dateien erstellen (projekt_und_abschlussarbeiten)

Erstelle zwei `.tex`-Dateien im Repo-Root `c:\Users\Chris\Documents\GitHub\projekt_und_abschlussarbeiten\`.

Vorlage für **`<latex_dateiname>.tex`** (Deutsch):
```latex
\documentclass{ohm_project_description}

\projecttitle{<Titel DE>}
\projectauthor{<Ort>}
\projectdate{<Jahr>}

\begin{document}
\maketitle
\thispagestyle{fancy}

<Abstract DE als Fließtext, 1–2 Absätze>

\section*{Arbeitspakete}
\begin{itemize}[leftmargin=0.5cm]
    \setlength\itemsep{.1em}
    <\item pro Arbeitspaket>
\end{itemize}

\section*{Voraussetzungen}
\begin{itemize}[leftmargin=0.5cm]
    \setlength\itemsep{.1em}
    <\item pro Voraussetzung>
\end{itemize}

\vspace{0.5cm}
Das Thema kann nach Abstimmung als \textbf{<Typ>} bearbeitet werden.

\vfill
\textcolor{ohm_red}{\rule{\linewidth}{0.4mm}}
\textbf{\textcolor{ohm_red}{<Ort>}} \\
\begin{tabular}{@{}ll}
\textbf{Betreuer:} & Prof. Dr. Christian Pfitzner \\
\textbf{E-Mail:}   & \href{mailto:christian.pfitzner@th-nuernberg.de}{christian.pfitzner@th-nuernberg.de} \\
<ggf. Co-Betreuer-Zeilen>
\end{tabular}

\end{document}
```

Vorlage für **`<latex_dateiname>_en.tex`** (Englisch):
- Identische Struktur, aber `\usepackage[english]{babel}` nach `\documentclass`
- Alle Texte professionell ins Englische übersetzt
- `\textbf{Supervisor:}` statt `\textbf{Betreuer:}`

---

## Schritt 6 — PDFs kompilieren

Führe für beide `.tex`-Dateien aus (Arbeitsverzeichnis: Repo-Root):
```
pdflatex -interaction=nonstopmode -output-directory=<repo> <repo>\<dateiname>.tex
```

Prüfe, ob die PDFs erstellt wurden. Verschiebe sie nach `build/` und lösche die Hilfsdateien (`.aux`, `.log`, `.out`).

---

## Schritt 7 — index.qmd aktualisieren

Füge am Ende der Tabelle eine neue Zeile ein:
```
| <Titel DE kurz> | Prof. Dr. Christian Pfitzner | [PDF](build/<latex_dateiname>_en.pdf) |
```

---

## Schritt 8 — index.html aktualisieren

Füge direkt vor `</tbody>` eine neue Tabellenzeile ein (odd/even abwechselnd zum letzten Eintrag):
```html
<tr class="odd|even">
<td><Titel DE kurz></td>
<td>Prof.&nbsp;Dr.&nbsp;Christian Pfitzner</td>
<td><a href="build/<latex_dateiname>_en.pdf">PDF</a></td>
</tr>
```

---

## Schritt 9 — Commit in projekt_und_abschlussarbeiten

```
git add <latex_dateiname>.tex <latex_dateiname>_en.tex build/<latex_dateiname>.pdf build/<latex_dateiname>_en.pdf index.qmd index.html
git commit -m "Neue Ausschreibung: <Titel DE>"
git push origin master
```

---

## Abschluss

Berichte kurz: Slug, erzeugte Dateien, ob beide Pushes erfolgreich waren.
