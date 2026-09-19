# Strop SL — koľko kazí tesný stop? (2026-09-16)

## Vysvetlenie po lopate

**Čo je „strop SL":** SL (stop-loss) je cena, pri ktorej vystúpiš so stratou. Manuál hovorí:
daj ho pod posledné Higher Low (long) / nad posledné Lower High (short) — tam, kde by sa
trend „rozbil". Lenže na malých trhoch môže tá štrukturálna úroveň byť aj 15 % od vstupu.
Preto je tu strop: **ak je štrukturálny SL ďalej než X %, priškr time ho na X %**.

**„Bez stropu" = stop dáš presne tam, kam ukazuje graf** (posledný swing), nech je to 5 %
alebo 15 %. Žiadne priškrcovanie. V teste bol medián takej vzdialenosti **14,8 %**.

**Prečo na tom záleží pri fixnom riziku 2 %:** 1R = vzdialenosť SL. Ak riskuješ 200 USDT
(2 % z 10 000) a SL je 8,6 % od vstupu, kúpiš pozíciu za `200 / 0,086 = 2 326 USDT`.
Ak SL priškrtíš na 6 %, kúpiš za `200 / 0,06 = 3 333 USDT` — väčšiu.
Riziko v peniazoch je **rovnaké (200)**, mení sa len veľkosť pozície.

| | strop 6 % | bez stropu (štrukturálny 8,6 %) |
|---|---|---|
| SL cena (januárový ETH short) | 2 985,90 | 3 059 |
| vzdialenosť | 169 USDT | 242 USDT |
| veľkosť pozície | 1,18 ETH (3 333 USDT) | 0,83 ETH (2 326 USDT) |
| výsledok obchodu | SL → **−200 USDT** | prežil → close 2 203,39 → **+507 USDT** |

## Stĺpce v tabuľkách

| Stĺpec | Znamená |
|---|---|
| Obch | koľko obchodov dokopy (34 trhov) |
| Ø R | priemerný výsledok na obchod v jednotkách rizika (+0,54 R = 54 % rizika na obchod) |
| t | štatistická vierohodnosť; pod 2 = mohlo to byť aj náhodou |
| ročne | mediánový ročný výnos účtu (2 % riziko na obchod, zložené) |
| pokles | najhorší prepad od vrcholu (max drawdown) |
| výn/riz | ročný výnos ÷ pokles — koľko výnosu za jednotku bolesti |
| +trhov | z 34 testovaných trhov, koľko skončilo v pluse |
| najväčší | najlepší jednotlivý obchod v R |

**Prečo širší stop = menej peňazí z rovnakého pohybu:** R = pohyb ceny ÷ vzdialenosť SL.
Ak cena spraví +10 % a SL je 5 %, je to +2R (× 200 USDT = +400). Ten istý pohyb so SL 10 %
je len +1R (+200). Zato ťa ale menej často vyhodí.

**Podnet (Alex):** *„SL to kazia, napríklad ten januárový short mohol urobiť kľudne 18 %."*

**Test:** ten istý FLIP (EMA20/SMA50, vstup na čerstvý cross, obrat na flipe, výstup len
flip/SL, riziko 2 % účtu), mení sa **iba maximálna vzdialenosť SL**.
Skript: `exports/scripts/flip_slcap.py`, 34 trhov (TOP 40 s históriou).

## Januárový ETH short — overené

```
vstup 25. 1. 2026 @ 2 816,89 (short)
max. protipohyb:  3 045,78  (28. 1.)  = +8,1 % PROTI pozícii
manuálny strop:   6,0 %      → SL zasiahnutý 27. 1. → −1,00 R
```

Čiže short potreboval stop ďalej než **8,1 %**, aby prežil. A čo by dostal:

```
minimum pred marcovým crossom: 1 747,80 (6. 2.)   = +38,0 % pre short
close pri marcovom crosse:     2 203,39 (18. 3.)  = +21,8 % pre short
```

**Alex má pravdu** — 18 % nebolo prehnané, v najlepšom bode to bolo 38 %.
So stropom 10 % by obchod prežil a uzavrel sa na flipe 18. 3. za **+2,55 R** (namiesto −1 R).

## Ale celkovo to nevychádza

| Strop SL | Obch | Ø R | t | ročne | pokles | výn/riz | +trhov | najväčší |
|---|---|---|---|---|---|---|---|---|
| 5 % | 1 286 | +0,14 | 0,28 | +0,4 % | 25,8 % | 0,02 | 53 % | 12,4 R |
| **6 % (manuál)** | 1 280 | **+0,54** | 0,65 | **+4,6 %** | 23,8 % | 0,14 | 59 % | 18,4 R |
| 8 % | 1 273 | +0,34 | 0,40 | +2,1 % | 21,1 % | 0,12 | 59 % | 13,3 R |
| 10 % | 1 269 | +0,17 | 0,34 | +0,8 % | 19,3 % | 0,08 | 59 % | 11,6 R |
| 12 % | 1 264 | +0,27 | 0,59 | +2,7 % | 18,5 % | 0,18 | 62 % | 10,0 R |
| **bez stropu** | 1 259 | +0,30 | 0,60 | +3,4 % | **13,8 %** | **0,27** | **71 %** | 9,2 R |

**Mechanizmus:** riziko je fixné 2 % účtu, takže **širší stop = menšia pozícia**.
Vyhneš sa stopom (−1 R), ale **každý víťaz vydá menej R**:

```
májový ETH short:  +2,24 R pri strope 5 %   →   +0,94 R pri strope 12 %
```

Rovnaký cenový pohyb, ale delený väčším stopom.

## ETH 2026 podľa stropu (jediný trh, ilustračne)

| Strop | 2026 spolu | Januárový short |
|---|---|---|
| 5 % | +4,54 R | −1,00 R |
| 6 % | +3,28 R | −1,00 R |
| 8 % | +1,71 R | −1,00 R (stop 8,0 % nestačil) |
| **10 %** | **+4,48 R** | **+2,55 R** (prežil) |
| 12 % | +4,30 R | +2,55 R |
| bez stropu | +5,05 R | +2,55 R |

Na ETH 2026 širšie stopy pomáhajú (+4,48 vs +3,28 R) — presne o ten januárový obchod.
**Ale to je jeden trh a jeden rok.** Na 34 trhoch je medián najlepší pri 6 %.

## Verdikt

- Tesný stop **reálne ukrajuje obchody** — januárový short je dokázaný príklad.
- Širší stop to **nevráti v celkovom výnose** (menšia pozícia → menšie R z každého víťaza).
- Čo širší stop **naozaj dáva**: nižší pokles (13,8 % bez stropu vs 23,8 % pri 6 %) a viac
  kladných trhov (71 % vs 59 %) — teda **hladší priebeh a lepší pomer výnos/riziko (0,27 vs 0,14)**.
- Možnosti: **6 % (max výnos)** · **8–10 % (kompromis)** · **bez stropu (najhladšie, najmenší výnos)**.

⚠️ Riziko v peniazoch je pri všetkých stropoch **rovnaké** (2 % účtu) — mení sa len veľkosť pozície.
