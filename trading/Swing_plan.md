# Swing plán — denný trend-following na košíku coinov

Vytvorené 2026-09-19. Backtest: `exports/scripts/swing_plan.py` (cache `exports/data_cache`, 20 coinov,
denné sviečky, 2017-08 → 2026-09, teda 9,1 roka).

## Pravidlá (verzia C — long+short; najlepší pomer výnos/riziko v testoch)

1. **Kedy sa pozerám:** raz denne, po zatvorení dennej sviečky (00:00 UTC).
2. **Vstup (long):** denná sviečka zavrie **nad najvyššou cenou za posledných 20 dní**. Nič viac —
   BTC filter aj 200-dňová podmienka pre long sú vypnuté (presne tak to má testovaná verzia C).
   Vstup na otvorení nasledujúceho dňa.
3. **Vstup (short):** denná sviečka zavrie **pod najnižšou cenou za posledných 20 dní** a zároveň je
   cena **pod 200-dňovým priemerom** daného coinu. Vstup na otvorení nasledujúceho dňa.
4. **Stop:** 2 × priemerný denný rozptyl (ATR14) od vstupu (long pod vstupom, short nad vstupom).
   Nikdy neposúvam.
5. **Výstup:** long zavrie **pod najnižšou cenou za 10 dní**; short zavrie **nad najvyššou cenou za
   10 dní**. Žiadne čiastočné výstupy, žiadne pevné ciele — v testoch boli najhoršie.
6. **Riziko:** 1 % kapitálu na obchod. Max **6 otvorených pozícií** naraz. Notional max 3× hodnota slotu.
7. **Univerzum:** 10–20 likvidných coinov s dlhou históriou (BTC, ETH, SOL, BNB, LINK, DOGE, ADA,
   AVAX, XRP, LTC, TRX, XLM, AAVE, UNI, NEAR, FIL, DASH, ZEC, HBAR, LSK).

## Výsledky (rovnaké poplatky 0,06 % + 0,02 % sklz za stranu, financovanie 0,03 %/deň)

| variant | účet z 10 000 | ročne | max pokles | obchodov | ziskových |
|---|---|---|---|---|---|
| A prielom 20d / výstup 10d | 217 588 | +40,3 % | 41,9 % | 296 | 35,8 % |
| B prielom 20d / výstup pod EMA50 | 679 265 | +59,1 % | 55,3 % | 268 | 34,3 % |
| C A + shorty (obojsmerne) | 321 421 | +46,5 % | 34,0 % | 641 | 37,0 % |
| D návrat k EMA20 / výstup 10d | 214 323 | +40,1 % | 31,9 % | 386 | 36,5 % |
| G A + filter BTC nad EMA200 | 217 588 | +40,3 % | 41,9 % | 296 | 35,8 % |
| H G + širší stop 3×ATR | 93 510 | +27,9 % | 26,8 % | 267 | 40,4 % |

_Prepočítané 2026-09-28 (história sa doplnila do 19. 9.; jediný podstatný rozdiel je lepší rok 2026,
zvyšok sedí). **G vychádza presne ako A — BTC filter je v skripte mŕtvy kód, naozaj nič nerobí.**_

Roky (variant A): 2018 −5 %, 2019 +23 %, 2020 +131 %, 2021 +170 %, **2022 −12 %**, 2023 +25 %,
2024 +29 %, 2025 +54 %, 2026 +25 %. Prakticky ziskových 11 z 20 coinov (C: 14 z 20).

## Prečo to funguje (a prečo to nie je zázrak)

- Neháda smer. Len sedí v trende a **reže straty skoro** — preto vyhrá len ~35 % obchodov, ale víťazi
  sú násobne väčší než prehry.
- Najhoršie roky sú tie, kde trh len chodí do strany (2018, 2022). Vtedy systém stratí málo, ale stratí.

## Obhajoba a korekcia odporúčania (2026-09-19, Alex: „obháj mi to”)

**Korekcia:** BTC filter som odporúčal zle. V dátach **nepomáha** — G 33,7 %/r pri poklese 41,8 %
vs A 37,1 %/r pri 41,9 % (rovnaký pokles, nižší výnos). Vypadol.

**Najlepšie podľa pomeru výnos/pokles je C (long+short): 44,2 %/r pri poklese 34 % (pomer 1,30).**
Long-only A: 37,1 %/r, pokles 41,9 % (0,89). Výstup pod EMA50: 54,9 %/r, ale pokles 55,3 %.

**Robustnosť C (či to nestojí na šťastí):**

- bez troch najlepších coinov (ZEC, BNB, SOL): 31,4 %/r, pokles 34,2 %
- len 10 najlikvidnejších coinov: 41,3 %/r, pokles 30,4 % (pomer 1,36 — najlepší)
- bez BTC a ETH: 34,5 %/r, pokles 37,2 %
- **len BTC samotné: 10,4 %/r** → edge nie je v jednom trhu, ale v košíku

**Stop:** 3×ATR namiesto 2×ATR zníži pokles (26,8 % vs 41,9 %), ale aj výnos (25,8 %/r) — pokojnejšia
voľba, nie lepšia.

**Čo som testoval a zavrhol (s číslami):** prielom 50 dní 25,9 %/r · návrat k EMA20 35,3 %/r ·
výstup pod EMA50 (54,9 %/r, ale 55 % pokles) · BTC filter bez efektu · práca na hodinových dátach
–22 až −31 „dielov rizika”/rok (vlastný ETH pokus).


1. **Prežívajúce coiny.** Test beží na coincoch, ktoré existujú dnes — tie, čo zmizli (LUNA a spol.),
   v ňom nie sú. Reálne výsledky by boli horšie.
2. **Košík ide spolu.** 20 coinov nie je 20 nezávislých stávok; pri poklese padajú naraz. Preto ten
   pokles 40 %.
3. **9 rokov bolo pre krypto prevažne býčích.** Nevieme, či ďalších 9 bude iných.
4. **Financovanie perpetualu** zobralo z výsledku ~23 % (228k → 176k). Počítať s ním.
5. Štatisticky je to **jeden scenár**, nie tisíce pokusov — čísla ber ako odhad, nie záruku.

## Nasadene 2026-09-19 (long+short, paper)

- **Oprava 2026-09-28 (Alex: „chcel som verziu C").** Bežiaci skript mal pri **longu** navyše
  podmienku „nad 200-dňovým priemerom", ktorú testovaná C nemá (C ju má len pri shortoch).
  Long je preto zbavený tejto podmienky → skript teraz presne sedí s testovanou C.
  Dôsledok: C = +46,5 %/r (s filtrom bolo +40,8 %/r); rozdiel je najväčší v roku 2023 (+66 % vs +7 %).
  Existujúce otvorené pozície sa nemenia, mení sa len to, čo sa bude brat do budúcna.
- Skript `exports/scripts/swing_live.py` (check/apply/status), stav `exports/swing_state.json`,
  paper účet **10 000 USD**, riziko 1 % (100 USD) na obchod, max 6 pozícií.
- Denná kontrola po zatvorení sviečky: automation `e49928b1-8fda-447d-b910-96fcfa252dc5`,
  cron `10 0 * * *` UTC, alert na Signal, zápis do Notionu (data source `65807134-...`).
- Signály sa berú z **poslednej zatvorenej** dennej sviečky (Binance posiela aj formujúcu sa).
- Prvé pozície (signál 18. 9.): LONG SOL, UNI, NEAR, ZEC — každá riziko 100 USD.
