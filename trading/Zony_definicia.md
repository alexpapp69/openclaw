# Definícia zón — ako ich číta Alex (2026-09-13)

Vzniká z dlhého rozhovoru. Toto je **presná, spočítateľná** definícia, overená na ETH.

## Kotva

```
1D graf → nájdi ATH (najvyšší bod)
       → nájdi LL  (najnižší bod po ATH)
```

## ✅ REZISTENCIA (potvrdené)

```
1. Zober OPEN a CLOSE každej sviečky  (NIE knôty!)
2. Nájdi cenu, ktorá je OPEN alebo CLOSE aspoň 3 sviečok
   (tolerancia 0,05 % — čiže takmer presne rovnaká)
3. Zóna = od tej hladiny NAHOR po DRUHÉ najvyššie HIGH
   z tých sviečok
```

**Prečo telá a nie knôty** (Alex): na hladine sa striedajú býčie a medvedie sviečky,
takže knôty idú rôzne — ale **telo (open/close) sedí.**

**Prečo až po high** (Alex): hladina je miesto zhody tiel; knôty ukazujú, kam až cena dosiahla.

**Prečo druhé najvyššie high** (Alex): jedna špička by zónu roztiahla do nezmyselnej šírky.

### Príklad od Alexa
```
sviečka 1:  O 1000 → C 1200
sviečka 2:  O 1200 → C 1090
sviečka 3:  O 1050 → C 1200
                   ↑
        spoločná hodnota = 1200  →  spodok zóny
        najvyššie high z tých troch  →  vrch zóny
```

### Overenie na ETH
Alexova reálna zóna: **2 365 – 2 465**
Stroj (rovnaká definícia, TOL 0,05 %): **2 374 – 2 460** → rozdiel **9 a 5 dolárov** ✅

## ⏳ SUPPORT (ešte nedefinované)

Alex: *„Chyba je, že nerozlišujeme medzi support a rezistenciou. Teraz sme definovali
rezistenciu."*

→ Support má **vlastnú** definíciu, ktorú ešte treba doplniť.
Pravdepodobne zrkadlo (hladina → druhé najnižšie low), ale **nie je potvrdené** —
Alex výslovne hovorí, že support a rezistencia sa musia rozlišovať.

## Čo ešte chýba doupravovať

- **Výber:** definícia nájde veľa hladín (v pásme 2 300–2 500 ich bolo 38).
  Chýba pravidlo, ktorá z nich je „tá zóna".
- **Šírka:** niektoré zóny vyšli 10–22 % — treba limit alebo dodatočné kritérium.
- **Support vs rezistencia:** nie je to len poloha voči cene, ale aj iná konštrukcia.

## Súbory
- `exports/scripts/eth_zony4.py` — implementácia rezistencie (finálna verzia)
- `exports/eth-zony-final.png` — graf s výsledkom
