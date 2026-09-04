# Analog-Kanal — Text-Wireframe (Schalter · Proxy · Papiercode · Offline-Kasse)

**Status:** Konzept-Wireframe · **kein Deploy** · Free only · kein Mail · kein Klarname · Publish-Pause  
**Stand:** Freitag, 4. September 2026, Abend (Europe/Berlin) · lokal `/workspace/foodallo/`  
**Bezug:** Pilot §5 · Allokationsregeln v1 §5–6 · Datenschutz-Konzeptskizze §3–6 · Demo-Lückenliste (Offline/Analog)  
**Invariante:** **Need, not influence** — gleiche Caps / gleiche Periode / eine Karte; Analog erzeugt **keinen** Mengenbonus und **keinen** Nachteil.

---

## Ziel des Wireframes

Beschreiben, was eine Person **ohne Smartphone / ohne Netz** (oder mit Proxy) Schritt für Schritt sieht und tut — als nummerierte Screens für Fachgespräch und spätere UI. Kein Prototyp-Code, keine Kassen-Integration.

**Akteure:** Haushalt · Schalter-Personal (Kommune / Sozialträger / LEH-Service) · Proxy · LEH-Kasse (offline-fähig).

---

## Screen-Fluss (nummeriert)

### 0) Einstieg — Kanalwahl (gemeinsam)

```
┌─────────────────────────────────────────────┐
│  FoodAllo — Zugang (Konzept)                │
│  Periode: eine Woche / Übungsintervall      │
│                                             │
│  [1] Schalter (hier vor Ort)                │
│  [2] Proxy (für Angehörige / Pflege)        │
│  [3] Papier-Notfallcode (bereits erhalten)  │
│                                             │
│  Hinweis: Gleiche Regeln wie App/Web.       │
│  Kein Extra-Kontingent. Kein First-come.    │
└─────────────────────────────────────────────┘
```

---

### Pfad A — Schalter

**A1 · Anmeldung / Berechtigung prüfen**
```
┌─────────────────────────────────────────────┐
│  Schalter — Berechtigung                    │
│  Nachweis: behördlicher Übergangsnachweis / │
│  Einladung Pilot-Kohorte (kein eID nötig)   │
│                                             │
│  Haushaltsgröße: [__] Erw. [__] Kind …      │
│  Vulnerable (sparsam): ☐ Säugling ☐ …       │
│                                             │
│  → Erzeugt / lädt **eine** Periodenkarte    │
│  Datenminimum: ID-Token · HH-Faktor · Caps  │
└─────────────────────────────────────────────┘
```

**A2 · Bedarf melden (Antrag, nicht Zuteilung)**
```
┌─────────────────────────────────────────────┐
│  Bedarf melden — Periode aktuell            │
│  Position     Anfrage   Cap (Baseline)      │
│  Mehl         [____]    4,0 kg              │
│  Reis         [____]    …                   │
│  …                                          │
│  Personal erklärt: Anfrage > Cap wird       │
│  auf Cap gekürzt (Need, not influence).     │
│  [Weiter zur Zuteilung gegen Bestand]       │
└─────────────────────────────────────────────┘
```

**A3 · Zuteilung sichtbar machen**
```
┌─────────────────────────────────────────────┐
│  Zuteilung (Fair-Modus)                     │
│  Angefragt · Cap · Zugeteilt · Lager danach │
│  (wie Gast-Demo — erklärbar, kein „Magie“)  │
│                                             │
│  Ausgabe: Papierbeleg + optional Kurzcode   │
│  für Kasse (TTL kurz)                       │
│  [Beleg drucken]  [Proxy verknüpfen]        │
└─────────────────────────────────────────────┘
```

**A4 · Abschluss Schalter**
```
┌─────────────────────────────────────────────┐
│  Erledigt                                   │
│  • Eine Karte / Periode gebucht             │
│  • Beleg: Positionen + Restkontingent       │
│  • Hinweis Abgabe: LEH-Partnerliste         │
│  • Betroffeneninfo (kurz, Papier)           │
└─────────────────────────────────────────────┘
```

---

### Pfad B — Proxy

**B1 · Vertretung dokumentieren**
```
┌─────────────────────────────────────────────┐
│  Proxy — Vertretung                         │
│  Vertretene:r (Haushalt) · Vertretung       │
│  Art: Angehörige / Pflege / Sozialträger    │
│  ☐ Widerrufbar  ☐ Befristet bis [Datum]     │
│  Nutzt **dieselbe** Periodenkarte — keine   │
│  zweite Karte, kein Extra-Kontingent.       │
└─────────────────────────────────────────────┘
```

**B2 · Danach wie A2–A4** (gleiche Caps; Audit: wer gemeldet hat).

---

### Pfad C — Papier-Notfallcode

**C1 · Code einlösen (Schalter oder LEH-Service)**
```
┌─────────────────────────────────────────────┐
│  Papiercode                                 │
│  Code: [####-####-####]  Einmalnutzung      │
│  TTL: kurz (Konzept: Stunden/Tage — mit DS) │
│  Status: ☐ gültig  ☐ verbraucht  ☐ abgelaufen│
│  → bindet an bestehende Periodenkarte oder  │
│    erzeugt Übergangsberechtigung Pilot      │
└─────────────────────────────────────────────┘
```

**C2 · Zuteilung / Beleg** wie A3–A4; Code danach ungültig.

---

### Pfad D — Offline-Kasse (Abgabe)

**D1 · Token prüfen (ohne Voll-Lager-Replikation)**
```
┌─────────────────────────────────────────────┐
│  Kasse — Offline-Validierung                │
│  Scan / Tippen: Kurzcode / Beleg-ID         │
│  Anzeige: Restkontingent je Position        │
│  (kein dauerhafter Warenkorb, kein Profil)  │
│                                             │
│  Netz weg: lokales Validierungstoken, TTL   │
│  Sync später → Aggregate, Rohlog befristen  │
└─────────────────────────────────────────────┘
```

**D2 · Abgabe buchen**
```
┌─────────────────────────────────────────────┐
│  Abgabe                                     │
│  Position   Rest vorher → Abgabe → Rest neu │
│  Caps nicht überschreitbar an der Kasse     │
│  [Bestätigen]  [Ablehnen — Cap/TTL]         │
└─────────────────────────────────────────────┘
```

**D3 · Quittung**
```
┌─────────────────────────────────────────────┐
│  Quittung (Papier)                          │
│  Periode · Positionen · Rest · Kanal=Analog │
│  Keine Marketing-Daten · Zweckbindungshinweis│
└─────────────────────────────────────────────┘
```

---

## Regel-Kopplung (Need, not influence)

| Wireframe-Punkt | Regel (Allokationsregeln v1) |
|-----------------|------------------------------|
| Eine Periodenkarte | §3.2 / Invariante 7 |
| Anfrage > Cap → Cap | §3.1 · Invariante 1 |
| Proxy = dieselbe Karte | §5 · kein Extra-Kontingent |
| Papiercode Einmal + TTL | §5 · Datenschutz §6 |
| Offline nur Rest-Token | §4 Punkt 3 · DS §8 |
| Gleicher Cap App/Analog | §5 Invariante · Pilot KPI Ausschluss ≈ 0 |
| Kein First-come-Betrieb | §7 Non-Goals |

---

## Datenminimum (pro Screen)

- **Schalter:** Berechtigungsnachweis → Token/HH-Faktor/Caps — keine Warenkorb-Historie.  
- **Proxy:** Vertretungsdokument + Widerruf — keine Gesundheitsfeindaten als Default.  
- **Papiercode:** Code-Hash/Status/TTL — Einmal.  
- **Kasse:** Restkontingent-Token — keine zentrale Einkaufsliste.

---

## Nicht-Ziele dieses Wireframes

- Kein Deploy, keine App-UI, keine LEH-POS-Anbindung  
- Keine gesetzlichen Caps behaupten (Demo-Zahlen = Szenario)  
- Kein Klarname, kein Mail-CTA  
- Keine Mengenboni für „wer am Schalter wartet“

**Optionaler Lokal-Stub:** `landing-mock/analog.html` (Plain-DE, Link zurück zu `demo.html`).

*Ende Wireframe. Ablage: `/workspace/foodallo/Analog_Kanal_Wireframe.md`*
