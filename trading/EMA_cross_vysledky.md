# EMA 10/30 cross — výsledky a walk-forward (2026-09-13)

## Pravidlá (Alexove)

```
1D graf, EMA 10 a EMA 30

LONG  = EMA10 prekríži EMA30 nahor
   SL = pod posledné HL (Higher Low) pred crossom
   TP = 2 × riziko                       (RRR 1:2)

SHORT = EMA10 prekríži EMA30 nadol
   SL = nad posledné LH (Lower High) pred crossom
   TP = 2 × riziko

+ RIZIKO OBMEDZENÉ NA 5 % z ceny (Alex)
Swingy: fractal 3 (max 3 sviečky dozadu — Alex)
```

## Výsledky podľa variantu SL (celé obdobie 2017–2026)

| Variant SL | Obchodov | Úspešnosť | Ø R | t | Riziko |
|---|---|---|---|---|---|
| štrukturálne (bez limitu) | 73 | 42,5 % | +0,27 | 1,57 | 12,0 % |
| pevne 5 % | 157 | 42,7 % | +0,28 | 2,36 | 5,0 % |
| **štrukturálne, max 5 %** | 151 | 45,0 % | **+0,35** | **2,88** | 4,7 % |

## WALK-FORWARD (rozdelenie času)

```
IN-SAMPLE  2017 → 2022        OUT-OF-SAMPLE  2022 → 2026
```

| Variant | IS Ø R | IS t | OOS Ø R | OOS t |
|---|---|---|---|---|
| struct 12 % (vybraný na IS) | +0,40 | 1,44 | +0,19 | 0,82 |
| fixed 5 % | +0,27 | 1,51 | +0,29 | 1,80 |
| **cap 5 %** | **+0,38** | **2,06** | **+0,33** | **2,01** |
| fixed/cap 8 % | +0,23 / +0,17 | ~1,2 | −0,01 | −0,08 |

## Záver

1. **Variant vybraný na IS prežil** OOS (+0,40 → +0,19). Oslabil, ale nezmizol — normálne správanie.
2. **Najsilnejší je „cap 5 %":** kladný a štatisticky významný v **oboch** poloviciach
   (+0,38 R / t=2,06 a +0,33 R / t=2,01). Prvý výsledok za celý projekt, ktorý
   prešiel cez t > 2 **dvakrát, na nezávislých dátach.**
3. **Limit rizika 5 % je kľúčový.** Pri 8 % sa edge stratí (−0,01). Pri 3 % je slabší.
4. Timeframe rozhoduje: **na 4H je edge nulový** (529 obchodov, +0,02 R, t=0,24).

## Obmedzenia (čo ešte nie je overené)

- Len BTC a ETH. Žiadne iné trhy.
- Bez poplatkov a slippage.
- Skúšali sme ~7 variantov → mierny výberový efekt (multiple comparisons).
- RRR fixné 1:2, EMA fixné 10/30 — neoptimalizované.
- Žiadne čiastočné výstupy, žiadny trailing.

## Porovnanie systémov (celé obdobie)

| Systém | Obchodov | Úspešnosť | Ø R | t |
|---|---|---|---|---|
| Trading Manual (breakout → retest) | 199 | 25,1 % | +0,20 | 1,40 |
| EMA 10/30 cross + cap 5 % | 151 | 45,0 % | +0,35 | 2,88 |

## Súbory
- `exports/scripts/ema_cross3.py` — tri varianty SL
- `exports/scripts/ema_walkforward.py` — walk-forward
- `exports/scripts/ema_cross.py`, `ema_cross2.py` — prvé verzie

## Čiastočný výstup + break even (2026-09-13)

| Variant | Obchodov | Úspešnosť | Ø R | t |
|---|---|---|---|---|
| A — nič | 151 | 45,0 % | +0,35 | 2,88 |
| B — plný BE pri +1R | 160 | 34,4 % | +0,28 | 2,72 |
| C — 50 % pri +1R + BE (manuál) | 160 | **59,4 %** | +0,29 | 3,17 |
| D — 50 % pri +1R, SL ostáva | 151 | 49,0 % | +0,33 | **3,29** |

Walk-forward: A +0,38/+0,33 · C +0,26/+0,32 · D +0,32/+0,34 — **všetky prežili**.
Plný BE (B) škodí: 25 % obchodov sa vráti na vstup a časť z nich by inak došla k TP.

## S poplatkami (Bitunix: Taker 0,05 %/strana)

| Round-trip náklad | A Ø R (t) | C Ø R (t) |
|---|---|---|
| 0 % | +0,33 (3,29) | +0,29 (3,17) |
| 0,10 % | +0,30 (3,03) | +0,27 (2,85) |
| 0,20 % | +0,28 (2,76) | +0,24 (2,53) |
| 0,25 % (realistický) | +0,27 (2,62) | +0,22 (2,37) |
| 0,40 % (pesimistický) | **+0,23 (2,22)** | +0,18 (1,89) |

**Edge prežíva aj pesimistické poplatky (0,40 %).** Walk-forward s 0,20 %:
A +0,27/+0,29 · C +0,21/+0,25 · D +0,27/+0,29.

## ⛔ Test na 31 trhoch (2026-09-15) — ROZHODUJÚCI VÝSLEDOK

Rovnaké pravidlá na 40 najväčších USDT pároch (31 malo dosť histórie):

```
kladných:      15  (48 %)
záporných:     16  (52 %)
t > 2:          4
medián Ø R:   −0,006     ← prakticky presná NULA
celkom obchodov: 1542
```

**Mediánový trh = nula.** Polovica trhov zarába, polovica stráca → **presne ako náhoda.**

⚠️ **Pozor:** do testu sa dostali **stablecoiny a pegnuté aktíva** (USDCUSDT −3,89 R,
USD1USDT −2,51, FDUSDUSDT −1,86, EURUSDT −0,47, PAXGUSDT −0,24). Tie **nič neznamenajú**
— na peggnutom aktíve nemá EMA cross čo merať. **Vždy ich vylúčiť.**
Po vylúčení: 26 trhov, ~15 kladných / ~11 záporných, priemer +0,085 R.

| Kladné | Ø R | t | | Záporné | Ø R | t |
|---|---|---|---|---|---|---|
| TRUMP | +0,62 | 1,43 | | HOLD | −0,55 | −1,87 |
| LINK | +0,38 | 2,64 | | XRP | −0,24 | −1,94 |
| ADA | +0,35 | 2,34 | | UNI | −0,14 | −0,88 |
| DOGE | +0,33 | 2,06 | | XLM | −0,11 | −0,85 |
| BTC | +0,29 | 2,08 | | AVAX | −0,10 | −0,64 |
| ETH | +0,20 | 1,47 | | SOL | −0,07 | −0,42 |
| BNB | +0,22 | 1,36 | | TRX | −0,04 | −0,30 |

### 🚨 Verdikt: „veľké trhy“ NIE JE vzorec

Všetky sú to veľké likvidné trhy — polovica zarába, polovica stráca. Žiadny
vzorec veľkosti. **BTC a ETH v pozitívnom zozname sú pravdepodobne náhoda**
(pri 31 testoch sa ~1–2 „významné“ objavia len tak).

**→ Systém NEMÁ robustný edge naprieč trhmi.** Včerajšie BTC/ETH výsledky boli
pravdepodobne šťastný výber dvoch trhov.

**Skript:** `exports/scripts/ema_many.py`

## 🆕 FLIP systém (2026-09-15) — najlepší výsledok projektu

**Pravidlá (Alexove, z jeho indikátora + manuálu):**
```
Vstup : EMA 20 prekročí SMA 50  (nahor → long, nadol → short)   [1D]
SL    : pod posledné HL / nad posledné LH (fractal 3), max 5 % od vstupu
TP    : ŽIADNY fixný — držím až kým nepríde OPAČNÝ FLIP
Po SL : čakám na ďalší flip
```
Poplatky 0,15 % na flip. Pozícia 100 % účtu (zložené) → účet z 100 USDT.
**Pozor:** shorty sa musia počítať `1 − výstup/vstup` (nie `vstup/výstup − 1`) —
prvá verzia mala túto chybu a nafukovala výsledky (medián +68 % → +31 % ročne po oprave).

### Výsledky — TOP 40 trhov (34 s dostatočnou históriou)

```
kladné ročne:      25 z 34  (74 %)
medián ročne:      +19,6 %
medián poklesu:    42,4 %
medián Ø R:        +0,88
medián t:          +1,11
medián výnos/riz:  0,45
celkom obchodov:   3 913
```

Najlepšie: DOGE +78 %, SOL +58 %, ADA +51 %, NEAR +46 %, PUMP +46 %, FET +70 %
Najhoršie: HOLO −58 %, REZ −31 %, TAO −22 %, XLM −16 %, XRP −14 %, LINK −12 %

Typický profil: **úspešnosť 8–26 %** (!!), ale Ø R +0,3 až +4,4. Čistý trend-following —
veľa malých strát, zopár obrovských výher. SL drží straty krátke, žiadny fixný TP
necháva výhry bežať do flipu.

### Stabilita (BTC/ETH, 6 štartov × 2 trhy)
**12 z 12 kladných.** Ø R +0,30 až +1,53. Poklesy 13–37 % (oproti 74–83 % pri držaní).
3× t > 2 (ETH 2021: 2,17).

### Porovnanie systémov na mnohých trhoch
| Systém | % kladných trhov |
|---|---|
| EMA 10/30 + SL/TP fixné | 48 % (15/31) |
| **FLIP + SL (drž do opaku)** | **74 % (25/34)** |

→ **„Držať do opaku" namiesto fixného TP je to, čo spravilo rozdiel.**

### Caveaty
- medián t = 1,11 → **štatisticky nepreukázané**
- medián výnos/riziko 0,45 = rovnaké ako držanie BTC → nie je jasná výhoda risk-adjusted
- pozícia 100 % účtu — pri poklese 42 % to bolí
- 9 trhov z 34 je záporných
- testované len na 1D

**Skript:** `exports/scripts/ema_flip_sl.py` (TOP_N), `flip_stability.py`

## 💰 PREVOD NA PENIAZE + REALISTICKÁ VERZIA (2026-09-15)

**Zadanie:** 10 000 USDT, riziko 2 % na obchod, future 5× páka, trhy BTC/ETH/SOL/DOGE/BNB.

### ⚠️ Chyba, ktorú treba poznať: SL môže byť absurdne tesný
Pri SL = „posledné HL" môže byť stop **0,014 % od vstupu** → pozícia by žiadala **147× páku**.
Fix: **SL vždy 0,5–5 %** (min. vzdialenosť). Potom max páka = 2 % / 0,5 % = **4,0×** → 5× stačí vždy.

### Výsledky (nereálne zloženie)
```
10 000 USDT → 5 221 712 259 USDT  (+336 % ročne)  ← FANTÁZIA
```
**Prečo je to fantázia:** 676 obchodov, ale **30 z nich (R > 10) dalo +1 606 R** —
zvyšných **646 bolo v mínuse (−194 R)**. Najväčší obchod **+366 R** (SL 0,5 % + 4× páka
+ 183 % pohyb ceny = +732 % účtu v jednom obchode). Nedosiahnuteľné v praxi.

### Realistická verzia (2024–2025)
SL **1,5–5 %**, poplatky **+ slippage 0,30 %** round trip:

| Trh | Obchodov | Úspešnosť | Ø R | Najlepší |
|---|---|---|---|---|
| ETH | 31 | 29,0 % | +0,93 | +14,89 |
| DOGE | 35 | 22,9 % | +2,02 | +44,38 |
| BNB | 31 | 22,6 % | +0,60 | +31,91 |
| BTC | 37 | 16,2 % | +0,05 | +11,08 |
| SOL | 44 | 18,2 % | −0,20 | +6,67 |
| **SPOLU** | **178** | 21,3 % | **+0,62** | +44,38 |

```
fixné riziko 200 USDT/obchod:   10 000 → 32 235 USDT  (+222 %)
zložené 2 %:                    10 000 → 43 042 USDT  (+330 %)  max. pokles 44,8 %
```
Proti nereálnej verzii: max R +366 → **+44**, obchodov s R>10: 30 → **7**.
Realistické predpoklady teda zoškrtali výsledok z miliárd na desaťtisíce. **Toto je to číslo, ktorému sa dá veriť.**

**Caveaty:** len 2 roky, býčí trh, 5 trhov, 178 obchodov, SOL mierne záporné.

## ⏭️ ČO ZOSTÁVA NEOTESTOVANÉ

Z pôvodného zoznamu sme vyškrtli takmer všetko. Zostáva jediné:

> **Alexov manuál so zónami** (1D štrukturálna brána + 1H vstup) — nikdy nedokončený.
> Je postavený na **štruktúre**, nie na križiatoch → iná trieda systému.
> Definícia zón je hotová (`Zony_definicia.md`), chýba iba ich výber a zapojenie do vstupu.

## Robustnosť — test na 5 trhoch (2026-09-13)

Rovnaké pravidlá (manuál C, RRR 1:2,5, cap 5 %, poplatky 0,25 %):

| Trh | Obchodov | Úspešnosť | Ø R | t |
|---|---|---|---|---|
| BTC | 82 | 62,2 % | +0,29 | 2,08 ✅ |
| ETH | 78 | 56,4 % | +0,20 | 1,47 🟡 |
| BNB | 69 | 55,1 % | +0,22 | 1,36 🟡 |
| SOL | 58 | 43,1 % | −0,07 | −0,42 ❌ |
| XRP | 99 | 34,3 % | −0,24 | −1,94 ❌ |
| **SPOLU** | 386 | 49,7 % | **+0,07** | **1,06** |

**Záver: systém sa NEPRENÁŠA na menšie trhy.** Kladné sú BTC, ETH, BNB (veľké,
likvidné, trendové); SOL a XRP záporné. Hypotéza: EMA cross potrebuje „čistý" trend.

⚠️ **Dôležité metodické upozornenie (Alexov postreh):** spájanie BTC+ETH dávalo
t = 2,52, ale **BTC samo má 2,08 a ETH len 1,47**. Spájanie korelovaných trhov
**nafukuje t** — nie sú to nezávislé pozorovania. Po korekcii na koreláciu je reálne
t ≈ 2,0 (na hranici). **Nespájať trhy len preto, aby vyšlo vyššie t.**

## Stabilita v čase — 10 štartovacích dátumov (2026-09-13)

| Od | Trh | Obchodov | Úspešnosť | Ø R | t | Ročne | Max. pokles |
|---|---|---|---|---|---|---|---|
| 2020 | BTC | 64 | 60,9 % | +0,24 | 1,51 | 4,3 % | 13,7 % |
| 2020 | ETH | 64 | 59,4 % | +0,25 | 1,64 | 4,6 % | 9,5 % |
| 2021 | BTC | 57 | 63,2 % | +0,28 | 1,70 | 5,5 % | 13,7 % |
| 2021 | ETH | 59 | 61,0 % | +0,25 | 1,65 | 5,1 % | 6,2 % |
| 2022 | BTC | 50 | 60,0 % | +0,21 | 1,18 | 4,3 % | 13,7 % |
| 2022 | ETH | 49 | 61,2 % | +0,29 | 1,68 | 5,8 % | 6,2 % |
| 2023 | BTC | 39 | 69,2 % | +0,42 | **2,05** | 8,9 % | 13,7 % |
| 2023 | ETH | 39 | 66,7 % | +0,38 | **2,04** | 8,0 % | 5,3 % |
| 2024 | BTC | 32 | 62,5 % | +0,22 | 0,96 | 4,9 % | 13,7 % |
| 2024 | ETH | 27 | 66,7 % | +0,34 | 1,55 | 6,8 % | 5,3 % |

**10 z 10 kombinácií kladných.** Ø R nikdy pod +0,21; úspešnosť nikdy pod 59 %;
pokles vždy 5–14 %. To je najsilnejší dôkaz robustnosti za celý projekt.

## Porovnanie s držaním (od 1.1.2022)

| | Systém (2 % riziko) | Držanie |
|---|---|---|
| BTC | +21,8 % (pokles 13,7 %) | +61,6 % (pokles 66,9 %) |
| ETH | +30,5 % (pokles 6,2 %) | **−33,8 %** (pokles 74,0 %) |

Systém je **konzistentný** (+22 % / +31 %), držanie je lotéria (+62 % / −34 %).
Systém obchoduje **long aj short**, takže zarába aj v medvedom trhu.

## ⏭️ KDE POKRAČOVAŤ (handover)

**Stav:** systém je kladný a stabilný na BTC/ETH, ale **štatisticky nepreukázaný** (t < 2 vo väčšine testov) a **nefunguje na SOL/XRP**.

**Otvorené smery:**
1. **Prečo SOL/XRP zlyhávajú** — možno cap 5 % je primalý (majú väčšie sviečky).
   Skúsiť iný cap, alebo ATR-based SL.
2. **Viac trhov** (30–50) — overiť, či je „veľké trhy" vzorec alebo náhoda.
3. **Dokončiť manuál so zónami** — 1D štruktúrna brána + 1H vstup (nedokončené).
4. **Iné EMA / timeframe** — neoptimalizované.
5. **Kombinácia:** EMA cross ako filter + zóny ako vstup.

**Skripty (všetky v `exports/scripts/`):**
- `ema_cross3.py` — 3 varianty SL
- `ema_walkforward.py` — walk-forward
- `ema_partial.py` — čiastočný výstup + BE
- `ema_fees.py` — poplatky
- `ema_equity.py` — rast účtu
- `ema_multi.py` — 5 trhov
- `ema_stability.py` — **10 štartovacích dátumov (najsilnejší dôkaz)**
- `eth_2022.py` — ETH len od 2022

**Prostredie:** `/root/.venv-chart/bin/python` (matplotlib). Dáta: Binance public API.
**Pozor:** pri `sed` je `&` v náhrade špeciálny znak (celý nález) — escapovať `\&`.
**Pozor:** `pgrep -f 'vzor'` matchne aj vlastný shell → použiť `pgrep -f 'vz[o]r'`.
