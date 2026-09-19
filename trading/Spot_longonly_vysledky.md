# Spot / long-only portfólio (2026-09-16)

**Zadanie (Alex):** *„Rozdeľ 10 000 na tie coiny a vyskúšaj len spot — buy pri flipe EMA20
nad SMA50, sell pri opačnom flipe."*

Skript: `exports/scripts/spot_longonly.py` · poplatok 0,10 % na stranu · žiadny SL, žiadny
short, žiadna páka · spoločný začiatok 2020-08-11 (SOL má najkratšiu históriu).

## Výsledok (6,1 roka)

| Coin | 2 000 → | zisk | obchodov | vs držanie |
|---|---|---|---|---|
| BTC | 14 159 | +608 % | 53 | **+6,5 %** |
| ETH | 40 196 | +1 910 % | 45 | +219 % |
| BNB | 37 490 | +1 775 % | 47 | **−44 %** |
| SOL | 155 924 | +7 696 % | 45 | +165 % |
| DOGE | 385 797 | +19 190 % | 47 | +726 % |
| **SPOLU** | **633 567** | **+6 236 %** | 237 | — |

```
ročne (CAGR):               +97,5 %
najväčší pokles portfólia:  60,1 %
BUY & HOLD:                 198 390 USDT (+1 884 %, ročne +63,2 %, pokles 85,1 %)
čas v trhu:                 42–53 % dní (zvyšok v cashi)
```

## Rok po roku

| Rok | Portfólio | Zmena |
|---|---|---|
| 2020 (od 11. 8.) | 10 000 → 15 669 | +56,7 % |
| 2021 | 15 669 → 345 145 | **+2 103 %** |
| 2022 | 345 145 → 279 745 | −18,9 % |
| 2023 | 279 745 → 457 111 | +63,4 % |
| 2024 | 457 111 → 909 344 | +98,9 % |
| 2025 | 909 344 → 815 909 | −10,3 % |
| 2026 (do 16. 9.) | 815 909 → 633 567 | **−22,3 %** |

## Ako to čítať úprimne

- **Skoro celý zisk spravil rok 2021** (+2 103 %). Od konca 2021 do dnes je to
  345 145 → 633 567 = **+84 % za 4,6 roka (~+14 %/rok)**. To je realistickejšie číslo
  než tých +97 % ročne.
- **Vybrali sme víťazov.** BTC/ETH/BNB/SOL/DOGE sú mince, ktoré v tomto období prežili
  a vyrástli. Keby sme v 2020 zobrali aj XRP, LINK, EOS, výsledok by bol horší.
- **DOGE ťahá všetko** (+19 190 %). Bez DOGE by portfólio skončilo na ~247 000 (+2 370 %).
- **BNB stratilo proti držaniu** (−44 %) a BTC takmer nič neprinieslo (+6,5 %) — stratégia
  neporazila držanie na každom trhu, len na tých volatilných.
- Model je optimistický: signál aj vykonanie na **dennom close**, žiadne slippage,
  žiadne dane, žiadne výpadky.
- Pokles 60 % portfólia aj pri 50 % času v cashi — to sa nedá „prečkať" bez pevných nervov.

## Porovnanie so systémom so SL (long+short, 2 % riziko)

| | Spot long-only | Flip so SL (obrat, 2 % riziko) |
|---|---|---|
| Trhy | 5 | 5 (BTC/ETH/SOL/DOGE) |
| Ročne | +97,5 % (celé obdobie) / ~+14 % (od 2022) | +32,9 % medián |
| Pokles | 60,1 % | 21,3 % |
| Riziko na obchod | 100 % rukávu | 2 % účtu |

Hlavný rozdiel: spot verzia **nemá SL** — riziko nesie celý rukáv. Preto vyšší výnos,
ale aj vyšší pokles a horšie zvládnuteľná psychika.

---

# A keby si pridal SL 8 %? (2026-09-16)

Alex: *„A keby si pridal SL 8 %?"* → `exports/scripts/spot_longonly_sl.py`.

SL = ak cena spadne 8 % pod vstup, predaj; potom sa čaká na **ďalší čerstvý upcross**.

| | Na konci | Zisk | Ročne | Pokles | Nákupov | SL výstupov |
|---|---|---|---|---|---|---|
| **BEZ SL** | 633 567 | +6 236 % | +97,5 % | 60,1 % | 121 | 0 |
| **SO SL 8 %** | **822 915** | **+8 129 %** | **+106,1 %** | **53,0 %** | 121 | 57 |

**SL 8 % to zlepšilo** — vyšší výnos aj nižší pokles. Ale pozor, nie je to jednoznačné:

| Coin | BEZ SL | SO SL 8 % | Rozdiel |
|---|---|---|---|
| BTC | 14 159 | 18 879 | **+33 %** |
| ETH | 40 196 | 44 178 | +10 % |
| BNB | 37 490 | 15 239 | **−59 %** |
| SOL | 155 924 | 71 376 | **−54 %** |
| DOGE | 385 797 | 673 244 | **+75 %** |

**Dva trhy z piatich sa zhoršili** (BNB, SOL) — tam bol pokles o 8 % len dočasný výkyv a stop
vyhodil pozíciu z trendu. Na BTC, ETH a DOGE stop pomohol (reálne odvrátil hlbšie pády).

## Rok po roku

| Rok | BEZ SL | SO SL 8 % |
|---|---|---|
| 2020 (od 11. 8.) | +56,7 % | +64,8 % |
| 2021 | +2 102,7 % | +2 128,0 % |
| 2022 | −18,9 % | **−12,6 %** |
| 2023 | +63,4 % | **+9,9 %** |
| 2024 | +98,9 % | **+182,7 %** |
| 2025 | −10,3 % | −4,5 % |
| 2026 (do 16. 9.) | −22,3 % | **−13,5 %** |

SL pomáha presne v tých rokoch, ktoré bolia (2022, 2026) a v roku 2024 dalo výrazne viac.
Ale **2023 je oveľa horší** (+9,9 % vs +63,4 %) — po vyhodení čakáš na nový cross a zmeškáš časť rastu.

## Úprimne

- „Zlepšenie" je do veľkej miery zásluha DOGE (+75 %) — bez neho by výsledok bol o dosť bližšie.
  Pri 5 trhoch sa jeden extrémny trh preleje do celého portfólia.
- Zlepšil sa aj pokles (60,1 % → 53,0 %) a hlavne **bolestivé roky** — to má reálnu hodnotu
  pre psychiku, aj keby výnos bol rovnaký.
- Stále platí: 6 rokov, šťastný začiatok (2020), vybraní víťazi, model bez slippage a daní.

**Teraz:** so SL je 4 z 5 rukávov v pozícii, DOGE je vyhodený (v cashi).

---

# Skorší znovuvstup po SL — test (2026-09-16, „Skús ešte")

Alex: *„po SL sa nevracaj cez nový cross, ale hneď ako cena zavrie späť nad EMA20"*.
Skript: `exports/scripts/spot_longonly_sl2.py` (7 variantov).

| Variant | Na konci | Ročne | Pokles | Nákupov | SL výstupov |
|---|---|---|---|---|---|
| bez SL | 633 567 | +97,5 % | 60,1 % | 121 | 0 |
| **SL 8 % + nový cross** | **822 915** | **+106,1 %** | **53,0 %** | 121 | 57 |
| SL 8 % + EMA20 | 553 238 | +93,1 % | 63,8 % | 157 | 84 |
| SL 8 % + SMA50 | 493 632 | +89,6 % | 67,7 % | 169 | 90 |
| SL 10 % + nový cross | 741 406 | +102,6 % | 53,1 % | 121 | 47 |
| SL 10 % + EMA20 | 547 912 | +92,8 % | 70,1 % | 147 | 65 |
| SL 12 % + EMA20 | 643 641 | +98,0 % | 62,8 % | 135 | 44 |

## Verdikt: skorší znovuvstup je HORŠÍ

Rýchlejší návrat (EMA20/SMA50) **nepomohol ani v jednej kombinácii**:

- **viac nákupov** (157–169 vs 121) a **viac stopov** (84–90 vs 57) — chytá to whipsawy,
- **vyšší pokles** (63,8–70,1 % vs 53,0 %),
- **nižší výnos** (493–553 tis. vs 823 tis.).

Najdrahšie to zaplatí DOGE: 673 244 (cross) vs 263 199 (EMA20). Rok po roku je skorší vstup
lepší len v 2023 (+101 % vs +9,9 %), inde horší — hlavne v 2022 (−22,5 % vs −12,6 %).

**Záver: po SL sa vyplatí čakať na nový čerstvý cross.** Potvrdené — a je to najlepší
variant zo všetkých, čo sme dnes skúsili (822 915 USDT, +106,1 %/rok, pokles 53 %).

Chyba v prvom behu (opravená): po SL ostal rukáv „zamknutý" (armed=False) a už sa nevrátil —
dával nezmyselné číslo 227 785 s 16 nákupmi.

---

# Len roky 2024, 2025, 2026 (2026-09-16)

Alex: *„Daj len 2024, 2025 a 2026"* → `exports/scripts/spot_2024_2026.py`.
Štart 2024-01-01, 10 000 na 5 mincí (2 000 každá), poplatok 0,10 %/strana.

| Variant | Na konci | Spolu | 2024 | 2025 | 2026 YTD | Pokles | Nákupov | SL |
|---|---|---|---|---|---|---|---|---|
| bez SL | 16 425 | +64,2 % | +71,7 % | +6,6 % | −10,3 % | 43,4 % | 56 | 0 |
| **SL 8 %** | **19 993** | **+99,9 %** | +93,6 % | +10,3 % | **−6,3 %** | **28,6 %** | 56 | 30 |
| SL 10 % | 19 101 | +91,0 % | +89,4 % | +12,6 % | −10,5 % | 36,8 % | 56 | 25 |
| BUY & HOLD | 13 489 | +34,9 % | **+118,5 %** | **−23,0 %** | −19,8 % | **62,2 %** | — | — |

Ročne (2,7 roka): SL 8 % **+29,2 %** · bez SL +20,1 % · držanie +11,7 %

## Per coin (2 000 → na konci, začiatok 2024)

| | BTC | ETH | BNB | SOL | DOGE |
|---|---|---|---|---|---|
| bez SL | 3 084 | 4 870 | 2 255 | 1 415 | 4 801 |
| SL 8 % | 3 325 | 4 937 | 2 651 | 1 241 | **7 840** |
| SL 10 % | 3 095 | 4 423 | 2 427 | 1 426 | 7 729 |
| držanie | **3 427** | 2 033 | **4 537** | **1 769** | 1 723 |

## Ako to čítať

- **V 2024 držanie vyhralo** (+118,5 % vs +93,6 %) — bull rok, kde sedieť a nič nerobiť bolo najlepšie.
- **V 2025 a 2026 systém vyhral** — držanie −23,0 % a −19,8 %, systém +10,3 % a −6,3 %.
  Presne o tom je ten systém: v zlých rokoch ťa dostane z trhu.
- **SL 8 % pomáha aj tu** — nižší pokles (28,6 % vs 43,4 %) a vyšší výnos (+99,9 % vs +64,2 %).
- **Per coin sa to nemieša rovnako:** systém vyhral na ETH (4 937 vs 2 033) a DOGE (7 840 vs 1 723),
  ale **prehral na BNB (2 651 vs 4 537) a SOL (1 241 vs 1 769)**. Na BTC je to remíza.
- **2026 je doteraz záporný vo všetkom** (−6 % až −20 %). To je realita, s ktorou treba rátať.

⚠️ 2,7 roka je krátka vzorka a január 2024 bol dobrý vstup. Nie je to dôkaz — je to indícia.
