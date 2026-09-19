# FLIP na ETHUSDT — rok 2026 (2026-09-16)

Pravidlá manuálu v1.1: EMA20/SMA50 cross na 1D, vstup na čerstvý cross, SL pod HL / nad LH
(1,5–6 %), výstup len pri opačnom flipe alebo SL, riziko 2 %.
Skript: `exports/scripts/flip_eth_2026.py` · dáta: Binance 1D (posledná sviečka 16. 9., ešte sa formuje)

## Uzavreté obchody 2026

| # | Vstup | Smer | Vstup cena | SL cena | SL % | Výstup | Výstup cena | Dôvod | R | Dní |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 2026-01-03 | LONG | 3 127,11 | 2 939,48 | 6,0 % | 2026-01-20 | 2 939,88 | SL | −1,00 | 17 |
| 2 | 2026-01-25 | SHORT | 2 816,89 | 2 985,90 | 6,0 % | 2026-01-27 | 3 026,77 | SL | −1,00 | 2 |
| 3 | 2026-03-18 | LONG | 2 203,39 | 2 071,19 | 6,0 % | 2026-03-21 | 2 084,87 | SL | −1,00 | 3 |
| 4 | 2026-05-18 | SHORT | 2 130,08 | 2 257,88 | 6,0 % | 2026-07-14 | 1 891,87 | flip | **+1,86** | 57 |
| 5 | 2026-07-14 | LONG | 1 891,87 | 1 778,36 | 6,0 % | *otvorená* | 2 393,50 | — | *+4,42* | 64 |

Všetky ceny = **denný close** (vstup na close dňa s prechodom, výstup cena je close dňa,
kedy sa aktivoval SL alebo flip). SL výstupy sa počítajú ako presné −1R (fill na SL cene).

**Poznámka:** všetkých 5 obchodov malo štrukturálny SL ďalej než 6 % → všade sa použil
**strop 6 %** (dĺžka SL 187,63 / 169,01 / 132,20 / 127,80 / 113,51 USDT). Pri riziku 2 %
účtu to znamená, že veľkosť pozície je vždy `riziko ÷ 0,06` — pri 10 000 USDT účte
**3 333 USDT na obchod** (1,07 / 1,18 / 1,51 / 1,57 / 1,76 ETH).

```
uzavreté:  4   ·   ziskové 1 (25 %)   ·   celkom −1,14 R   ·   Ø −0,28 R
účet od 1.1.2026 (2 % riziko, zložené): 100 → 97,4  (−2,6 %)   ·   najväčší pokles 6,0 %
LONG 2 obchody (−2,00 R)  ·  SHORT 2 obchody (+0,86 R)
```

## Otvorená pozícia (verné manuálu — flip sa obráti)

```
2026-07-14   LONG   vstup 1 891,9   SL 1 778,4 (6,0 %)   držaná 64 dní   teraz +4,42 R
```

Ak by sa zavrela dnes, rok by bol **+3,28 R ≈ +6,0 %** na účte (z toho 4 uzavreté obchody −1,14 R).
**Pozor:** podľa konzervatívnejšieho čítania (po flipe sa neobracia, čaká sa na ďalší cross)
by táto pozícia neexistovala a rok by ostal na −2,6 %.

## Stav teraz

```
ETH close 2 393,5   ·   EMA20 = 2 431,1   ·   SMA50 = 2 217,8   →   long režim
```

## Všetky prechody EMA20/SMA50 v roku 2026 (kontrola počtu obchodov)

Alex na grafe napočítal 9 obchodov. Preverené na 4 zdrojoch dát — **všade rovnakých 5 prechodov**:

| Zdroj | Počet prechodov 2026 | Dátumy |
|---|---|---|
| Binance spot ETHUSDT | 5 | 3. 1. ↑ · 25. 1. ↓ · 18. 3. ↑ · 18. 5. ↓ · 14. 7. ↑ |
| Binance perp ETHUSDT | 5 | rovnaké |
| Bybit spot ETHUSDT | 5 | rovnaké |
| Bybit linear ETHUSDT (perp) | 5 | rovnaké |

**Vysvetlenie čísla 9:** na grafe je 5 vstupov + 4 výstupy = **9 značiek**:

```
1)  3.1.  LONG  vstup
2) 20.1.  SL výstup
3) 25.1.  SHORT vstup
4) 27.1.  SL výstup
5) 18.3.  LONG  vstup
6) 21.3.  SL výstup
7) 18.5.  SHORT vstup
8) 14.7.  flip výstup
9) 14.7.  LONG  vstup (obrat) — stále otvorená
```

Čiže 5 pozícií (4 uzavreté + 1 otvorená), 9 udalostí. Ak Alexových 9 sú **vstupy**,
tak je v grafe iný indikátor (iné dĺžky MA) a treba porovnať dátumy.

## Poznámky

- **4 obchody za 9 mesiacov** je malá vzorka — z toho sa nedá vyvodzovať nič o systéme.
- Úspešnosť 25 % je presne to, čo manuál hovorí („prehráš 3–4 z 5") — a je to vidieť na prvých troch.
- Rok 2026 je zatiaľ **bez veľkého trendu na ETH** — tri SL boli rýchle (2–17 dní), jediný flip
  držal 57 dní a dal +1,86 R. Celý výsledok roka tak nesie jedna otvorená pozícia.
- Celá história ETH (2017–2026): 61 obchodov, +107 R (vo verzii s obratom na flipe).
