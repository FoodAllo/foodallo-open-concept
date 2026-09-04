# Öffentliche Regeltafel — FoodAllo (eine Seite)

**Projekt-first · Deutsch · Gemeinwohl · Stand 4.9.2026**  
**Status:** Diskussionsstand / Pilotskizze — **keine** Beauftragung, **keine** gesetzlichen Caps  
**Ableitung:** `Allokationsregeln_v1.md` · Gast-Demo `landing-mock/demo.html` · Spec Hero+Gast-Demo  
**Pause:** kein Mail, kein Klarname, keine neuen öffentlichen Posts ohne Desk

---

## Wofür diese Tafel ist

Staatliche Reserven und ESVG beantworten, *dass* und *wo* Vorräte existieren.  
FoodAllo skizziert die fehlende Schicht: **wer was wann** erhält — prüfbar, nach Bedarf, nicht nach Ellenbogen.

**Fachlicher Hook (kein Rechtsanspruch):** ESVG § 11 Abs. 2 — geordnete Abgabe, Mengenbegrenzung je Verbraucher. AMK TOP 22 (20.3.2026): §-11-Vorsorge + BLE-Lagebild *prüfen*.

---

## Die Regeln (öffentlich, kurz)

| # | Regel | In einem Satz |
|---|--------|----------------|
| 1 | **Bedarf, nicht Einfluss** | Eine höhere Anfrage über der Wochenbaseline erhöht die Zuteilung nicht. |
| 2 | **Pro-Kopf-Baseline** | Wochenanteil nach Alter (Säugling ≠ Erwachsener); Demo-Zahlen = Szenario. |
| 3 | **Vulnerable zuerst bei Enge** | Wenn Lager nicht für alle Baselines reicht: zuerst Säuglinge, Kinder, Ältere — bei Infant-Essentials vor Staples. |
| 4 | **Cap am Restbestand** | Zugeteilt = min(angefragt, Baseline, Restlager). Kein Haushalt über den Cap. |
| 5 | **Eine Karte / Haushalt / Woche** | Ein Token je Periode; Proxy nutzt dieselbe Karte, keine zweite. |
| 6 | **Bestand koppelt Zuteilung** | Keine Blindvergabe ohne Lagerbezug; Restbestand nach jeder Abgabe nachvollziehbar. |
| 7 | **Gleiche Regel, jeder Kanal** | App, Web, Schalter, Proxy, Papiercode — **gleiche Caps**, kein Digitalbonus. |
| 8 | **Zweckbindung** | Anspruch + Kontingent, keine Konsumprofile, keine dauerhaften Warenkörbe. |

**Mini-Formel (zitierbar):**  
`zugeteilt = min(angefragt, Wochen-Baseline, Restlager)` · bei Enge zuerst Säugling / Kind / älter · 1 Karte / Haushalt / Woche

---

## Was die Demo zeigt (Klartext)

| Modus | Mehl-Beispiel |
|-------|----------------|
| **Mit Regeln** | B will 25 kg → bekommt **4 kg** (Wochenanteil). A mit Säugling behält Mehl und Säuglingsnahrung. |
| **Wer zuerst kommt** (Kontrast, kein Betrieb) | B nimmt **18 kg**, Lager leer. A mit Säugling: **0 kg** Mehl. |

---

## Analog / Offline (Pflichttext)

Ohne Smartphone: **Schalter** (Kommune / Sozialträger / LEH) · **Proxy** (Angehörige, widerrufbar) · **Papiercode** · Offline-Abgleich an der Ausgabe.  
Digitale Mehrheit ≠ digitale Pflicht. Ausschluss wegen fehlendem Gerät ist Regelverstoß.

---

## Explizit nicht

- First-come-first-served als Betriebsregel  
- Ersatz für Eigenvorsorge, BLE-Reserven oder Behörden  
- Operative Rolle in Konfliktzonen / Aid-Substitution („FoodAllo ergänzt Aid, ersetzt sie nicht“)  
- Mengenboni für Einfluss, Loyalty oder „wer laut ist“  
- Behörden-Impersonation, Gewinn-/Startup-Framing, Klarname in der Tafel  

---

## Ein-Satz-Position

> Reserven brauchen eine faire Allokationsschicht: Bedarf melden, gerecht zuteilen — digital wo es hilft, analog wo nötig.

Lokaler Mock (kein Deploy): `landing-mock/index.html` · `landing-mock/demo.html`  
Vertiefung: `Allokationsregeln_v1.md`

---

*FoodAllo · Gemeinwohl-Konzept · Leipzig-Pilotskizze · Free only*
