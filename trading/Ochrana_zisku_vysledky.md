# Ochrana zisku — výsledky testu (2026-09-16)

**Otázka (Alex):** dá sa doladiť ochrana zisku tak, aby pokles nebol 40 %?

**Skúšané na:** TOP 40 trhov (34 s históriou), 1D, EMA20/SMA50, SL 1,5–6 % (manuál v1.1),
riziko 2 % účtu, zložené, poplatky 0,15 % round trip.
**Skript:** `exports/scripts/flip_protect.py`

## Varianty

| # | Popis |
|---|---|
| **A** | pevný SL, výstup len pri opačnom flipe (= terajší manuál) |
| **B** | SL sa posúva pod každé nové HL / nad nové LH |
| **C** | 50 % pozície von pri +1R, zvyšok so SL na break-even |
| **D** | trailing, ale zapne sa až keď je obchod +1R |
| **E** | C + D (50 % pri +1R a zvyšok trailinguje) |
| **S** | A, ale vstup **len na čerstvý cross** (po SL sa čaká na ďalší flip) |
| **T** | B + len čerstvý cross |
| **U** | D + len čerstvý cross |

## Výsledky

| Var | Ø R | t | ročne | pokles | výnos/riziko | +trhov | najväčší obchod |
|---|---|---|---|---|---|---|---|
| **A** | +0,59 | 1,06 | +10,7 % | 39,6 % | 0,26 | 68 % | 41,9 R |
| B | +0,41 | 0,83 | +14,1 % | 44,5 % | 0,26 | 71 % | 44,1 R |
| C | −0,06 | −1,03 | **−13,7 %** | 56,0 % | −0,22 | **6 %** | 7,1 R |
| D | +0,42 | 0,82 | +13,0 % | 45,6 % | 0,24 | 71 % | 44,1 R |
| E | −0,07 | −1,25 | **−16,4 %** | 58,3 % | −0,23 | **6 %** | 5,2 R |
| **S** | +0,95 | 0,68 | +6,0 % | **22,1 %** | 0,27 | 59 % | 28,3 R |
| T | +0,22 | 0,65 | +2,0 % | 19,7 % | 0,07 | 59 % | 10,4 R |
| U | +0,36 | 0,70 | +3,9 % | 20,3 % | 0,17 | 56 % | 10,6 R |

## Čo z toho vyplýva

1. **Čiastočný výstup + posun SL na BE je najhoršia vec, akú môžeš spraviť (C, E).**
   Ø R padne na nulu, ročne −14 %, kladných je len **6 % trhov** (2 z 34), najväčší
   obchod spadne z ~40 R na ~7 R. Obchodov >10R: 106 → 18.
   Dôvod: FLIP zarába na pár obrovských trendoch; 50 % von pri +1R odstrihne presne ich.

2. **Trailing SL neznížil pokles (B, D).** Výnos vyšší (+14 % vs +10,7 %), ale pokles
   tiež vyšší (44,5 % vs 39,6 %) → pomer výnos/riziko **rovnaký (0,26)**.
   Nič nezískal, len viac obchodoval (5 608 vs 3 411).

3. **Skutočný nález je inde: pravidlo „po SL čakám na ďalší flip".**
   Testovaná verzia (A) po SL vstupuje hneď znova — **to nie je to, čo je napísané v manuáli.**
   Keď sa pravidlo dodrží (S): pokles z 39,6 % → **22,1 %**, Ø R +0,59 → **+0,95**,
   obchodov 3 411 → 1 109. Ročný výnos nižší (+6,0 %), ale pomer výnos/riziko je
   rovnaký (0,27) — čiže: **menej bolesti, nie horší systém.**

## Záver

- **Do manuálu sa nepridáva nič** (žiadny partial, žiadny BE, žiadny trailing).
- **Manuál v praxi = variant S**, nie A → čísla v bode 7 manuálu popisujú A.
- Kto chce viac výnosu, hýbe **rizikom na obchod**, nie ochranou zisku.

| Trh (S) | ročne | pokles | Ø R |
|---|---|---|---|
| BTC | +14 % | 20 % | +1,46 |
| ETH | +16 % | 24 % | +1,99 |
| DOGE | +32 % | 8 % | +3,71 |
| SOL | +20 % | 28 % | +2,32 |
| BNB | +17 % | 19 % | +3,27 |

## Obmedzenia

- Median t = 0,68 (S) / 1,06 (A) → **štatisticky nepreukázané**.
- Pomer výnos/riziko ~0,27 = približne ako držanie BTC.
- Zoznam TOP 40 sa mení s časom; obsahuje aj nové/nelikvidné tokeny (PUMP, TRUMP…).
- Test len na 1D, len dlhé+krátke, bez slippage nad rámec poplatku.
