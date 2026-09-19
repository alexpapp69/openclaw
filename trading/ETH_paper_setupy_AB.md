# ETHUSD 1H paper trading — setupy A/B (engine `eth_paper.py`)

Stav: 2026-09-18. Účet 2,80 ETH · riziko 2 % (0,056 ETH) · páka 5× · coin-M (inverzný kontrakt).

## Pravidlá

**Setup A — odraz od podpory**
- 1H sviečka s low v zóne **2 425–2 435**, close späť v zóne, bullish reversal (engulfing / hammer).
- SL **2 418** (pod zónou), TP1 **2 483** (50 %), TP2 **2 544**.
- Filter: RRR ≥ 2 voči TP1.

**Setup B — prielom + retest** (do 18. 9. 2026 v engine chýbal)
- Čerstvý 1H close nad úrovňou z `LEVELS_UP = [2483, 2544, 2614, 2665]`
  (predtým aspoň `B_FRESH = 20` sviecok nesmelo zavrieť nad úrovňou → inak je to chop v range).
- Retest do 8 sviecok: low sa vráti do **0,3 %** nad úroveň, sviečka zavrie bullish a nad úrovňou.
- SL = low retestu − 0,2 %, ale nie bližšie než **0,5 %** od vstupu (inak sa pozícia nezmestí do účtu).
- TP1 = najbližší odpor nad úrovňou, TP2 = ďalší (pre 2 483 → 2 544 / 2 614). RRR ≥ 2.

**Spoločné:** jedna pozícia naraz · TP1 → zavrieť 50 % + SL na break even · TP2 → zvyšok · marža
max 90 % účtu (`MAX_MARGIN_PCT`) · hliadka skenuje posledných `LOOKBACK = 14` sviecok, signál
z poslednej zatvorenej sviečky otvára obchod, starší sa hlási ako **MISSED** (neotvára sa).

## Replay (`eth_paper_replay.py`, poplatky 0,06 %/strana)

| okno | filter B_FRESH | obchody | net R |
|---|---|---|---|
| 90 dní | 20 | 5× A + 1× B | +4,04 R (z toho +2,40 R otvorený) |
| 90 dní | 0 | 6× A + 6× B | −1,86 R |
| 360 dní | 20 | 7× A + 1× B | +2,79 R (z toho +2,40 R otvorený) |
| 360 dní | 0 | 7× A + 6× B | −3,11 R |

**Záver:** bez filtra B vyrába 5–6 signálov za rok na úrovni 2 483, z toho 5× SL (−1 R) — úroveň
bola vtedy v chop-e a „čerstvý prielom" bol šum. Filter B_FRESH tieto whipsawy odstráni, ale B
potom vystrelí len raz za rok. Miss 18. 9. 06:00–07:00 bol reálny B signál
(vstup 2 486,90, SL 2 474,47, TP1 2 544, RRR 4,59), ale v replay sa neotvoril, lebo pozíciu
držal A obchod z 17. 9. 11:00.

**Poznámka:** úrovne sú pevné konštanty — po prekonaní cenou ich treba pregenerovať (Alex: ručne).

## AKTUALIZÁCIA 18. 9. — úrovne sa prepočítavajú automaticky

`eth_levels.py` skladá z 1H dát 4H sviečky, hľadá fractal-3 swingy a zapisuje `paper_levels.json`
(rezistencie, nákupná zóna, SL). Engine ich číta pri každom behu hliadky → žiadne ručné prepisovanie.
TP = najbližší odpor, ktorý dá RRR ≥ 2.

**Replay s automatickými úrovňami (360 d):** 204 obchodov, **−82,90 R**, 41/204 ziskových
(bez B filtra 303 obchodov, −103,42 R). 90 d: 35 obchodov, −0,12 R.

→ Automatické úrovne nie sú problém ani riešenie; **stratégia ako celok je stratová** a na vine je
výstup „50 % na TP1 + SL na BE“. Ďalší krok: držať celú pozíciu, stopku posúvať za cenou.

## AKTUALIZÁCIA 18. 9. — nový výstup (bez delenia, stopka za cenou)

Pozícia sa nedelí, stopka sa posúva pod najnižší low posledných 3 sviečok (−0,15 %), koniec na TP2.
Logika je v jednej funkcii `manage(t, d, k)` — používa ju live aj replay.

**Sweep cez rok (360 dní):** žiadna stopka −76,4 R · 1 sviečka −47,4 R · 3 sviečky −77,6 R ·
6 sviečok −80,0 R · 12 sviečok −61,2 R · 24 sviečok −63,8 R (všetko mínus, najlepší variant sa
medzi oknami mení). → Problém nie je výstup, ale vstupy: príliš veľa obchodov (200–290 za rok),
~25 % ziskových. Ďalší krok: menej/väčšie úrovne (denné), trendový filter, alebo len signály bez obchodovania.
