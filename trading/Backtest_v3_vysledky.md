# Backtest v3 — prvé reálne čísla (2026-09-12)

**Systém:** Alexov Trading Manual, kaskáda breakout → retest → SL → RRR ≥ 1:2
**Dáta:** BTCUSDT + ETHUSDT, 4H, 17.08.2017 → 12.09.2026 (19 866 sviečok / trh)
**Zóny:** automatické (ZigZag 6 % + clustering 1,5 %), rolling 12 mesiacov
**Bez poplatkov a slippage** (dopočítané zvlášť)

## Výsledky

| Metrika | Hodnota |
|---|---|
| **Obchodov** | **199** (97 BTC + 102 ETH) |
| Úspešnosť | **25,1 %** |
| Break-even pri Ø RRR | **14,8 %** |
| Priemerné RRR (výherné) | 3,78 |
| **Priemerné R / obchod** | **+0,20 R** |
| **Celkom** | **+40,2 R** |
| S poplatkami (2× 0,05 %) | **+0,13 R / obchod, +25,0 R** |
| Priemerné riziko | 2,07 % z ceny |
| Priemerná dĺžka | 3 dni |

### Rozpad výstupov
```
SL zasiahnutý:  149  (75 %)    ← väčšina obchodov skončí rýchlo stratou
TP zasiahnutý:   50  (25 %)    priem. RRR 3,78
```
Kontrola: `0,25 × 3,78 − 0,75 × 1 = +0,195 R` ✅ sedí s nameraným +0,20 R.

## Štatistická významnosť

```
smerodajná odchýlka R  ≈ 2,07
štandardná chyba      = 2,07 / √199 = 0,147
t = 0,20 / 0,147      ≈ 1,4
```

**t ≈ 1,4 → ŠTATISTICKY NEVÝZNAMNÉ** (treba t > 2). Výsledok je **nádejný, nie preukázaný**.

## Diagnostika filtračnej kaskády

```
BTC:  559 breakoutov → slabé telo 512 → bez retestu 62 → bez vstupu 29
      → bez TP 34 → RRR<2 337  →  97 obchodov
ETH:  539 breakoutov → slabé telo 451 → bez retestu 52 → bez vstupu 20
      → bez TP 25 → RRR<2 340  → 102 obchodov
```

Najsilnejší filter je **RRR ≥ 1:2** (zahodí ~⅔ setupov) a **telo ≥ 60 %**.
To je presne to, čo Alex napísal do manuálu — systém je selektívny zámerne.

## Čo v tomto backteste NIE JE (zjednodušenia)

1. **1D struktúra (krok 2 checklistu)** — neimplementovaná brána (range/trend).
2. **1H vrstva** — vstup sa hľadá na 4H, nie na 1H.
3. **Zóny sú strojové**, nie Alexove ručné → netestujeme presne jeho systém.
4. **Len long** — manuál je písaný ako „checklist — long".
5. Žiadne čiastočné výstupy (50 % na 4H úrovni) — len jednoduchý SL/TP.

## Záver a ďalšie kroky

Systém má **slabú pozitívnu odchýlku** — čo je presne ten prípad, kde podľa
pôvodného plánu **má zmysel XGBoost filter** (nie na predpoveď ceny, ale na
vytriedenie setupov). Ak by baseline bol jasne ziskový, ML by bol zbytočný;
ak jasne stratový, nepomôže mu. Toto je hraničný prípad — ideálny.

Poradie ďalších krokov:
1. **Robustnosť** — prežije výsledok zmenu parametrov (fractal/zigzag %, telo, RRR)?
2. **Doplniť 1D štruktúrnu bránu** (range/trend) — najväčšie zjednodušenie.
3. **1H vstupná vrstva** — vernosť manuálu.
4. **XGBoost filter** — až na validovanom baseline.

## Súbory

- `exports/scripts/backtest_v1.py` (1D, prvá verzia — bug v breakout detekcii, opravený)
- `exports/scripts/backtest_v2.py` (1D, BTC+ETH, širší SL)
- `exports/scripts/backtest_v3.py` (**4H, 199 obchodov — aktuálny**)
