# Setup Rules v0.1 — kalibrácia manuálu

*Vzniká 2026-09-12 z rozhovoru s Alexom. Každé pravidlo je potvrdené jeho slovom
alebo odvodené z jeho reálnych zón. Most medzi `Trading_Manual_v1.0.md` a kódom.*

---

## ⛓️ POSTUPNOSŤ — chrbtová kosť systému

Toto je najdôležitejšia časť. **Nie je to jeden graf — sú to tri, v poradí.**
Každý stupeň je **brána**: ak neprejde, systém zastaví a nič sa nedeje.

```
┌─────────────────────────────────────────────────────────────┐
│  STUPEŇ 1 ── 1D ── KONTEXT                                  │
│  "Kto má kontrolu nad trhom?"                               │
│                                                             │
│  1. Nájdi významné S/R zóny      (šírka ~2 %, ≥2 reakcie)   │
│  2. Urči 1D market structure     (fractal 5)                │
│     → kupujúci / predávajúci / RANGE                        │
│  3. Ak RANGE → čakám. Koniec.                              │
│  4. Ak breakout: close NAD/POD zónou + telo ≥ 60 %          │
│                                                             │
│  🚦 BRÁNA: jasný 1D scenár?  →  inak STOP                   │
└──────────────────────────────┬──────────────────────────────┘
                               ▼
┌─────────────────────────────────────────────────────────────┐
│  STUPEŇ 2 ── 4H ── ZÓNA ZÁUJMU                              │
│                                                             │
│  1. Štruktúra od posledného 1D Low / High                   │
│  2. Hľadám HH + HL (bullish)     (fractal 5 — POTVRDENÉ)    │
│  3. Súlad 4H s 1D                                            │
│                                                             │
│  🚦 BRÁNA: 4H v súlade s 1D?  →  inak STOP                  │
└──────────────────────────────┬──────────────────────────────┘
                               ▼
┌─────────────────────────────────────────────────────────────┐
│  STUPEŇ 3 ── 1H ── VSTUP                                    │
│                                                             │
│  1. Určím posledné High, Low a aktuálnu cenu                │
│  2. Breakout: close NAD posledným High                      │
│  3. Korekcia a RETEST prerazenej úrovne                     │
│     → cena musí VSTÚPIŤ do zóny                             │
│  4. Price Action: ideálne sviečka s dlhým spodným knôtom    │
│  5. SL pod relevantným HL + rezerva podľa likvidity         │
│  6. Kontrola RRR ≥ 1:2                                      │
│  7. Veľkosť pozície = riziko / vzdialenosť SL               │
│                                                             │
│  🚦 BRÁNA: RRR ≥ 1:2?  →  inak obchod NEOTVÁRAM             │
└──────────────────────────────┬──────────────────────────────┘
                               ▼
                    ✅ VSTUP DO OBCHODU

┌─────────────────────────────────────────────────────────────┐
│  MANAŽMENT                                                  │
│  • 50 % pozície na prvej významnej 4H úrovni (ak RRR ≥ 1:1) │
│    → SL zvyšku na úroveň TP1 (break even)                   │
│  • zvyšok na hlavnom 1D cieli                               │
│  • SL posúvam pod každé nové relevantné 1H HL               │
│    (relevantné HL = také, po ktorom cena spraví nové HH)    │
└─────────────────────────────────────────────────────────────┘
```

**Zásada:** *„Nemusím obchodovať každý deň. Mojou úlohou je čakať."*
Každá brána je miesto, kde systém aktívne **neobchoduje**.

---

## Zamknuté knoby

| # | Pravidlo | Hodnota | Zdroj |
|---|---|---|---|
| **S1** | Swing (fractal) | **5 sviečok** | ✅ Alexovo oko (4H) |
| **Z1** | Šírka S/R zóny | **~2,0 %** (jeho zóny 1,92 % / 2,61 %) | ✅ jeho zakreslenie |
| **Z2** | Rešpekt zóny | ≥ 2 reakcie trhu | predpoklad |
| **R1** | Retest | cena musí **vstúpiť do zóny** | ✅ Alex |
| **B1** | Breakout | **close NAD CELOU zónou** (nie knôt) | ✅ Alex |
| **B2** | Range | kým nie je B1 → **RANGE**, neobchodovať | ✅ Alex + manuál 4.6 |
| **B3** | Bullish trend | až po B1 | ✅ Alex |
| **B4** | Sila breakoutu | 1 zavretá sviečka, **telo ≥ 60 %** | ✅ Alex („c") |
| **M1** | Riziko | 1 % účtu / 50 € na obchod | manuál 10 |
| **M2** | RRR | min **1:2** | manuál 7 |
| **M3** | Čiastočný výstup | 50 % na 4H úrovni (RRR ≥ 1:1), SL → BE | ✅ Alex |
| **M4** | Hlavný TP | 1D zóna | ✅ Alex |
| **M5** | Max. obchody | 1 na trh, pokiaľ nie je uzavretý; iný trh OK | manuál 10 |

## Kľúčové zistenia

1. **„Range" nie je vlastnosť swingov — je to vlastnosť ZÓN.**
   Fractal vie povedať len „toto high bolo vyššie". Nevie povedať „stále sme
   v pásme". Bez range detektora by systém obchodoval longy v range.

2. **Alexovo oko je „pomalé":** na 4H mu sedí fractal 5 (nie 2 ani 3).

3. **Toto je kaskáda, nie jedna rovina.** 1D dáva kontext, 4H dáva zónu,
   1H dáva vstup. Každý stupeň má vlastnú bránu.

4. **Presnosť OCR:** zóny z jeho screenshotu vytiahnuté s odchýlkou ~0,1 %.

## Otvorené otázky

- **STUPEŇ 2 detail:** čo presne znamená „štruktúra od posledného 1D Low"?
  (odkiaľ presne začínaš počítať?)
- **1D swing:** sedí na 1D tiež fractal 5, alebo iné číslo?
- **Vstup 1H:** kde presne meriaš vstup po reteste? (close sviečky s knôtom? okraj zóny?)
- **SL:** pod relevantným 1H HL, alebo pod spodnou hranou zóny? (dva rôzne prípady?)
- **Likvidita:** ako merateľne definovať „rezervu podľa likvidity"?
- **Z2:** koľko reakcií robí zónu „významnú"? (2, 3, viac?)
- **Knoby na test:** telo 50/60/70 %; fractal 4/5/6; retest okno

## Aktuálna situácia (2026-09-12)

```
BTC 77 330
  1D: RANGE  (Alexovo čítanie)
  support      75 964 – 77 438   (1,92 %)
  rezistencia  80 152 – 82 270   (2,61 %)
  cena VNÚTRI support zóny

  → STUPEŇ 1 = čakám, žiadna brána neprešla
  → bullish až po 1D close NAD 82 270 (silná sviečka)
```
