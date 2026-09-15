# FoodAllo Landing / Demo (lokal)

**Übung / Konzept-Demo · Free only · kein Deploy · kein Klarname · kein Mail · Gemeinwohl**  
**PDF-Linie:** `Strukturkonzept_ENV_2026.pdf` · Region nicht festgelegt

## Sprachen (UI)

| Code | Sprache | Status |
|------|---------|--------|
| DE | Deutsch (Default) | voll (Hero, Demo, Analog) |
| EN | English | voll |
| FR | Français | voll (Hero, Demo, Analog); Index unterhalb Hero → EN-Fallback |
| ES | Español | voll (Hero, Demo, Analog); Index unterhalb Hero → EN-Fallback |
| UK | Українська | voll (Hero, Demo, Analog); Index unterhalb Hero → EN-Fallback |

Eine Sprache gleichzeitig (`data-lang` + Header-Buttons). Optional: `?lang=fr`.

## Öffnen
```bash
cd /workspace/foodallo/landing-mock
python3 -m http.server 8765
```
Dann: http://127.0.0.1:8765/

Schock-Preset: http://127.0.0.1:8765/demo.html?preset=markt  
(auch `#markt`; Default ohne Param: Knappe Woche)

## Dateien
| Datei | Inhalt |
|-------|--------|
| `index.html` | Klartext-Hero · 3 Schritte · CTA `demo.html?preset=markt` · DE–UK |
| `demo.html` | Presets Knappe Woche / Markt gestört · Nach Bedarf vs Wer zuerst kommt · Höchstanteil · Analog · `#esvg11` `#analog-line` `#regeln` `#aid-satz` |
| `analog.html` | Schalter / Nachbar / Papiercode |
| `eliminationsmaschine.html` | Premissen P1–P7 (DE/EN wie bisher) |

## Walkthrough
- `../Crash_Ready_R4_Walkthrough_15min.md` — Sprecher-Skript 15 Min  
- `../Fachgespraech_Demo_Walkthrough.md` — Fachgespräch  
- `../Demo_Behoerden_Klartext_2026-09-15.md` — Änderungsprotokoll

## Crash-ready (lokal)
1. Hero 30 s → Demo `?preset=markt` → Mode-Toggle → Analog → Aid-Satz  
2. Optional: Eliminationsmaschine  
3. Kein Deploy ohne Desk
