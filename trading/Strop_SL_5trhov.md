# Strop SL na 5 trhoch, ktoré Alex obchoduje (2026-09-16)

Alex: *„Ja nebudem obchodovať 34 trhov. Budem maximálne BTC, ETH, SOL, DOGE, KAS."*
→ Premerané presne na týchto trhoch. Rovnaký FLIP (EMA20/SMA50, vstup na čerstvý cross,
obrat na flipe, výstup len flip/SL), riziko 2 %, poplatky 0,15 %.
Skript: `exports/scripts/flip_5markets.py`

**Dôležité:** **KAS nie je na Binance** (symbol neexistuje). Dáta pre KAS sú z **Bybit perp**
a majú len **2,7 roka** (od 2023-12-22) — preto sa hodnotí zvlášť.

## 4 veľké trhy (BTC, ETH, SOL, DOGE) — história 5,8–8,9 roka

| Strop SL | Ø ročne | medián ročne | Ø pokles | najhorší pokles | Ø výnos/riziko |
|---|---|---|---|---|---|
| 5 % | +35,1 % | +22,7 % | 22,4 % | 28,3 % | 2,47 |
| **6 % (v manuáli)** | **+32,9 %** | **+21,8 %** | 21,3 % | 26,7 % | 2,26 |
| **8 %** | **+39,7 %** | **+36,3 %** | 19,3 % | 24,7 % | 2,48 |
| 10 % | +36,6 % | +32,0 % | 17,3 % | 20,7 % | 2,70 |
| 12 % | +34,9 % | +29,1 % | 16,3 % | 18,8 % | 2,33 |
| **bez stropu** | +34,3 % | +26,7 % | **12,2 %** | **16,9 %** | **3,00** |

**6 % je tu najhoršie** (najnižší priemer aj medián), hoci na 34 trhoch bolo najlepšie.
Rozdiel: 34-trhový medián ťahali malé/nelikvidné tokeny, kde široký štrukturálny stop
zabíja R. Na veľkých trendových trhoch je to naopak.

Per trh — najlepší strop podľa ročného výnosu:

| Trh | Najlepší | 6 % | bez stropu |
|---|---|---|---|
| BTC | bez stropu +15,4 % | +12,6 % | +15,4 % |
| ETH | 8 % +19,9 % | +18,8 % | +19,3 % |
| SOL | 8 % **+52,8 %** | +24,7 % | +34,1 % |
| DOGE | 5 % +82,8 % | +75,6 % | +68,5 % |

SOL je najcitlivejší: 8 % → +52,8 % vs 6 % → +24,7 %. DOGE je naopak najlepší s tesnejším
stopom (ale DOGE má extrémne čísla — Ø R +10 — a ťahá priemer, preto sa pozeraj na medián).

## KAS (Bybit perp, len 2,7 roka)

| Strop | Obch | Úspešnosť | Ø R | celkom | ročne | pokles |
|---|---|---|---|---|---|---|
| 5 % | 20 | 5,0 % | −0,83 | −16,7 R | −13,1 % | 29,6 % |
| 6 % | 20 | 10,0 % | −0,80 | −16,1 R | −12,6 % | 28,5 % |
| 8 % | 20 | 10,0 % | −0,83 | −16,5 R | −12,9 % | 29,0 % |
| 10 % | 19 | 26,3 % | −0,27 | −5,1 R | −4,5 % | 12,8 % |
| 12 % | 19 | 26,3 % | −0,32 | −6,2 R | −5,3 % | 13,9 % |
| bez stropu | 19 | 36,8 % | −0,13 | −2,4 R | **−2,2 %** | **8,4 %** |

**KAS je v každej verzii záporný** (−2,2 % až −13,1 %). Menšia história a široký stop
aspoň zráža stratu na štvrtinu. Z 19–20 obchodov sa nedá robiť záver o trhu.

## Rozhodnutie (16. 9. 2026, 17:34)

> **KAS vyradiť a prepísať strop na 8 %.** — Alex

→ Manuál v1.2: strop SL **8 %** (bod 3 KROK 4, bod 5), KAS na zozname NEobchodovať (bod 2).

## Záver

- Na **jeho 5 trhoch je lepší širší stop**: 8 % (najvyšší priemer aj medián na 4 veľkých trhoch),
  alebo **bez stropu** (najmenší pokles 12,2 %, najlepší pomer výnos/riziko 3,00).
- **6 % (terajší manuál) je na jeho trhoch najhoršia voľba** — a to je opak toho, čo vyšlo na 34 trhoch.
- **KAS kazí celý portfólio** — je záporný pri každom nastavení. Buď ho vyradiť,
  alebo brať ako experiment s vedomím, že história je krátka.
