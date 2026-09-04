# Lagebild-Anschlussmatrix — BLE-Aggregate vs. Haushalts-Allokation

**Status:** Konzept / **Hypothese** — kein BLE-Produktivschema, keine Schnittstellen-Spezifikation  
**Stand:** 4. September 2026 (Abend, Europe/Berlin) · lokal · Free only · kein Mail  
**Auftrag:** Evidenzdossier §7 Proof-Action 2 · Fachfrage 4 (`Fachfragen_ENV_Gespraech.md`) · Datenschutz-Rollen (`Datenschutz_Konzeptskizze_ENV.md`)  
**Framing:** BLE-IT-Lagebild = AMK TOP 22 *Prüfauftrag* — FoodAllo beansprucht nicht, dieses System zu ersetzen, sondern anschlussfähig zu diskutieren.

---

## These (eine Zeile)

**Lagebild aggregiert Lage** (Bestände, Unternehmen, Regionen, Quoten). **Allokation entscheidet Haushalt** (wer / was / wann gegen Cap und Bestand). Rohpersonenlisten gehören nicht ins BLE-Lagebild-Default.

---

## Schichtentrennung

| Schicht | Zweck | Grain | Personenbezug |
|---------|-------|-------|----------------|
| **BLE-Lagebild** (Hypothese) | bundeseinheitliche Lage-/Lageberichtsfähigkeit für zuständige Stellen | Region / Unternehmen / Warengruppe / Periode | **aggregiert** — keine Rohpersonenlisten als Default |
| **FoodAllo-Allokation** (Konzept) | geordnete Abgabe, Mengen je Verbraucher (§ 11 Abs. 2 als fachlicher Hook) | Haushalt / Anspruchskarte / Position | Token + Kontingent; sparsame Vulnerable-Flags |
| **LEH / Ausgabe** | physische Abgabe, Offline-Validierung | Kasse / Schalter | Abgabezeitpunkt/-ort grob; kein Warenkorb-Dauerlog |

---

## Matrix — was wohin (Hypothesen)

Alle Zeilen: **H** = Hypothese (Diskussionsstand). Abgleich nur nach Fachgespräch mit BMLEH/BLE/Land.

| # | Kennzahl / Feld | FoodAllo-Allokationsschicht (lokal) | → BLE-Lagebild (aggregiert, Hypothese) | Nicht weitergeben |
|---|-----------------|--------------------------------------|----------------------------------------|-------------------|
| H1 | Lagerbestand je Position | `stock[item]` vor/nach Periode (Demo: Mehl, Reis, Öl, Wasser, Hygiene, Formula, Windeln) | Summe / Füllgrad je Warengruppe und Region; Trend knapper Staples | Einzel-HH-Bestandsbuch |
| H2 | Meldepflicht-Anschluss (§ 11 Abs. 1) | Bestandsinput von LEH/Lager angenommen | Unternehmens-/Standortmeldungen lagebildrelevant (einheitliche Kriterien = AMK-Prüfgegenstand) | — |
| H3 | Zuteilungsquote | `granted / baseline` je Position und Periode | Anteil erfüllter Baselines je Region / Warengruppe | Personenlisten „wer bekam wie viel“ |
| H4 | Caps-Verstöße / Cap-Wirkung | Anfrage > Cap (Demo: B 25 kg → 4,0 kg) | Anzahl/Quote der Deckelungen je Region (Anonym) | Identität der anfragenden HH |
| H5 | Vulnerable-first bei Enge | T0 Infant-Items (`formula`, `diapers`); T1 Kind/Ältere | Quote bedienter Infant-/Vulnerable-Baselines vs. Staples | medizinische Rohdaten, Diagnose-Flags |
| H6 | Ausschlussquote Analog/65+ | Pilot-KPI: Zugang ohne Smartphone | Anteil Abgaben über Schalter/Proxy/Papier vs. App (aggregiert) | Namen, Adressen |
| H7 | Kanalmix | App / Web / Schalter / Proxy / Papiercode | Kanalanteile je Region (statistisch) | Gerätedaten, Tracking |
| H8 | Eine Karte / HH / Woche | Dubletten-KPI, Audit-Trail lokal | Dublettenrate aggregiert (Missbrauchssignal) | Berechtigungs-IDs roh |
| H9 | Blindvergabe vs. Bestandsbezug | Pilot-KPI: Anteil Zuteilungen mit Stock-Coupling | Quote bestandsgekoppelter Abgaben | — |
| H10 | Offline-TTL / Token | kurze TTL, kein Voll-Lager auf Gerät | Ausfall-/Offline-Rate der Validierung (aggregiert) | Token-Inhalte |
| H11 | Periodenrestlager | `stock after` in Demo | Lage „Restreichweite“ je Staple (Tage/Wochen-Schätzung nur wenn fachlich vereinbart) | HH-Restkontingente namentlich |
| H12 | LEH-Partnerabdeckung | Pilot: 2–3 Formate | Zahl/Format lagebildrelevanter Abgabestellen in der Region | Vertragsdetails personenbezogen |

---

## Was BLE-Lagebild (Hypothese) *nicht* aus der Allokationsschicht braucht

- Klarnamen, Adressen, vollständige Haushaltszusammensetzung als Default  
- dauerhafte Warenkörbe / Konsumprofile  
- Parteinähe, Einkommen, Loyalty  
- Rohpersonenlisten „Vulnerable“ ohne Rechtsgrundlage und Zweckbindung  

(vgl. Datenschutz-Konzeptskizze: Lagebild-Rolle = Kennzahlen, keine Rohpersonenlisten.)

---

## Was die Haushalts-Allokation *zusätzlich* braucht (bleibt lokal zur Ausgabe)

| Bedarf | Warum nicht Lagebild-Default |
|--------|------------------------------|
| Berechtigungs-Token / 1 Karte je HH | operative Abgabe, nicht Bundeslage |
| `requested` vs. `baseline` vs. `granted` je HH | Fairnessprüfung am Schalter |
| Vulnerable-Flag sparsam (infant/child/elderly) | Tiers bei Enge |
| Proxy-/Papier-Nachweis | Zugang, kein Extra-Kontingent |
| kurzer Audit-Trail | Missbrauch lokal, dann aggregieren |

---

## Anschluss an Fachfrage 4

> Welche **aggregierten** Kennzahlen aus einer Allokationsschicht wären für das geprüfte IT-Lagebild relevant — und welche personenbezogenen Rohdaten bleiben bewusst draußen?

**Antwortskizze (Konzept):** relevant = H1, H3–H6, H8–H9, H11–H12 als Aggregate. Draußen = Roh-IDs, Klarnamen, Warenkörbe, medizinische Details. Schnitt = erst nach Rechtsgrundlage + Verantwortlichenklärung (Fachfrage 1) und Pilotstufe (Fachfrage 2).

---

## Offene Punkte (kein Claim)

1. Einheitliche BLE-Kriterien für „lagebildrelevante Ernährungsunternehmen“ sind AMK-Prüfauftrag — hier nicht spezifiziert.  
2. Rechtsgrundlage Vorsorge vs. Krise und gemeinsame Verantwortung mit LEH: Fachgespräch.  
3. Keine API-, Schema- oder Produktivbehauptung.  
4. Abgleich der Matrix nur nach Desk-Freigabe und Fachgespräch — **kein Mail**.

---

*FoodAllo — Reserven brauchen eine faire Allokationsschicht. Hypothesenmatrix, keine Beauftragung.*
