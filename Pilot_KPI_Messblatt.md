# Pilot-KPI-Messblatt — FoodAllo ENV (Übung / Real-Light)

**Status:** Konzept · Messdefinitionen für 8–12-Wochen-Pilot · Stand 4.9.2026 Abend  
**Bezug:** `Pilot_Steckbrief_1_Region.md` §6 · `Allokationsregeln_v1.md` · `Lagebild_Anschlussmatrix.md` (Aggregate)  
**Rahmen:** Free only · lokal · kein Mail · keine erfundenen Ist-Werte — Formeln + Zählregeln für eine **Übung** oder begrenzten Real-Light-Lauf  
**Grain:** Haushalt (HH) · Periode = vereinbarte Woche / Übungsintervall · Region = Pilotgebiet

---

## 0) Wie dieses Blatt nutzen

1. Vor Start: Kohorte N_berechtigt festlegen (Einladung Kommune/Sozialträger).  
2. Pro Periode: Rohzähler in Spalte „Übung: Zählregel“ erfassen (Papier oder Sheet).  
3. KPI = Formel unten; Zielrichtung aus Steckbrief, **keine** Fake-Benchmarks.  
4. Aggregate für hypothetischen Lagebild-Anschluss: nur anonymisierte Quoten (vgl. Matrix H3–H9) — **keine** Rohpersonenlisten.

---

## 1) Fairness

| Element | Definition |
|---------|------------|
| **Was** | Ungleichheit der Zuteilung vs. Pro-Kopf-/HH-Baseline; Caps greifen gegen Hamstern |
| **Zähler roh** | Je HH und Position `i`: `granted_h,i`, `baseline_h,i`, `requested_h,i` |
| **Kennzahl A — Baseline-Erfüllung** | `F_fill = mean_h ( granted_h / baseline_h )` über Staples mit `baseline>0` (geclippt auf [0,1] je Position, dann Mittel) |
| **Kennzahl B — Über-Baseline-Quote** | `F_over = (# HH-Positionen mit granted > baseline) / (# HH-Positionen mit Anfrage)` → Ziel **0** (Invariante Need-not-influence) |
| **Kennzahl C — Caps-Wirkung** | `F_cap = (# Anfragen mit requested > baseline und granted ≤ baseline) / (# Anfragen mit requested > baseline)` → Ziel nahe **1** |
| **Kennzahl D — Varianz (optional)** | Varianz von `granted_h / baseline_h` über HH derselben Prioritätsklasse (T2) — sinkend = gleicher |
| **Übung: Zählregel** | Pro Periode Tabelle: HH \| Item \| requested \| baseline \| granted. Manuell oder aus Demo-Log. First-come-Kontrastlauf **nicht** in Fairness-KPI mischen (nur Kontrollarm). |
| **Richtung** | Niedrigere Ungleichheit in T2; Caps greifen; keine Belohnung hoher Anfragen |

**Demo-Referenz (QA):** B Mehl 25→4,0 (Cap) zählt als Caps-Treffer; A und B nahe Baseline bei Staples.

---

## 2) Wartezeit

| Element | Definition |
|---------|------------|
| **Was** | Zeit bis erfolgreiche Abgabe bzw. bis Registrierung am Schalter |
| **Messpunkte** | T_reg = Ankunft Registrierung → Token ausgegeben; T_abgabe = Ankunft LEH/Schalter-Ausgabe → Abgabe bestätigt |
| **Kennzahlen** | Median und P90 von T_reg und T_abgabe (Minuten), getrennt **digital** vs. **analog** |
| **Übung: Zählregel** | Stempeluhr oder Übungsbogen: Start/Ende je Vorgang. Stichprobe mind. 30 Vorgänge/Kanal/Woche oder alle, wenn Kohorte klein. |
| **Ausreißer** | Vorgänge mit Systemausfall / bewusstem Offline-Drill separat kennzeichnen, nicht in P90 der Normalphase |
| **Richtung** | Sinkend nach Startphase; Analog darf nicht systematisch „unzumutbar“ länger sein als digital *wegen Kanal* (gleiche Regel) |

---

## 3) Ausschlussquote (bes. Analog / 65+)

| Element | Definition |
|---------|------------|
| **Was** | Anteil berechtigter HH ohne erfolgreichen Zugang in der Periode |
| **Nenner** | `N_berechtigt` = eingeladene / als berechtigt geführte HH der Kohorte |
| **Zähler Ausschluss** | HH mit `granted_sum = 0` **und** keinem erfolgreichen Kanalversuch **oder** abgewiesen ohne Ersatzkanal |
| **Kennzahl** | `A = N_ausgeschlossen / N_berechtigt` |
| **Teilquote Analog** | Untergruppe `no_digital` bzw. 65+: `A_analog` gleich definiert |
| **Übung: Zählregel** | Jeder HH: mind. ein dokumentierter Versuch (App/Web/Schalter/Proxy/Papier). Erfolg = Token + mind. eine Abgabe oder bestätigter Kontingentabruf. Verweigerung mit Ersatzkanal ≠ Ausschluss. |
| **Richtung** | Nahe **0**; Multi-Kanal nachweisbar (mind. ein Nicht-App-Pfad genutzt und erfolgreich) |

---

## 4) Doppelregistrierung / Missbrauch

| Element | Definition |
|---------|------------|
| **Was** | Erkannte Dubletten und ungültige Codes |
| **Zähler** | `D_dup` = HH-IDs/Tokens die derselben natürlichen Person/Adresse doppelt zugeordnet wurden (manuelle Prüfung); `D_invalid` = Papiercodes/Tokens abgelehnt (TTL abgelaufen, schon verwendet, gefälscht) |
| **Kennzahlen** | `Dup_rate = D_dup / N_karten`; `Invalid_rate = D_invalid / N_validierungsversuche` |
| **Übung: Zählregel** | Audit-Liste: Kartenausgabe; bei Verdacht Abgleich Name/Adresse nur bei Identitätsstelle (nicht im Allokationskern speichern). Proxy = **dieselbe** Karte → zählt nicht als Duplikat. |
| **Richtung** | Kontrolliert niedrig; jeder Treffer mit Audit-Trail; keine automatische Strafe ohne Review |

---

## 5) Bestandsabgleich

| Element | Definition |
|---------|------------|
| **Was** | Anteil Zuteilungen mit Lagerbezug vs. Blindvergabe |
| **Zähler** | `Z_coupled` = Abgaben mit `stock_before` bekannt und `stock_after = stock_before − granted`; `Z_blind` = Abgabe ohne Bestandsbezug |
| **Kennzahl** | `B = Z_coupled / (Z_coupled + Z_blind)` |
| **Übung: Zählregel** | Pro Position Periodenstart-Bestand notieren (LEH/Lager-Übungswert). Jede Fair-Zuteilung dekrementiert. Drill „Blindvergabe“ nur als Negativkontrolle. |
| **Richtung** | **Hoch** (nahe 1 im Fair-Betrieb) |

---

## 6) Akzeptanz

| Element | Definition |
|---------|------------|
| **Was** | Wahrgenommene Fairness vs. Chaos bei Nutzer:innen und LEH-/Schalter-Personal |
| **Instrument** | Kurzer Bogen (3–5 Items), Likert 1–5, Ende Woche 2 / 6 / 12 |
| **Kernitems (Vorschlag)** | (1) „Zuteilung wirkte gerecht“ (2) „Regeln waren verständlich“ (3) „Zugang war möglich ohne Smartphone“ (4 Personal: „Caps waren an der Kasse handhabbar“) |
| **Kennzahl** | Anteil Zustimmungen (≥4) je Item; Freitext-Themen zählen (Hamstern, Wartezeit, Analog) |
| **Übung: Zählregel** | Anonym; n ≥ 20 Nutzer + n ≥ 5 Personal wenn Kohorte es hergibt; sonst qualitative Auswertung kennzeichnen |
| **Richtung** | Fairness sichtbar > Chaos-Wahrnehmung; kein Fake-NPS |

---

## 7) Datenschutz-Incidents

| Element | Definition |
|---------|------------|
| **Was** | Meldepflichtige oder übungsrelevante Vorfälle |
| **Zähler** | Unbefugter Zugriff · Fehlversand Personenliste · Lagerung von Warenkörben entgegen Konzept · Klartext-IDs im Lagebild-Export |
| **Kennzahl** | `I = Anzahl Incidents im Pilot` |
| **Übung: Zählregel** | Jeder Vorfall: Datum, Schicht (Identität/Allokation/LEH), Schwere, Maßnahme. Near-miss separat. |
| **Richtung** | **0** meldepflichtig; Near-miss dokumentieren und Regeln nachschärfen |

---

## 8) Perioden-Erfassungsblatt (Kopiervorlage)

| Periode | N_berechtigt | N_mit_Abgabe | A Ausschluss | Median T_abgabe dig. | Median T_abgabe analog | F_cap | B Bestand | D_dup | I | Notiz |
|---------|--------------|--------------|--------------|----------------------|------------------------|-------|-----------|-------|---|-------|
| W1 | | | | | | | | | | |
| W2 | | | | | | | | | | |
| … | | | | | | | | | | |

Optional Zusatzzeile: Kanalanteile App / Schalter / Proxy / Papier (→ Matrix H7).

---

## 9) Was *nicht* gemessen wird (v1)

- Bundesweite Repräsentativität  
- „Erfolg“ als PR-Metrik oder Follower  
- Medizinische Outcomes  
- Einkommen / Parteinähe / Loyalty  
- Produktiv-API-Latenz BLE (kein Claim)

---

## 10) Exit-Bezug (Steckbrief §8)

KPI-Paket fließt in Pilotbericht → Entscheidung (a) Lagebild-Schnitt prüfen (b) zweites Land (c) Stopp.  
Messblatt allein erzeugt **keinen** Behördenkontakt und **kein** Mail.

---

*FoodAllo — Need, not influence. Messkonzept für Übung, keine Beauftragung.*
