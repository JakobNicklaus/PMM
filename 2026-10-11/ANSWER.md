# Antwort: Was lässt sich mit R effizienter lösen als mit Taschenrechner und Papier?

**Kurzfassung:** R/RStudio ist überall dort klar überlegen, wo **viele Werte
verarbeitet**, **Tabellen nachgeschlagen** oder **Grafiken erstellt** werden.
Taschenrechner und Papier bleiben sinnvoll beim **Verstehen** der Formeln und in
der **Klausur ohne Rechner**.

Der Statistik-Stoff der 3. Klasse (JG3, KM5+KM6) lässt sich in sechs Bereiche
aufteilen:

---

## 1. Deskriptive Kennzahlen (Mittelwert, Median, Standardabweichung, …)

| Kennzahl | R-Befehl | Vorteil |
|----------|----------|---------|
| Arithmetisches Mittel | `mean(x)` | kein manuelles Summieren |
| Median | `median(x)` | sofort, ohne Sortieren von Hand |
| Standardabweichung / Varianz | `sd(x)`, `var(x)` | keine Abweichungsquadrate von Hand |
| Quantile | `quantile(x, c(0.25, 0.5, 0.75))` | beliebige Perzentile |
| Spannweite / IQR | `range(x)`, `IQR(x)` | – |
| Alles auf einmal | `summary(x)` | Min, Q1, Median, Mittel, Q3, Max in einer Zeile |
| Gruppierte Kennzahlen | `tapply(x, g, mean)` | mehrere Gruppen gleichzeitig |

**Warum R besser ist:** kein Rundungsfehler, beliebig große Datensätze, mehrere
Gruppen gleichzeitig, reproduzierbar per Skript.
**Papier/TR besser:** einmalige Mini-Datensätze (z. B. 5 Werte) und zum
Nachvollziehen der Formel.

---

## 2. Boxplot

- R: `boxplot(x)` bzw. `ggplot2::geom_boxplot()`

**Warum R besser ist:** Quartile, Median, Whisker und **Ausreißer** werden
automatisch berechnet und gezeichnet – von Hand sehr aufwendig. Der Vergleich
**mehrerer Gruppen** in einem Bild (`boxplot(wert ~ gruppe, data = df)`) ist per
Hand praktisch nicht machbar.
**Papier/TR besser:** das manuelle Zeichnen aus der 5-Zahlen-Zusammenfassung
schult das Verständnis – in der Klausur oft verlangt.

---

## 3. Diagramme (Histogramm, Kreisdiagramm, Balken-/Stabdiagramm)

- R: `hist()`, `pie()`, `barplot()`, `ggplot2`

**Warum R besser ist:** sofortige Darstellung, automatische Klasseneinteilung
beim Histogramm, beliebig viele Kategorien, Farben/Beschriftung anpassbar und
exportierbar.
**Papier/TR besser:** eine grobe Skizze, wenn in der Klausur gefordert.
**Hinweis:** Kreisdiagramme werden bei vielen Kategorien auch in R schnell
unübersichtlich – R ist hier nur schneller, nicht immer „besser".

---

## 4. Binomialverteilung

| Zweck | R-Befehl |
|-------|----------|
| P(X = k) | `dbinom(k, n, p)` |
| P(X ≤ k) | `pbinom(k, n, p)` |
| Quantil | `qbinom(alpha, n, p)` |
| Zufallszahlen | `rbinom(m, n, p)` |

**Warum R besser ist:** kumulierte Wahrscheinlichkeiten **ohne Tabellenwerk** –
bei großem `n` ein enormer Zeitgewinn. Beliebige `n` und `p` (Tabellen enthalten
nur ausgewählte Werte) und schnelles Summieren von Bereichen, z. B.
`sum(dbinom(3:7, 20, 0.4))`.
**Papier/TR besser:** kleine `n` mit Binomialkoeffizienten, um die Formel zu üben.

---

## 5. Normalverteilung (Dichte- und Verteilungsfunktion)

| Zweck | R-Befehl |
|-------|----------|
| Dichte φ(x) | `dnorm(x, mean, sd)` |
| Verteilungsfunktion P(X ≤ x) | `pnorm(x, mean, sd)` |
| Quantil / z-Wert | `qnorm(p, mean, sd)` bzw. `qnorm(p)` |
| Zufallszahlen | `rnorm(m, mean, sd)` |
| Kurve plotten | `curve(dnorm(x), ...)`, `curve(pnorm(x), ...)` |

**Warum R besser ist:** **kein Tabellen-Nachschlagen und Interpolieren** mehr –
der größte Zeitfresser bei der Arbeit von Hand. Beliebige μ und σ ohne vorheriges
Standardisieren, und Dichte- bzw. Verteilungsfunktion lassen sich sauber plotten.
**Papier/TR besser:** das Standardisieren (z = (x − μ)/σ) + Φ-Tabelle üben, um
das Konzept zu verstehen.

---

## 6. t-Verteilung

| Zweck | R-Befehl |
|-------|----------|
| Dichte | `dt(x, df)` |
| P(T ≤ t) | `pt(t, df)` |
| Kritischer Wert / Quantil | `qt(1 - alpha/2, df)` |
| Zufallszahlen | `rt(m, df)` |

**Warum R besser ist:** kritische Werte direkt statt t-Tabelle mit
Freiheitsgraden – auch bei „krummen" df (z. B. 17) – und p-Werte sofort.
**Papier/TR besser:** kleine df mit vorliegender Tabelle; zum Verständnis, warum
die t-Verteilung bei großem df gegen die Normalverteilung strebt.

---

## Faustregel

**In R/RStudio besser, schneller oder erleichtert:**

- ✅ kumulierte Wahrscheinlichkeiten und Integrale (`pbinom`, `pnorm`, `pt`) – ersetzt Tabellen
- ✅ Quantile / kritische Werte (`qbinom`, `qnorm`, `qt`) – ersetzt Tabellen
- ✅ große Datensätze und gruppierte Auswertungen
- ✅ Grafiken (Boxplot, Histogramm, …) automatisch
- ✅ Wiederholung und Vergleich vieler Szenarien (verschiedene n, p, μ, σ)
- ✅ Reproduzierbarkeit durch ein Skript statt handschriftlicher Rechnung

**Taschenrechner/Papier besser:**

- 📝 Klausuren ohne Computer
- 📝 Verständnis der Formeln (einmal von Hand gerechnet)
- 📝 sehr kleine Datensätze / schnelle Überschlagsrechnung
- 📝 wenn eine Skizze verlangt ist

> **Merksatz:** Rechnen und Zeichnen → R. Verstehen und Skizzieren → Papier.
