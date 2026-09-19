# Výstup skôr než flip — SMA50 / EMA20 (2026-09-16)

**Otázka (Alex):** namiesto čakania na opačný flip vystúpiť pri **prvom dennom close
za SMA50** (long pod, short nad). Prípadne skôr, pri EMA20.

**Test:** `exports/scripts/flip_exit.py`, 34 trhov (TOP 40 s históriou), 1D, EMA20/SMA50,
SL 1,5–6 %, riziko 2 %, poplatky 0,15 %, vstup len na čerstvý cross (ako manuál).

| Var | Pravidlo výstupu | Obch | Ø R | t | ročne | pokles | výnos/riziko | +trhov | najväčší |
|---|---|---|---|---|---|---|---|---|---|
| **S** | len pri opačnom flipe (manuál) | 1 070 | **+0,51** | 0,56 | **+3,6 %** | 22,1 % | **0,14** | **56 %** | 16,1 R |
| **F** | prvý close za SMA50 | 1 293 | +0,04 | 0,13 | **−0,6 %** | 21,5 % | −0,02 | 47 % | 13,2 R |
| **G** | SMA50, ale len keď je ≥ +1R | 1 249 | +0,13 | 0,30 | +0,6 % | 21,8 % | 0,02 | 53 % | 13,2 R |
| **X** | prvý close za EMA20 | 1 297 | +0,16 | 0,29 | +1,0 % | **17,9 %** | 0,08 | 53 % | 8,1 R |

## Verdikt

**Nie. Výstup pri SMA50 edge zruší** — Ø R z +0,51 na +0,04, ročne z +3,6 % na −0,6 %,
kladných trhov z 56 % na 47 %. Počet obchodov pritom **stúpol** (1 070 → 1 293), takže
nejde o „menej obchodov" — ide o to, že **tie isté obchody skončia skôr**.

Mechanizmus: kríž EMA20/SMA50 vzniká **na úrovni SMA50**. Hneď po vstupe sa cena bežne
dotkne SMA50 (bežný pullback) → pravidlo vystúpi pri +0,2R, a potom čaká na ďalší čerstvý
cross — ktorý v tom trende nemusí prísť. Presne to je najhoršia kombinácia: malý zisk von
a zmeškaný zvyšok trendu.

**Podmienka „len keď je obchod ≥ +1R" (G) nepomohla** (−0,7 % → +0,6 %). Aj tak odstrihne
trend po prvom väčšom pullbacku — len o kus neskôr.

**EMA20 (X)** je lepšia než SMA50, ale stále horšia než nič: Ø R +0,16, najväčší obchod
8,1 R (oproti 16,1 R). Jej jediná výhoda je pokles 17,9 % namiesto 22,1 %.

## Per-market (ročne / pokles / Ø R)

| Trh | S (manuál) | F (SMA50) | G (SMA50 ≥+1R) | X (EMA20) |
|---|---|---|---|---|
| BTC | +15 % / 20 % / +1,60 | +14 % / 22 % / +1,33 | +17 % / 18 % / +1,60 | +3 % / 15 % / +0,28 |
| ETH | +16 % / 23 % / +2,06 | +17 % / 21 % / +1,62 | +18 % / 22 % / +1,74 | +3 % / 21 % / +0,26 |
| DOGE | +32 % / 8 % / +3,71 | +63 % / 20 % / +10,02 | **+77 % / 12 % / +10,69** | +6 % / 11 % / +0,48 |
| SOL | +20 % / 27 % / +2,41 | +28 % / 21 % / +2,35 | +28 % / 24 % / +2,43 | +24 % / 19 % / +1,82 |
| BNB | +18 % / 17 % / +3,36 | +27 % / 19 % / +4,49 | +24 % / 17 % / +4,62 | −1 % / 24 % / +0,01 |

Na veľkých trhoch je F/G takmer rovné S — rozdiel robia **malé trhy**, kde skorý výstup
zabíja trend. Výnimka je DOGE, kde F/G výrazne pomohli (trend mal veľa pullbackov na SMA50).

## Diagnostika: prečo to vyzerá inak na grafe (`flip_diag.py`)

Alexov postreh: *„na 1D grafe cena po crosse zostane nad SMA50 až do opačného crossu"*.

Z 1 062 uzavretých obchodov (236 flip / 826 SL):

```
počas obchodu aspoň raz close za SMA50:   520  (49 %)
z 236 flip obchodov:
   close za SMA50 skôr než flip:          218  (92 %)
   ostalo nad SMA50 až do flipu:           18  (8 %)
```

**Čiže vizuálne má Alex skoro pravdu, ale pravidlo funguje inak:** ten prvý close za SMA50
je **mediánovo len 0,05 % za SMA50** (Ø 0,12 %); hlbšie než 0,5 % bolo len **39 z 218**.
Je to mikroskopický close, ktorý na grafe vyzerá, že cena „ostala nad SMA50" — ale pravidlo
„close za SMA50" naň tvrdo chytí.

Čo to spraví:

```
výstup by prišiel v priemere o 10 dní skôr (medián 48 dní vs 58 dní do flipu)
z 218 takých obchodov: 116 už bolo nad +3R, 30 nad +10R   ← presne tie, čo nesú zisk
Ø strata 0,45 R na obchod (medián −0,05 R) → zráža to pár veľkých winnerov
```

## Ďalšie varianty (mäkšie prahy)

| Var | Pravidlo | Obch | Ø R | ročne | pokles | +trhov |
|---|---|---|---|---|---|---|
| S | flip (manuál) | 1 070 | +0,51 | +3,6 % | 22,1 % | 56 % |
| V1 | prvý close za SMA50 | 1 293 | +0,04 | −0,6 % | 21,5 % | 47 % |
| **V2** | **dva po sebe closes za SMA50** | 1 273 | +0,27 | +2,0 % | 22,0 % | **59 %** |
| V3 | close aspoň 1 % za SMA50 | 1 286 | +0,05 | −0,5 % | 21,7 % | 44 % |

V2 (potvrdený výstup) je najlepšia z včasných verzií a dokonca má viac kladných trhov
(59 %) než flip — ale výnos je stále nižší (+2,0 % vs +3,6 %). V3 (hĺbka 1 %) nepomohla.

## Diagnostika EMA20 (Alex: „cena skôr spadne pod EMA20 ako pod SMA50")

Platí — z 220 obchodov, kde obe čiari zavreli, **EMA20 zavrelo skôr v 210 prípadoch (95 %)**.

```
z 236 flip obchodov:  close za EMA20 skôr než flip:  220  (93 %)
                      ostalo nad EMA20 až do flipu:    16  (7 %)   ← bežci
medián R pri EMA20 výstupe:      +2,97   (Ø +4,65)
medián R, ktorý dal flip potom:  +3,60   (Ø +8,76)
Ø strata na obchod:              +4,11 R
pri EMA20 už > 3R: 108   a > 10R: 17
medián dní do EMA20 vs do flipu: 27 vs 58     ← výstup v polovici trendu
hĺbka za EMA20 pri tom close:     medián 0,08 %   (zase mikroskopické)
```

Čiže EMA20 je presne to, čo Alex vidí: **najskoršie varovanie** — a zároveň **najdrahší výstup**.
Nechá na stole Ø 4,11 R (oproti 0,45 R pri SMA50), lebo vystúpi v polovici držby.

Záver poradia: **čím bližšie je čiara k cene, tým viac systému vezme.**
`EMA20 (Ø +0,16 / +1,0 %)` < `SMA50 (Ø +0,04 / −0,6 %)` ≈ `prvé close za SMA50` < `flip (Ø +0,51 / +3,6 %)`.
Jediná výhoda skorých výstupov: pokles 17,9 % (EMA20) namiesto 22,1 % (flip).

## OPRAVA (2026-09-16, večer): výstup × vstup — čistý faktoriál

Pri ETH 2026 sa ukázalo, že predošlé baseliny neboli jednotné: verné čítanie manuálu je
**na opačný cross pozíciu obrátiť** (zavrieť + otvoriť novú), čo „S" nerobil. Premerané
znova všetko naraz (`exports/scripts/flip_exit2.py`, 34 trhov):

| Výstup / vstup | Obch | Ø R | t | ročne | pokles | výn/riz | +trhov | najväčší |
|---|---|---|---|---|---|---|---|---|
| flip / strict | 1 070 | +0,51 | 0,56 | +3,6 % | 22,1 % | 0,14 | 56 % | 16,1 R |
| **flip / REVERSE (manuál)** | 1 280 | +0,54 | 0,65 | **+4,6 %** | 23,8 % | 0,14 | **59 %** | 18,4 R |
| flip / loose (publikované čísla) | 3 328 | +0,55 | 1,01 | +9,6 % | 41,0 % | 0,20 | 65 % | 39,4 R |
| sma50 / strict | 1 293 | +0,04 | 0,13 | −0,6 % | 21,5 % | −0,02 | 47 % | 13,2 R |
| 1R+ / strict | 1 249 | +0,13 | 0,30 | +0,6 % | 21,8 % | 0,02 | 53 % | 13,2 R |
| ema20 / strict | 1 297 | +0,16 | 0,29 | +1,0 % | **17,9 %** | 0,08 | 53 % | 8,1 R |

**Závery sa nemenia** (skoré výstupy sú hlboko pod flipom), len sa spresňujú:
- verný manuál (obrat na flipe) je o kúsok lepší než „čakať na ďalší cross": +4,6 % vs +3,6 %,
  59 % vs 56 % kladných trhov, pri takmer rovnakom poklese,
- „loose" režim (vstup hneď keď som flat, tak počítali publikované čísla) dáva +9,6 %,
  ale s poklesom 41 % a 2,6× viac obchodov — je to iný, agresívnejší systém,
- u výstupu je úplne jedno, či sa po flipe obracia (sma50/ema20: +0,04 vs +0,04, +0,16 vs +0,16).

## Poznámky k spoľahlivosti

- Absolútne čísla medzi behmi mierne kolíšu: posledná (dnešná) denná sviečka sa ešte
  formuje a univerzum TOP 40 sa refetcheuje. Porovnávaj **v rámci jedného behu**.
- Median t = 0,56 (S) → štatisticky nepreukázané; rozdiely F/G/X vs S sú v tom istom pásme.
- Zmena pravidla výstupu je presne to, čo sa v testoch ukazuje ako najcitlivejšie:
  4 rôzne ochranné mechanizmy (16. 9. ráno) + 3 skoré výstupy (teraz) — **žiaden neporazil základ.**
