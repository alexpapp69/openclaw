# Checklist 1:1 — doslovný prevod do kódu

*Toto NIE JE interpretácia. Toto je tvoj „11. Trading checklist – long"
preložený bod za bodom na to, čo vie stroj overiť. Nič nepridávam, nič neubúdam.*

---

## 1D graf

| # | Tvoj text (doslovne) | Ako to stroj overí |
|---|---|---|
| **1** | *„Identifikujem významné S/R zóny a určím, kde sa cena nachádza voči nim."* | `zones = detect_zones(1D, sirka≈2%, reakcie≥2)` → `poloha_ceny = nad / v / pod` |
| **2** | *„Vyhodnotím 1D Market Structure a určím, či došlo k zmene štruktúry."* | `swings = fractal(1D, 5)` → `HH/HL` vs `LH/LL` → `kontrola = kupujuci/predavajuci/range` |
| **3** | *„Pri bearish štruktúre čakám na prerazenie posledného významného High a zatvorenie ceny nad touto úrovňou."* | `close_1D > posledne_vyznamne_High` **a** `telo_sviecky ≥ 60 %` |
| **4** | *„Po potvrdení 1D scenára prechádzam na 4H."* | 🚦 `if not potvrdeny_1D_scenar: return CEKAJ` |

## 4H graf

| # | Tvoj text (doslovne) | Ako to stroj overí |
|---|---|---|
| **5** | *„Skontrolujem štruktúru od posledného 1D Low."* | `start = index(posledny_1D_swing_Low)` — ✅ **Alex: fractal 5 na 1D** |
| **6** | *„Hľadám bullish štruktúru HH + HL."* | `posledne_2_highs su HH` **a** `posledne_2_lows su HL` |
| **7** | *„Overím súlad 4H s 1D."* | `smer_4H == smer_1D` (bullish == bullish) |
| **8** | *„Ak je 4H v súlade s 1D, prechádzam na 1H."* | 🚦 `if not sulad: return CEKAJ` |

## 1H graf

| # | Tvoj text (doslovne) | Ako to stroj overí |
|---|---|---|
| **9** | *„Určím posledné High, Low a aktuálnu cenu."* | `swings = fractal(1H, 5)` → `posledne_High`, `posledne_Low` |
| **10** | *„Čakám na prerazenie a uzavretie nad posledným High."* | `close_1H > posledne_High_1H` |
| **11** | *„Čakám na korekciu a retest prerazenej úrovne, ktorá sa môže stať supportom."* | `cena_vstupi_do_zony(prerazena_uroven)` ← Alex: „cena musí vstúpiť do zóny" |
| **12** | *„Pri odraze hľadám potvrdzujúce Price Action, ideálne sviečku s dlhým spodným knôtom."* | `lower_wick_ratio` — ✅ **Alex: BONUS** (nie tvrdá brána) |
| **13** | *„Určím Stop Loss pod relevantným HL s rezervou podľa štruktúry a likvidity."* | `SL = posledne_relevantne_HL − rezerva(struktura, likvidita)` |
| **14** | *„Skontrolujem RRR minimálne 1:2."* | 🚦 `if RRR < 2: return NEOBCHODUJ` |
| **15** | *„Vypočítam veľkosť pozície podľa maximálneho rizika a vzdialenosti SL."* | `size = riziko(50 €) / vzdialenost_SL` |

## Manažment (kap. 8)

| Krok | Tvoj text | Ako to stroj overí |
|---|---|---|
| M1 | *„Ak cena dosiahne významnú 4H úroveň a obchod dosahuje min. RRR 1:1, uzavriem 50 % pozície."* | `if cena >= 4H_uroven and RRR >= 1: close_50_percent()` |
| M2 | *„Po dosiahnutí TP1 Stop Loss zvyšnej pozície posuniem na úroveň TP1."* | `SL = entry` (break even) |
| M3 | *„Po dosiahnutí TP1 budem SL posúvať pod každé nové relevantné 1H HL."* | `trailing: SL = HL − rezerva` |
| M4 | *„Za relevantné Higher Low považujem také HL, po ktorom cena vytvorí nové Higher High."* | `relevantne_HL = HL[i] if exists HH po nom` |

---

## Čo z tohto vyplýva pre kód

```
for kazdu 1D sviecku:
    if nie je potvrdeny 1D scenar:  continue        # body 1-4
    for kazdu 4H sviecku:
        if nie je sulad s 1D:       continue        # body 5-8
        for kazdu 1H sviecku:
            if prejde body 9-13:
                if RRR >= 2:        ZAZNAMENAJ OBCHOD
```

**Každý bod je jedna funkcia. Každá funkcia vracia true/false.** To je celé.

---

## Čo ešte potrebujem dosadiť (1 číslo)

- **Bod 13** — *„rezerva podľa štruktúry a likvidity"*. Ako hlboko pod HL ide SL?
  (pevné %, ATR, pod posledný knôt?)

### ✅ Potvrdené
- **Bod 5** — „posledný 1D Low" = swing low, **fractal 5 na 1D**
- **Bod 12** — dlhý spodný knôt je **bonus**, nie tvrdá podmienka
- **Bod 14** — RRR ≥ 1:2 (manuál)

## Poznámka

Sekcia **9 chýba aj v origináli manuálu** (ide 8 → 10). Ak tam niečo bolo,
patrí to doplniť.
