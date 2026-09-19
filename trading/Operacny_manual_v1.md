# OPERAČNÝ MANUÁL v1.2

*Systém: „EMA flip" · postavený 2026-09-15 z tvojho indikátora a tvojho manuálu*

> **Účel:** aby si vedel presne, čo urobiť — bez rozmýšľania, bez pocitov,
> aj keď je hlava unavená a trh ide proti tebe.

---

## 1. ČO TO JE

```
Vstup:   EMA 20 prekročí SMA 50 na dennom grafe
SL:      pod posledné Higher Low (long) / nad posledné Lower High (short)
Výstup:  keď sa kríž otočí (opačný flip), alebo keď ťa vyhodí SL
```

**Žiadny fixný Take Profit.** Necháváš zisk bežať, kým sa trend neotočí.

---

## 2. NA ČOM TO OBCHODUJEŠ

| | |
|---|---|
| **Timeframe** | 1D (denný graf) |
| **Trhy** | BTC, ETH, BNB, SOL, DOGE *(testované: 5 trhov)* |
| **Nástroj** | Future, **max 5× páka** |
| **Poplatky/slippage** | rátaj ~0,30 % na obchod (round trip) |

⚠️ **NEobchoduj:** XRP, LINK *(v testoch záporné so 76–84 % poklesom)*
⚠️ **NEobchoduj:** KAS *(test 16. 9.: záporný pri každom strope SL, −2,2 až −13,1 %/rok; história len 2,7 r.)*
⚠️ **NEobchoduj:** stablecoiny, zlato, eurové páry *(nemajú čo merať)*

---

## 3. VSTUP — presný postup

**Kontroluj raz denne, po zatvorení dennej sviečky (napr. 01:00 tvojho času).**

```
KROK 1:  Je EMA 20 NAD SMA 50?   →  hľadám LONG
         Je EMA 20 POD SMA 50?   →  hľadám SHORT

KROK 2:  Prekročila práve dnes?  (včera bola na druhej strane)
         →  AK ÁNO: mám signál
         →  AK NIE: nič nerobím

KROK 3:  Nájdi posledné Higher Low (long) / Lower High (short)
         = posledný bod, kde sa cena otočila (3 sviečky na každej strane)

KROK 4:  Vypočítaj SL:
         LONG:  SL = to HL, ale NIE bližšie než 1,5 % a NIE ďalej než 8 %
         SHORT: SL = to LH, ale NIE bližšie než 1,5 % a NIE ďalej než 8 %

KROK 5:  Skontroluj CIEĽ — najbližšia logická prekážka (High/Low) musí dať 2R:
         LONG:   cieľ ≥ vstup + 2 × vzdialenosť SL
         SHORT:  cieľ ≤ vstup − 2 × vzdialenosť SL
         →  AK NEDÁ: tento signál preskoč

KROK 6:  Vypočítaj veľkosť pozície (viď bod 5)

KROK 7:  Vstup na close tej sviečky. Zapíš do denníka.
```

**Ak sa nedá nájsť HL/LH → tento signál preskoč.**

---

## 4. VÝSTUP — presný postup

```
A) SL zasiahnutý        →  von, strata −1 R, zapíš
B) KRÍŽ SA OTOČIL       →  von, zapíš výsledok v R
C) NIČ Z TOHO           →  držím ďalej. Nič nerobím.
```

**Nikdy nevystupuj „len tak".** Dôvod na výstup sú len A alebo B.

---

## 5. KOĽKO RISKOVAŤ — najdôležitejšia časť

**Fixné je RIZIKO. Vzdialenosť SL určuje trh, nie percento.**

```
RIZIKO NA OBCHOD = 2 % AKTUÁLNEHO ZÚSTATKU ÚČTU
```

```
VZOREC (vždy z konkrétnych cien):

  vzdialenosť SL (USDT)  = |vstup − SL|
  veľkosť pozície (kusy) = riziko (USDT) ÷ vzdialenosť SL
  veľkosť pozície (USDT) = kusy × vstup
```

**Príklad (účet 10 000 USDT → riziko 200 USDT), ETH:**
```
vstup 1800, logický SL 1702  →  vzdialenosť = 98 USDT (5,4 %)

  pozícia  = 200 / 98      = 2,04 ETH
  notional = 2,04 × 1800   = 3 673 USDT  (0,37× účet)
  strata pri SL = 2,04 × 98 = 200 USDT   ✓ presne riziko
```

**Prečo NIE percento:** keby si pozíciu počítal z „3 %“, vyšlo by 6 667 USDT
(3,70 ETH) — pri tvojom SL 98 USDT by strata bola **363 USDT (3,6 % účtu)**,
nie 200. Percento musí ísť z ceny, nie naopak.

| Vzdialenosť SL | v % z ceny | Pozícia (ETH @1800) | Notional | Strata pri SL |
|---|---|---|---|---|
| 27 USDT | 1,5 % | 7,41 ETH | 13 333 USDT | 200 |
| 54 USDT | 3,0 % | 3,70 ETH | 6 667 USDT | 200 |
| 98 USDT | 5,4 % | 2,04 ETH | 3 673 USDT | 200 |

→ **Čím ďalej SL, tým menšia pozícia. Strata je vždy 200 USDT.**

**Hranice vzdialenosti SL (z bodu 3):**
```
min 1,5 %   → bližší SL = väčšia pozícia (pri 1,5 % je to 1,33× účet)
max 8 %     → NIE kvôli riziku (to je stále 2 %), ale kvôli RRR:
              pri 8 % SL musí cieľ dať aspoň 16 % pohyb, aby obchod dal 2R
              → preto KROK 5: bez cieľa na 2R sa neobchoduje

  (prečo 8 % a nie 5–6 %: premerané na BTC/ETH/SOL/DOGE 16. 9. 2026 —
   strop 8 % dal najlepší priemer aj medián, 6 % najhorší;
   zdroj: `Strop_SL_5trhov.md`)
```

**Kontrola pred vstupom:**
```
notional ≤ 4× účet    (poistka pre prípad veľmi blízkeho SL)
```

---

## 6. ČO NEROBIŤ — zoznam, ktorý ťa udrží v hre

| ❌ | Nikdy |
|---|---|
| 1 | Neposúvaj SL bližšie k cene „aby to vydržalo" |
| 2 | Nezvyšuj riziko po strate (žiadne „dobijanie") |
| 3 | Neobchoduj signál, ktorý si zmeškal (nevstupuj „dopočítaním") |
| 4 | Nepridávaj do stratovej pozície |
| 5 | Neobchoduj bez SL — ani raz |
| 6 | Neriaď sa tým, čo cítiš, ale tým, čo vidíš |
| 7 | Neobchoduj, keď si naštvaný alebo euforický |
| 8 | Neladí parametre po 3 stratách (to nie je systém, to je panika) |
| 9 | Nepoužívaj páku väčšiu, než zvládneš pri 50 % poklese |
| 10 | Neobchoduj trh, ktorý nie je na zozname v bode 2 |
| 11 | Nedávaj čiastočný výstup ani SL na break-even *(test 16. 9.: −14 %/rok, len 6 % trhov kladných)* |

**Po 5 stratách za sebou:** preruš na týždeň a **skontroluj, či si dodržal manuál.**
(Nie „či systém nefunguje" — ale „či som ho dodržal".)

---

## 7. ČO MÔŽEŠ ČAKAŤ — realisticky

Z testov na 5 trhoch, roky 2024–2025, realistické náklady:

```
Úspešnosť:      20–29 %   ← vyhráš len 1 z 4 až 5 obchodov!
Ø R:            +0,6 na obchod
Ročný výnos:    ~15–25 %  (na dobrých trhoch viac)
Max. pokles:    35–45 %   ← toto zažiješ, priprav sa
Obchodov ročne: ~20–30 na trh
```

### ⚠️ Toto je najdôležitejšie, čo si musíš zapamätať:

```
Prehráš 3–4 obchody z 5.  TO JE SPRÁVNE.
Celý zisk spraví 5–10 obchodov z 100.
Keby si im odrezal zisky skôr, nemáš NIČ.
```

### A úprimne — čo NIE JE overené
- **Strop SL 8 % je tvoje rozšírenie** — čísla vyššie sú z testov s pôvodným stropom 5 %
- **Na tvojich trhoch (BTC/ETH/SOL/DOGE) vyšlo 8 % najlepšie**: priemer +39,7 %/rok, medián +36,3 %, pokles 19,3 % (oproti +32,9 % / +21,8 % pri 6 %). Zdroj: `Strop_SL_5trhov.md`
- **Čísla hore sú z testovacej verzie, ktorá po SL vstupovala hneď znova** — nie z pravidiel tohto manuálu. Keď sa dodrží „po SL čakám na nový cross" (KROK 2), pokles padne z ~40 % na ~22 %, ale ročný výnos z ~11 % na ~6 % (pomer výnos/riziko rovnaký). Zdroj: `Ochrana_zisku_vysledky.md`
- Nie je štatisticky preukázané (t < 2 vo väčšine testov)
- 2 roky testu je krátka vzorka
- V medvedom trhu sa systém správa inak
- Minulé výsledky nie sú záruka

---

## 8. DENNÍK OBCHODOV — ako sa merať

Po každom obchode zapíš **týchto 7 vecí:**

| # | Pole | Príklad |
|---|---|---|
| 1 | Dátum vstupu | 2026-09-15 |
| 2 | Trh | BTCUSDT |
| 3 | Smer | LONG |
| 4 | Vstup / SL | 77 400 / 74 300 |
| 5 | Riskované USDT | 200 |
| 6 | Výsledok v R | +2,4 R |
| 7 | **Dodržal som pravidlá?** | ÁNO / NIE |

**A ten siedmy bod je najdôležitejší.** Po 50 obchodoch zistíš, čo ťa zráža:
```
Ak máš "NIE" vo viac než 20 % obchodov  →  problém je disciplína, nie systém
```

---

## 9. OČAKÁVANÝ VÝSLEDOK — ako vyzerá dobrý rok

```
Reálny priebeh účtu (ilustračne, 2 % riziko):

  mesiac 1:   −8 %     (5 obchodov, 4 straty)
  mesiac 2:   −4 %
  mesiac 3:  +22 %     (jeden veľký trend)
  mesiac 4:   −6 %
  mesiac 5:  +14 %
  ...
  za rok:    +20 %  pri poklese −38 %
```

**Tie dva-tri zlé mesiace sú normálne.** Práve vtedy väčšina ľudí systém opustí.

---

## 10. RUTINA — čo robiť kedy

| Kedy | Čo |
|---|---|
| **Denne (5 min)** | Po zatvorení 1D sviečky skontroluj 5 trhov. Je nový kríž? |
| **Pri signáli** | Prejdi kroky 1–7 v bode 3. Zapíš do denníka. |
| **Týždenne** | Skontroluj otvorené pozície — SL drží? |
| **Mesačne** | Spočítaj si výsledky z denníka. Dodržal si pravidlá? |
| **Po 50 obchodoch** | Vyhodnoť: systém, alebo disciplína? |

---

## 11. PRED PRVÝM OBCHODOM — kontrola

```
☐ Mám účet s max 5× pákou
☐ Viem, koľko je 2 % môjho účtu v USDT
☐ Mám otvorený denník
☐ Poznám zoznam trhov (bod 2)
☐ Prečítal som body 6 a 7 (čo NEROBIŤ a čo čakať)
☐ Viem, že prehrám 3–4 obchody z 5 — a je to správne
☐ Toto nie je môj hlavný príjem
```

**Ak nezaškrtneš posledné dva body, nezačínaj.**

---

*Manuál v1.2 · 2026-09-16 · postavený z `Trading_Manual_v1.0.md`, indikátora EMA/SMA
a testov v `EMA_cross_vysledky.md`. Overený na 40 trhoch, 10 štartoch, s poplatkami.*

*Zmeny v1.1: veľkosť pozície z reálnej vzdialenosti SL v USDT (bod 5);
strop SL 5 % → 6 % + povinná kontrola cieľa na 2R (KROK 5 v bode 3).*

*Zmeny v1.2: strop SL 6 % → **8 %** (test na BTC/ETH/SOL/DOGE ukázal 8 % ako najlepšie);
KAS pridaný na zoznam NEobchodovať (záporný pri každom strope);
postup výstupu spresnený — na opačný cross sa pozícia **obráti** (test: +4,6 %/rok, 59 % trhov kladných).*
