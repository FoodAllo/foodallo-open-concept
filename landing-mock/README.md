# FoodAllo Landing Mock (lokal)

Free-Tier · kein Paid-Hosting · **kein** grok.me-Deploy ohne Desk-Freigabe · kein Klarname · Publish-Pause.

| Datei | Inhalt |
|-------|--------|
| `index.html` | Hero (Reserve ≠ Allokation), §-11-/AMK-Zeile, Analog-Pflichttext, Demo-Teaser, Prinzipien, FAQ-Gegenargumente, Impressum-Platzhalter ohne Klarname, DE/EN-Toggle |
| `demo.html` | Interaktive Gast-Demo: **Need-not-influence** vs **First-come** (Caps, Vulnerable-first, Lagerkopplung) |

## Lokal öffnen (3 Wege)

**1) Doppelklick / Datei-URL (schnellste Prüfung)**  
Datei im Browser öffnen:

- `…/foodallo/landing-mock/index.html`
- `…/foodallo/landing-mock/demo.html`

**2) Mini-HTTP-Server (empfohlen, relative Links sauber)**

```bash
cd /workspace/foodallo/landing-mock
python3 -m http.server 8765
```

Dann im Browser: `http://127.0.0.1:8765/` (Hero) und `http://127.0.0.1:8765/demo.html` (Gast-Demo).

**3) Desk-Review 2-Min-Punchline**  
Hero → Klartext fair vs First-come · §-11-Zeile · Analog · Aid-Satz separat · DE/EN umschalten · Demo: Mehl 25 kg → Cap 4 kg vs First-come leert Lager.

## Nicht tun

- Nicht als Produktiv-Landing verlinken ohne Desk  
- Kein Mail-CTA, kein Klarname ergänzen  
- Live-Site grok.me **nicht** eigenmächtig angleichen

Ableitung: `Spec_Landing_Hero_GastDemo.md` · `Copy_Hero_Reserve_Allokation.md` · `Allokationsregeln_v1.md` · `Regeltafel_oeffentlich.md`
