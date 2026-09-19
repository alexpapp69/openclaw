# Trading Manual v1.0

*Spoločný projekt na vybudovanie vlastného obchodného systému.*
(Zdroj: `Trading_Manual_v1.0.pages` na Macu, Alex. Extrahované 2026-09-10.)

## 1. Filozofia

Obchodujeme proces, nie výsledok. Každé pravidlo musí mať dôvod. Pravidlá meníme iba podľa dát. Do obchodného systému zapisujeme iba pravidlá, ktoré vieme objektívne rozpoznať alebo otestovať. Nepostavíme systém na domnienkach o tom, čo robia veľkí hráči.

## 2. Trhy

BTC Perpetual · ETH Perpetual

## 3. Timeframy

- **1D** = Kontext
- **4H** = Zóna záujmu
- **1H** = Vstup

## 4. Market Structure

### 4.1 Definícia
Market Structure je spôsob, ako zistiť, ktorá strana (kupujúci, predávajúci alebo nikto) má momentálne kontrolu nad trhom.

### 4.2 Cieľ
Pred každou analýzou musím odpovedať na jedinú otázku: **Kto má momentálne kontrolu nad trhom?** Možné odpovede sú iba tri:
- Kupujúci
- Predávajúci
- Nikto (range)

### 4.3 Pravidlo č. 1
Pred určením Market Structure nehľadám: Support, Resistance, Vstup, Stop Loss, Take Profit. Najprv určím Market Structure. Až potom pokračujem.

### 4.4 Ako určujem market structure?
1. Otvorím 1D graf.
2. Pozriem, či cena vytvára HH a HL alebo LH a LL.
3. Ak áno, určím, kto má kontrolu nad trhom.
4. Ak nie, považujem trh za range, kým nedostanem dôkaz o opaku.

### 4.5 Trend
Trend je stav trhu, v ktorom kupujúci alebo predávajúci prevzali kontrolu.
Rastúci trend vzniká, keď sú kupujúci ochotní nakupovať za stále vyššie ceny.
Klesajúci trend vzniká, keď sú predávajúci ochotní predávať za stále nižšie ceny.
Na grafe sa to prejavuje vytváraním HH a HL (rastúci trend) alebo LH a LL (klesajúci trend).

### 4.6 Range
Range je stav trhu, keď ani kupujúci, ani predávajúci nemajú dostatočnú prevahu na vytvorenie nového trendu.
Kupujúci nie sú ochotní nakupovať za výrazne vyššie ceny a predávajúci nie sú ochotní predávať za výrazne nižšie ceny.
Na grafe sa to prejavuje pohybom ceny medzi supportom a rezistenciou bez vytvorenia nového trendu.

### 4.7 Najčastejšie chyby
**Chyba č. 1:** Nepovažuj každý silný pohyb za nový trend. Prečo? Pretože aj v rámci range môže cena spraviť veľmi silný pohyb bez toho, aby sa zmenila Market Structure.

### 4.8 Zhrnutie
Market Structure je stav trhu, ktorý nám ukazuje, kto určuje pravidlá hry. Môžu to byť kupujúci, predávajúci alebo nikto (range).

## 5. Support / Resistance

Support je cenová zóna, v ktorej kupujúci získavajú prevahu nad predávajúcimi a zastavujú pokles ceny.

### 5.1 Čo je S/R zóna
S/R zóna je cenová oblasť, na ktorej v minulosti došlo k výraznej reakcii trhu. V závislosti od aktuálneho vývoja môže táto zóna fungovať ako support alebo rezistencia.

### 5.2 Ako určujeme support
Support zakresľujeme ako **zónu, nie ako jednu čiaru**. Zónu určujeme podľa oblasti, z ktorej opakovane prichádza reakcia kupujúcich. Pri zakresľovaní berieme do úvahy telá sviečok aj knôty, pretože cena nereaguje na jednu presnú hodnotu, ale na cenovú oblasť.
Najvýznamnejšie supporty sú často zóny, ktoré predtým fungovali ako rezistencia a po prerazení zmenili svoju úlohu na support.

### 5.3 Významnosť S/R zóny (pracovná verzia)
S/R zóna je pre mňa významná vtedy, keď na nej trh v priebehu času viackrát reagoval. Počas času môže meniť svoju úlohu zo supportu na rezistenciu a naopak.

### 5.4 Významná reakcia trhu
Významná reakcia trhu je taká reakcia od S/R zóny, ktorá vedie ku **zmene Market Structure**. Takéto zóny považujeme za dôležitejšie než zóny, od ktorých sa cena iba krátkodobo odrazila.

## 6. Likvidita

Likvidita je cenová oblasť, pri ktorej očakávame zvýšenú aktivitu účastníkov trhu, pretože sa tam často nachádzajú stop-lossy alebo čakajúce objednávky.

### 6.1 Kde hľadáme likviditu
Likviditu najčastejšie hľadáme **nad významnými High a pod významnými Low**. Na oboch stranách trhu môže byť nahromadená likvidita. Úlohou tradera je určiť, ktorá z nich je vzhľadom na aktuálny kontext pravdepodobnejším cieľom ceny.

Likvidita sama o sebe **nie je vstupným signálom**. Je iba upozornením, že na trhu môže dochádzať k zmene rovnováhy medzi kupujúcimi a predávajúcimi.

## 7. Vstupy

1. Nad vstupom do obchodu začnem uvažovať až vtedy, keď mi 1D graf potvrdí, kto má kontrolu nad trhom.
2. Keď mi 1D graf potvrdí, kto má kontrolu nad trhom, prepnem sa na 4H graf, kde začnem hľadať obchodnú príležitosť.
3. Ak obchod nespĺňa podmienky môjho systému alebo neumožňuje dosiahnuť minimálne RRR 1:2, obchod neotvorím. Radšej vynechám obchod, než by som vstúpil do nekvalitného setupu.
4. Na 4H grafe hľadám súlad (confluence) signálov z 1D grafu.
5. Na 1H grafe hľadám najlepšie podmienky pre vstup do obchodu v súlade s 1D a 4H grafom.
6. Obchod otvorím až po uzavretí 1H sviečky nad posledným Higher High (pri longu), pričom predtým musí byť vytvorené Higher Low a musí existovať súlad s 1D a 4H grafom.

## 8. Riadenie obchodu

Pri long obchode umiestnim Stop Loss pod najnižší bod posledného relevantného HL na 1H grafe s rezervou určenou podľa konkrétnej štruktúry a likvidity. Ak takto umiestnený Stop Loss neumožní dosiahnuť minimálne RRR 1:2, obchod neotvorím.

Hlavný TP hľadám na 1D grafe, pričom beriem do úvahy aj významné úrovne zo 4H grafu. Ak cena dosiahne významnú 4H úroveň a obchod v tomto momente dosahuje minimálne RRR 1:1, uzavriem 50 % pozície.

Po dosiahnutí TP1 Stop Loss zvyšnej pozície posuniem na úroveň TP1.
Po dosiahnutí TP1 budem Stop Loss zostávajúcej pozície posúvať pod každé nové relevantné 1H Higher Low s rezervou podľa likvidity. Za relevantné Higher Low považujem také HL, po ktorom cena vytvorí nové Higher High.

## 10. Risk Management

1. Maximálne **1 % účtu** na obchod.
2. Veľkosť pozície určujeme podľa maximálneho rizika a vzdialenosti Stop Lossu:
   - Príklad: maximálne riziko = 50 €, vstup = 100 000 €, SL = 98 000 €, vzdialenosť SL = 2 000 €
   - `50 / 2 000 = 0,025 BTC`
3. Leverage nemení maximálne riziko obchodu. Veľkosť pozície určujem podľa povoleného rizika a vzdialenosti SL, nie podľa dostupnej marže alebo maximálnej pozície, ktorú mi umožňuje leverage.
4. Ak mám otvorený obchod na jednom trhu, ďalší obchod na tom istom trhu už neotváram, kým prvý obchod nie je uzavretý.
5. Ak mám otvorený obchod na jednom trhu, môžem otvoriť obchod na inom trhu. Každý samostatný obchod má maximálne riziko 50 €.
6. Po **5 stratových obchodoch za sebou** obchodovanie preruším a vykonám kontrolu.
7. Najprv skontrolujem, či som pri stratových obchodoch dodržal Trading Manual. Ak boli pravidlá dodržané, vyhodnotím obchody a hľadám spoločný problém alebo opakujúci sa vzorec.
8. Ak boli obchody vykonané podľa Trading Manualu a kontrola neodhalí spoločný technický problém, sériu strát považujem za možnú súčasť systému a nemením pravidlá iba na základe tejto série.

## 11. Trading checklist — long

**1D graf**
- ☐ Identifikujem významné S/R zóny a určím, kde sa cena nachádza voči nim.
- ☐ Vyhodnotím 1D Market Structure a určím, či došlo k zmene štruktúry.
- ☐ Pri bearish štruktúre čakám na prerazenie posledného významného High a zatvorenie ceny nad touto úrovňou.
- ☐ Po potvrdení 1D scenára prechádzam na 4H.

**4H graf**
- ☐ Skontrolujem štruktúru od posledného 1D Low.
- ☐ Hľadám bullish štruktúru HH + HL.
- ☐ Overím súlad 4H s 1D.
- ☐ Ak je 4H v súlade s 1D, prechádzam na 1H.

**1H graf**
- ☐ Určím posledné High, Low a aktuálnu cenu.
- ☐ Čakám na prerazenie a uzavretie nad posledným High.
- ☐ Čakám na korekciu a retest prerazenej úrovne, ktorá sa môže stať supportom.
- ☐ Pri odraze hľadám potvrdzujúce Price Action, ideálne sviečku s dlhým spodným knôtom.
- ☐ Určím Stop Loss pod relevantným HL s rezervou podľa štruktúry a likvidity.
- ☐ Skontrolujem RRR minimálne 1:2.
- ☐ Vypočítam veľkosť pozície podľa maximálneho rizika a vzdialenosti SL.

**Vstup:** Ak sú všetky podmienky splnené → otváram LONG.

**NEOBCHODUJEM, AK:**
1. 1D/4H štruktúra nie je jasná.
2. Cena je uprostred range.
3. Nemáme potvrdený breakout.
4. Chýba retest.
5. Retest nemá vhodnú Price Action.
6. Nevychádza požadované RRR.
7. SL je príliš široký.
8. Cena po breakoute ušla bez retestu.

## Kľúčové myšlienky

- Ak nie sú splnené podmienky checklistu, sedím na rukách.
- Dodržiavam minimálne RRR 1:2.
- V každom obchode riskujem vždy rovnakú sumu 50 €.
- Pri RRR 1:1 uzatváram 50 % pozície a SL posúvam na break even.
- Ak ide obchod proti mne, Stop Loss je svätý.
- Nemusím obchodovať každý deň. Mojou úlohou je čakať na kvalitný setup podľa Trading Manualu.
- Neobchodujem to, čo si myslím, že sa stane. Obchodujem to, čo mi potvrdí trh.
