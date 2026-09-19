# Výskum: automatická detekcia S/R zón (2026-09-12)

**Cieľ:** stroj má sám nájsť zóny tak, ako ich kreslí Alex.
**Testovacia sada:** 6 grafov (5 historických + aktuálny) × ~2 zóny = 10 referenčných zón.
**Metrika:** *krytie* = aká časť Alexovej zóny je pokrytá strojovou (0–100 %).
Dve varianty: **najbližšia** (realistická – zóna pod/nad cenou) a **najlepšia** (optimistická – najlepšia z kandidátov).

## Výsledky

| Prístup | Ø najbližšia | Ø najlepšia | aktuálny graf |
|---|---|---|---|
| Swing clustering, cluster **0,5 %** (prvý pokus) | 14 % | 45 % | 13 % |
| Swing clustering, cluster **2,0 %** (oprava) | 45 % | 58 % | 50 % |
| + filter manuál 5.4 (zmena štruktúry) | 0–? | — | — (zhoršilo) |
| ZigZag 6 %, cluster 1,5 %, min 2 dotyky | **46 %** | **73 %** | 50 % |
| Čas-na-cene (objemový profil) | 0 % | 0 % | 0 % |

## Kľúčové zistenia

1. **Cluster threshold bol nastavený zle.** Alexove zóny sú ~2 % široké; clustering
   na 0,5 % rozbil jednu zónu na päť malých. Oprava zdvihla zhodu **14 % → 45 %**.
   → Potvrdzuje pravidlo **Z1** (šírka zóny ~2 %) aj pre stroj.

2. **ZigZag (percentuálny obrat) je lepší než fractal** — 73 % najlepšia zhoda.
   Potvrdzuje hypotézu, že **človek vidí swingy ako ZigZag, nie ako fractal**.

3. **Úzke hrdlo je SELEKCIA, nie detekcia.**
   „Najlepšia" zhoda 73 % znamená, že správna zóna je **skoro vždy medzi kandidátmi** —
   problém je vybrať tú pravú. Alex totiž nevyberá podľa počtu dotykov, ale podľa
   **kontextu** (čo je relevantné pre cenu teraz).

4. **Nepodarilo sa reprodukovať ľudské videnie zón** na úrovni použiteľnej pre
   backtest (46 % pri realistickej metrike).

## Poučenie o metodike

- Ladenie na 8–10 referenčných zónach **je overfitting** — presne to, pred čím
  sme varovali pri XGBooste. Ďalšie ladenie bez nových dát nemá zmysel.
- Pre seriózny výsledok treba **viac referenčných zón** (Alex nakreslí 30–50)
  a **oddelenú testovaciu sadu**, na ktorej sa neladí.

## Možné ďalšie smery

1. **Skórovanie namiesto filtrovania:** každú zónu obodovať (sila reakcie,
   zmena štruktúry podľa manuálu 5.4, recentnosť, vzdialenosť od ceny)
   a vybrať podľa skóre — namiesto pevných pravidiel.
2. **ZigZag + kontext ceny:** kombinovať ZigZag swingy s váhou podľa blízkosti ceny.
3. **Semi-automatický backtest:** Alex označí zóny, stroj odsimuluje checklist.
   (Navrhnuté, Alex súhlasil s prístupom „C".)

## Súbory

- `exports/scripts/zones_auto3.py` — detektor v3 (role reversal)
- `exports/scripts/validacia_grafy.py` — generátor validačných grafov
- `exports/scripts/validacia_eval.py` — vyhodnotenie
- `exports/scripts/eval_designs.py`, `eval_grid.py`, `eval_grid2.py`, `eval_grid3.py` — experimenty
- `exports/validacia/alex_zony.json` — referenčné zóny (6 grafov)
