# Allokationsregeln v1 — FoodAllo (Diskussionsstand)

**Status:** Konzept / v1 — konkret genug für Entwickler:in und Behörden-Fachgespräch  
**Stand:** 4. September 2026 · projekt-first · keine Beauftragung  
**Abgeleitet aus:** `landing-mock/demo.html` · `Spec_Landing_Hero_GastDemo.md` · `Pilot_Steckbrief_1_Region.md` · `github-concept/README.md` · `Datenschutz_Konzeptskizze_ENV.md`  
**Geltung:** Illustrative Pilotskizze und Regelkern. Zahlen in der Demo sind **Szenario**, keine gesetzlichen Caps.

---

## 0) Zweck und Geltungsbereich

FoodAllo formalisiert die operative Schicht **wer / was / wann gegen Bestand**.  
Anknüpfung DE-ENV: ESVG § 11 Abs. 2 (geordnete Abgabe, Mengenbegrenzung je Verbraucher) — als *fachlicher* Hook, nicht als behauptete Rechtsverordnung.

**v1 gilt für:** eine Allokationsperiode (in der Demo: eine „knappe Woche“); Food + ausgewählte Essentials (Nonfood).  
**v1 gilt nicht für:** bundesweite Produktivsoftware; Konfliktzonen-Operation.

---

## 1) Inputs

### 1.1 Bedarf (Need)

Haushalt erklärt Bedarf **pro Position** für die Periode.

| Feld | Typ | Quelle in v1 |
|------|-----|----------------|
| `requested[item]` | Menge + Einheit | Demo: fest verdrahtete Anfragen; Produktiv: Meldung App/Web/Schalter |
| Katalog-Positionen | geschlossen | Spec/Demo: `wheat_flour`, `rice`, `oil`, `water`, `hygiene`, `formula`, `diapers` |

Bedarf ist **Anspruchsantrag**, nicht Zuteilung. Hamster-Anfragen (z. B. 25 kg Mehl bei Baseline 4,0 kg) sind zulässig als Input und werden durch Caps gebrochen.

### 1.2 Haushalt

| Feld | Demo-Ist | v1-Regel |
|------|----------|----------|
| Haushalts-ID | A / B (fiktiv) | eine Berechtigungskarte je Haushalt und Periode (Pilot §KPI; Landing-Verbesserung „1 Karte/Woche“) |
| Zusammensetzung | A: 2 Erw. + 1 Säugling; B: 2 Erw. | Altersgruppen: infant / child / adult / elderly (Catalog-Baselines laut Spec; Demo aggregiert bereits zu Haushalts-Baseline) |
| Kanal | Gast-Demo ohne Auth | App, Web, Schalter, Proxy, Papiercode (Pilot §5) — gleiche Regeln unabhängig vom Kanal |

### 1.3 Vulnerable-Flags

Sparsam, zweckgebunden (`Datenschutz_Konzeptskizze_ENV.md` §4).

| Flag | Wirkung in v1 | Demo |
|------|----------------|------|
| `infant` (Säugling im Haushalt) | Priorität auf Infant-Items `formula`, `diapers`; Staples nicht automatisch höher als Baseline | Haushalt A |
| `child` | Vulnerable-first bei Enge (Spec/README) | nicht in 2-HH-Demo instanziert |
| `elderly` | Vulnerable-first bei Enge | nicht in Demo instanziert |
| `immobile` / Proxy | Zugangsweg, nicht Extra-Kontingent | Pilot: Proxy-Berechtigung |
| `displaced` / neu zugezogen | erweiterbare Ansprüche nur mit Rechtsgrundlage (Pilot + Datenschutz Krisenmodus) | nicht in Demo |
| `no_digital` | Analog-Pfad Pflicht, kein Mengenbonus | Pilot Multi-Kanal |

**Nicht als Flag missbrauchen:** Einkommen, Parteinähe, „wer zuerst kommt“, LEH-Loyalty-Status.

### 1.4 Bestand (Stock)

| Feld | Demo-Start „knappe Woche“ | Regel |
|------|---------------------------|--------|
| `stock[item]` | Mehl 18 kg · Reis 8 kg · Öl 5 L · Wasser 400 L · Hygiene 6 kits · Formula 6 tins · Windeln 4 packs | Zuteilung **nur** gegen aktuellen Restbestand |
| Meldequelle (ENV-Ziel) | fest im Client | LEH / Lager / ggf. §-11-Meldepflichten — in v1 als Input angenommen, nicht spezifiziert als Schnittstelle |

Kein Blindvergabe-Modus in „Need, not influence“. Pilot-KPI: Anteil Zuteilungen mit Bestandsbezug vs. Blindvergabe → hoch.

---

## 2) Priority tiers

Bei **Enge** (Restbestand reicht nicht für alle Baseline-Anfragen der Periode):

| Tier | Wer | Welche Positionen | Reihenfolge |
|------|-----|-------------------|-------------|
| **T0** | Haushalte mit Infant-Flag | `formula`, `diapers` (und analoge Infant-Essentials) | **vor** Staples; in der Demo: A vor B, B hat keine Infant-Items |
| **T1** | Vulnerable (infant / child / elderly; medizinisch nur soweit rechtlich abgesichert) | knappe Staples und Essentials | Spec: „zuerst Säuglinge, Kinder, Ältere“ |
| **T2** | Alle berechtigten Haushalte | Staples (`wheat_flour`, `rice`, `oil`, `water`, `hygiene`) | proportional zur **Baseline** (nicht zur Anfrage), nie über Cap |
| **T3** | Rest / nicht priorisiert | nur wenn nach T0–T2 Bestand übrig | in Demo nicht genutzt |

**Demo-Vereinfachung (explizit):** Staples werden im Fair-Modus „A dann B“ gegen Rest abgearbeitet, nachdem Infant-Items für A bedient sind. Spec fordert parallel nach Baseline-Anteil; v1-Soll für Code/Pilot:

```
share_h(item) = baseline_h(item) / sum_h baseline_h(item)
granted_h     = min(requested_h, baseline_h, share_h * remaining_after_T0)
```

First-come ist **Kontrastmodus**, kein Betriebsmodus (siehe Non-Goals).

---

## 3) Caps (per capita / household)

### 3.1 Perioden-Baseline (Cap)

`granted[item] ≤ min(requested[item], baseline_household[item], remaining_stock[item])`

**Demo-Baselines (QA-Referenz Spec 2.4 / demo.html):**

| Position | HH A (2 Erw. + Säugling) | HH B (2 Erw.) |
|----------|--------------------------|---------------|
| Weizenmehl | 4,2 kg | 4,0 kg |
| Reis | 2,5 kg | 2,4 kg |
| Speiseöl | 0,7 L | 0,7 L |
| Trinkwasser | 56 L | 42 L |
| Hygienepaket | 1 kit | 1 kit |
| Säuglingsnahrung | 4 tins | — |
| Windeln | 2 packs | — |

Pro-Kopf-Logik (Catalog, Spec): Baseline summiert sich aus Altersgruppen infant/child/adult/elderly. v1 behandelt die Haushalts-Baseline als **verbindlichen Perioden-Cap**. Zusätzlicher Hamster-Puffer existiert nicht.

### 3.2 Haushaltskarte

- **Eine Karte / ein Token je Haushalt und Periode** (Woche in der Demo).
- Doppelregistrierung = Missbrauchspfad (Pilot-KPI Dubletten + Audit-Trail).
- Proxy nutzt **dieselbe** Karte, erzeugt keine zweite.

### 3.3 Cap am Restbestand

Kein Haushalt darf mehr erhalten als sein Baseline-Cap **und** nicht mehr als der nach Tiers verfügbare Rest.  
QA Fair-Modus Mehl: B fragt 25 kg an → zugeteilt **4,0 kg** (Cap), Lager danach 18 − 4,2 − 4,0 = **9,8 kg**.  
QA First-come: B erhält min(25, 18) = **18 kg** → Lager 0; A Mehl **0**.

---

## 4) Stock coupling

1. Jede Zuteilung dekrementiert `stock[item]` atomar in der Periode.  
2. `granted = 0`, wenn `stock = 0` — keine Negativbestände, keine Reservierungsfiktion ohne Bestand.  
3. Offline-Kasse (Pilot): Validierungstoken mit **kurzer TTL**; keine Vollreplikation des Lagers auf jedes Gerät (`Datenschutz_Konzeptskizze_ENV.md` §8).  
4. Lagebild (Ziel, nicht v1-Schnittstelle): aggregierte Kennzahlen (Bestand, Zuteilungsquote, Caps-Verstöße) ohne Rohpersonenlisten.

**Demo-Ist vs. Soll:** Client-only, kein Persistenz-Backend, Reset setzt `STOCK0` zurück. Für Pilot: Bestandsquelle LEH/Lager, Abgleich Pflicht.

---

## 5) Analog- und Proxy-Pfade

Gleiche Allokationsregeln, anderer Kanal. Kein digitaler Vorteil.

| Pfad | Wer | Token | Datenminimum |
|------|-----|-------|----------------|
| App / Web | Haushalt selbst | digitale Karte | Berechtigungs-ID, HH-Größe, Kontingent |
| Schalter (Kommune, Sozialträger, LEH-Service) | analog | gleiche ID oder Papiercode | Pilot §5 |
| Proxy (Angehörige / Pflege) | immobile / Säuglingshaushalte | dokumentierte Vertretung, widerrufbar | Datenschutz §5 |
| Papier-Notfallcode | kein Smartphone / kein Netz | Einmalnutzung, kurze TTL | Datenschutz §6 |
| Offline-Kassenvalidierung | LEH-Abgabe | Restkontingent-Token, kein Warenkorb-Dauerlog | Datenschutz §3 LEH-Rolle |

**Invariante:** Analog darf Baseline nicht unterschreiten *weil analog* — Ausschlussquote (bes. 65+) ist Pilot-KPI „nahe 0“.

---

## 6) Fairness-Invarianten — Need, not influence

Muss in jedem Betriebsmodus (außer dem Demo-Kontrast „First-come“) gelten:

1. **Need not influence:** Anfragehöhe über Baseline erhöht die Zuteilung nicht.  
2. **Gleiche Regel, gleicher Cap** unabhängig von Kanal, Ankunftszeit (im Fair-Modus) und sozialem Einfluss.  
3. **Vulnerable-first bei Enge**, nicht Privilegienlogik (Pilot §4).  
4. **Bestand koppelt Zuteilung** — Fairness ohne Lager ist unvollständig.  
5. **Transparenz:** angefragt / zugeteilt / Lager danach sind erklärbar (Demo-UI).  
6. **Zweckbindung:** Speicherung Anspruch + Kontingent, keine dauerhaften Warenkörbe, keine Konsumprofile.  
7. **Eine Periode, eine Karte.**

Verletzung in der Demo absichtlich nur im Toggle „Wer zuerst kommt“ — als Gegenbild, nicht als Option für den Pilotbetrieb.

---

## 7) Explizite Non-Goals

- Kein First-come-first-served als Betriebsregel.  
- Kein Ersatz für Eigenvorsorge, BLE-Reserven oder Behörden.  
- Keine operative Rolle in humanitären Konfliktzonen; keine NGO-/WFP-Substitution.  
- Keine Mengenboni für digitale Nutzer, Loyalty oder „wer laut ist“.  
- Kein Scoring / Marketing / Friedensmodus-Profiling.  
- Keine bundesweite Produktivsoftware in v1; kein Vendor-Lock-in.  
- Keine Behauptung gesetzlicher Caps — Demo-Zahlen sind Szenario.  
- Kein Mail-CTA, kein Klarname in Regeln/UI.  
- Keine Gesundheitsfeindaten als Default-Flag (nur soweit rechtlich abgesichert).

---

## 8) Referenzrechnung (QA, Spec 2.4)

**Need, not influence**

| Position | A angefragt | A zugeteilt | B angefragt | B zugeteilt | Lager danach |
|----------|-------------|-------------|-------------|-------------|--------------|
| wheat_flour | 4,2 | 4,2 | 25 | **4,0** (Cap) | **9,8** |
| formula | 4 | **4** | — | — | 2 |
| diapers | 2 | **2** | — | — | 2 |
| rice | 2,5 | 2,5 | 2,4 | 2,4 | **3,1** |

**Wer zuerst kommt:** B-Mehl 18, Lager Mehl 0, A-Mehl 0; Formula kann bei A bleiben, Staples leer/knapp.

Implementierung: `landing-mock/demo.html` Funktion `allocate()`.

---

## 9) Offene Punkte (v1 → Pilot)

1. Exakte Pro-Kopf-Baselines je Altersgruppe aus App-Catalog in eine öffentliche Tafel überführen (Landing-Schritt 3).  
2. Proportionale Staples-Teilung statt Demo-Reihenfolge A-dann-B.  
3. Zeitraum der Periode (Kalenderwoche vs. Übungsintervall) mit Behörden.  
4. Infant-Items: Härtefall, wenn Bestand < Summe T0-Baselines (Rationierungsschlüssel).  
5. LEH-Bestandsmeldung: Felder für spätere Lagebild-Matrix (Hypothese, Evidenz Proof-Action 2).

*Ende Allokationsregeln v1. FoodAllo — Need, not influence.*
