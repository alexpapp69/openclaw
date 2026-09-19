# FUTURES vs SPOT — férové porovnanie (2026-09-17)

Alex: *„Momentálne vychádza najlepšie ten future a nie spot."*

Doterajšie čísla sa nedali porovnať priamo (spot mal iné okno, iné trhy a inú intenzitu
kapitálu). Preto jeden beh, dve ramená, **rovnaké trhy, rovnaké okno, rovnaké poplatky**.

**Nastavenie:** trhy BTC/ETH/BNB/SOL/DOGE · 10 000 USDT (5 rukávov po 2 000) ·
poplatky 0,10 %/strana u oboch · dáta Binance 1D (cache `exports/data_cache/`).

- **SPOT** = long-only, buy pri čerstvom upcrosse EMA20>SMA50, sell pri downcrosse alebo SL −8 %,
  po výstupe sa čaká na ďalší čerstvý upcross. (Bez páky, celý rukáv v trhu.)
- **FUTURES** = FLIP obojsmerne, vstup na čerstvý cross, SL = posledné HL/LH (fractal 3),
  strop 8 %, min 1,5 %, riziko 2 % z rukáva, páka max 5×, na flipe obrat, po SL čakanie na nový cross.

**Skripty:** `exports/scripts/futures_vs_spot.py`, `exports/scripts/futures_risk_sweep.py`

## Celá história: 2020-08-11 → 2026-09-17 (6,10 roka)

| | na konci | zisk | ročne | pokles | výnos/riziko | obchodov |
|---|---|---|---|---|---|---|
| SPOT long-only SL 8 % | 826 533 | +8 165 % | +106,2 % | 53,0 % | 2,00 | 121 |
| FUTURES flip 2 % / 5× | 121 257 | +1 113 % | +50,5 % | **7,5 %** | **6,70** | 224 |

Per trh (z 2 000 na rukáv), ročne: BTC spot +44,7 % / fut +10,9 % · ETH +66,7 / +23,4 ·
BNB +40,0 / −3,9 · SOL +80,6 / +49,6 · DOGE +159,6 / +85,0.

Rok po roku (celé portfólio, spot / future):
2021 +2128 % / +574 % · 2022 −12,6 % / +13,3 % · 2023 +9,9 % / −0,5 % ·
2024 +182,7 % / +57,8 % · 2025 −4,5 % / −5,2 % · **2026 −13,1 % / +7,5 %**.

## Len 2024 → dnes (2,71 roka)

| | na konci | zisk | ročne | pokles | výnos/riziko | obchodov |
|---|---|---|---|---|---|---|
| SPOT long-only SL 8 % | 20 221 | +102,2 % | **+29,7 %** | 28,6 % | 1,04 | 56 |
| FUTURES flip 2 % / 5× | 12 588 | +25,9 % | +8,9 % | **7,0 %** | **1,27** | 106 |

## Krivka rizika — future pri rôznom riziku na obchod

| riziko | celá história ročne | pokles | v/riz | 2024→dnes ročne | pokles | v/riz |
|---|---|---|---|---|---|---|
| 2 % | +51,9 % | 7,2 % | 7,23 | +9,0 % | 7,0 % | 1,29 |
| 3 % | +72,6 % | 12,6 % | 5,77 | +12,8 % | 10,3 % | 1,24 |
| 4 % | +91,2 % | 18,0 % | 5,08 | +16,2 % | 13,5 % | 1,20 |
| **6 %** | +123,5 % | 28,1 % | 4,40 | +21,7 % | 19,8 % | 1,10 |
| **8 %** | +150,0 % | 37,2 % | 4,03 | +25,4 % | 25,6 % | 0,99 |
| 10 % | +172,0 % | 45,3 % | 3,80 | +27,4 % | 31,2 % | 0,88 |

**SPOT na porovnanie:** +106,2 %/rok pri poklese 53,0 % (6,1 r.) · +29,7 %/rok pri 28,6 % (2024+).

## Verdikt

1. **Alex má pravdu v rizikovo upravenom pohľade.** Future má pri 2 % rizika pokles 7,5 %
   oproti 53 % u spotu — výnos/riziko 6,7 vs 2,0. A v roku **2026 je future +7,5 %, spot −13,1 %**
   (shortová strana zarába v klesajúcom trhu, spot vie len sedieť a čakať).
2. **V absolútnych peniazoch za celú históriu vedie spot** (826 tis. vs 121 tis.), ale len preto,
   že spot drží **celý rukáv** v trhu (efektívne oveľa väčšie riziko), nie preto, že by bol lepší systém.
3. **Pri rovnakom poklese vyhráva future:** future pri 5–6 % rizika dáva ~+106–123 %/rok pri poklese
   18–28 %, teda rovnaký alebo vyšší výnos ako spot (+106 %/rok) pri **polovičnom poklese**.
4. **V okne 2024 → dnes (býčie) je to remíza:** spot +29,7 % / 28,6 % vs future pri 6–8 % rizika
   +21,7 % / 19,8 % a +25,4 % / 25,6 %. Žiadna strana nemá jasne navrch; výhoda future sa rodí
   v medvedích rokoch (2022, 2026).
5. **Caveaty:** bez fundingu a slippage (future ich má, spot nie); pokles future je portfóliový
   (5 rukávov sa čiastočne vykrýva) — na jednom trhu je pokles väčší; 2024+ je krátka vzorka.

**Odporúčanie:** neporovnávať „spot vs future" ako systémy, ale ako **dve hladiny rizika**.
Rozhoduje, aký pokles Alex unesie: pri tolerancii ~20 % dáva future pri 4 % rizika +91 %/rok
(celá história), čo spot neprekoná inak než poklesom 53 %.
