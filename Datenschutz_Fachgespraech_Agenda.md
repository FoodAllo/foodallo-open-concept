# Datenschutz-Fachgespräch — Kurzagenda (Landesdatenschutz / Behörden-DS)

**Status:** Konzept / Diskussionsunterlage · **kein Mail** · kein Klarname · Free only · Publish-Pause  
**Stand:** Freitag, 4. September 2026, Abend (Europe/Berlin) · lokal `/workspace/foodallo/`  
**Perspektive:** Landesdatenschutzbeauftragte:r / behördliche:r Datenschutz · Anknüpfung ENV (ESVG), **keine** Behörden-Impersonation  
**Unterlage:** `Datenschutz_Konzeptskizze_ENV.md` · `Fachfragen_ENV_Gespraech.md` · `Pilot_Steckbrief_1_Region.md` · `Allokationsregeln_v1.md`  
**Dauer (Vorschlag):** 30–40 Min · Paper only — kein AV, keine DPIA-Festlegung in diesem Termin

---

## Haltung (vor Minute 0)

- FoodAllo = **Gemeinwohl-Konzept**, keine Beauftragung, kein Produktivsystem.  
- Diese Agenda klärt **Fragen**, sie behauptet keine Rechtsgrundlage.  
- AV-Vertrag und DPIA sind **Folgearbeiten** nach Verantwortlichenklärung — hier nur einordnen.  
- Pilot-Scope: DE-ENV / eine Region; internationale Bezüge: **keine**.

---

## Zeitplan (kurz)

| Min | Block | Kernfragen | Artefakt |
|-----|-------|------------|----------|
| **0–5** | Scope & Zweckbindung | Verarbeitung **nur** für Anspruch + Kontingent + aggregiertes Lagebild. Nicht-Zwecke (Marketing, Scoring, Konsumprofile) explizit. Reicht Zweckbindung Art. 5 Abs. 1 lit. b als Diskussionsrahmen? | Konzeptskizze §1–2 · Fachfrage 1 |
| **5–15** | **Identität vs. Allokation** | Rollentrennung: Identitätsstelle hält Wer-/Berechtigung; Allokationskern nur Pseudonym-/Kontingent-IDs; LEH nur Validierungstoken; Lagebild nur Aggregate. Designprinzip akzeptabel? Wo sitzt Verantwortlichkeit Bund/Land/LEH? | Konzeptskizze §3 · Pilot Governance |
| **15–22** | **Speicherbegrenzung** | Vorschlagstabelle Frieden vs. Krise (kurze TTL, Einmal-Papiercodes, Rohlogs → Aggregate). Welche Fristen würden Aufsicht/Behörde als *diskussionsfähig* sehen — ohne Festlegung heute? | Konzeptskizze §6 |
| **22–30** | **Krisen- vs. Friedensmodus** | Frieden/Vorsorge: Übung, Opt-in wo möglich, minimale Daten. Krise: hoheitlich ausgelöst, streng zweckgebunden; Rückkehr = beschleunigte Löschung, keine „Krisendaten auf Vorrat“. Umschaltung dokumentiert? | Konzeptskizze §7 · Fachfrage 1 |
| **30–35** | Analog / Übergang ohne eID | Schalter, Proxy (widerrufbar), Papiercode, Offline-Kasse — gleiche Caps, Datenminimum. Welche Übergangsnachweise Tag 1 akzeptabel (Fachfrage 3)? | Pilot §5 · Allokationsregeln §5 |
| **35–40** | **AV / DPIA = später** | Heute: Konzeptcheckliste. AVV (Art. 28) mit LEH/IT erst nach Rollenklärung. DPIA-Pflicht und Timing offen (Konzeptskizze Offene Punkte 1–7). Exit: wer prüft was — **kein** Vertrags-Commit. | Konzeptskizze §9–10 · Fachfrage 5 |

---

## Fünf Leitfragen (mitnehmen)

1. **Zweckbindung:** Vorsorge/Übung vs. festgestellte Versorgungskrise — getrennte Rechtsgrundlagen?  
2. **Verantwortliche:** Bund, Land, ggf. gemeinsame Verantwortung mit LEH — wer führt das Register der Berechtigung, wer die Kontingentlogs?  
3. **Trennung ID ↔ Allokation:** Reicht Pseudonym-Token + kurze TTL an der Kasse, um „keine gläserne Einkaufsliste“ zu halten?  
4. **Retention:** Welche Zahlen (Wochen/Monate) für Roh-Abgabe-Logs im Übungsmodus — und wer setzt sie?  
5. **Nächste formale Stufe:** Wann DPIA / AVV — erst nach Pilot-Partnerwahl oder schon vor Tabletop?

---

## Explizit nicht in diesem Termin

- AV-Vertragstext, DPIA-Formular, eID/EUDI-Produktentscheidung  
- Produktiv-Schnittstelle BLE-Lagebild (nur Aggregate-Hypothese)  
- Mail-Versand, Klarname, Live-Deploy  
- Besondere Kategorien (Gesundheit) als Default-Flag — nur „falls rechtlich abgesichert“ markieren

---

## Bezug Need-not-influence

Gleiche Allokationsregeln unabhängig vom Kanal; Datenschutz schützt **Zugang ohne Profilbildung**, nicht Mengenboni für digitale Nutzer (`Allokationsregeln_v1.md` §5–6).

*Ende Kurzagenda. Ablage: `/workspace/foodallo/Datenschutz_Fachgespraech_Agenda.md`*
