# Kde jsme skončili (28. 8. 2026, verze v42)

## Hotové a nasazené v `main`
- **Hledání po slovech**: dotaz se rozpadne na slova a v textu musí sedět všechna,
  na pořadí nezáleží. Dvě příjmení jdou najít i obráceně nebo se spojovníkem
  („janoušková horváthová" i „Horváthová-Janoušková" najdou Marii Horváthovou
  Janouškovou). Když v podsložce nic nesedí, ukáže se hláška s počtem shod
  ve složce Vše dohromady a tlačítkem na přepnutí.
- **Složky nahoře** dvouúrovňové: Volby 2022 / Volby 2026 / Vše.
  Pod 2022: Kandidátky 2022 · Výsledky voleb · Zastupitelstva 2022–2026.
  Hledání se řídí podsložkou (kandidáti daného roku, strany s mandáty, současné funkce).
- **Výsledky voleb 2022** u obce: souhrn + tabulka stran; plní se vložením stránky
  z volby.cz (Ctrl+A/Ctrl+C). Editor pozná i stránku „Hlasy pro kandidáty" a složí
  z ní kandidátku 2022 (hlasy, procenta, zvolení).
- **Kandidátky 2022** jedou stejnou cestou jako 2026 (přepínač období v importu,
  vlastní pole `strany_2022`, `kandidati_2022`, …).
- **Tisk kandidátek**: za stranu / za obec / dávkově s výběrem obcí fajfkou,
  přepínač období, prázdný sloupec Poznámka.
- **Volební programy** u obce: rozcestník + ruční ukládání odkazů (M. Třebová,
  Polička, Litomyšl, Svitavy mají ověřené odkazy).
- **Porovnání s AquaControlem** + „Srovnat podle hranice.json".
- `hranice.json`: Kladky, Krasíkov a Roubanina nejsou provozované (82/38).

## Rozdělané – pokračovat tady
1. **Hromadný import kandidátek 2022 za okres – zbývá ho jen spustit.**
   - Celé listiny jsou v registrech KV2022 a jsou **ve dvou souborech**:
     `kvrk.csv` (kandidáti; název strany v něm NENÍ, jen `POR_STR_HL`) a
     `kvros.csv` (názvy stran, `NAZEVCELK`). Nahrát oba naráz – apka je spáruje
     přes `KODZASTUP` + `POR_STR_HL`. V importu je na to tlačítko
     **🌐 Stáhnout registry KV2022 (kvrk + kvros)**.
   - Sloupce registrů `KPOLE` trefuje bez úprav (ověřeno na hlavičkách z popisu
     registrů): KODZASTUP→kód, POR_STR_HL→číslo strany, PORCISLO, JMENO,
     PRIJMENI, TITULPRED/ZA, VEK, POVOLANI, BYDLISTEN, PSTRANA, NSTRANA,
     PLATNOST, POCHLASU, MANDAT.
   - Soubory jsou za **celou ČR** (~200 tis. řádků), takže stažení i čtení chvíli
     trvá; apka si nechá jen naše obce (podle kódu), zbytek zahodí.
   - Když prohlížeč stahování nepustí (CORS), otevřít odkaz, uložit na disk
     a nahrát tlačítkem **Vybrat soubor s kandidátkami** – zvládne i .zip.
   - `vysledky_obce_okres?datumvoleb=20220923&nuts=CZ0533` naopak dává
     **výsledky a jen zvolené zastupitele** – hodí se na výsledky voleb, ne sem.
   - Špatný import jde smazat: okno Kandidátky 2022 → 🗑 Smazat načtené kandidátky.
2. **Hromadné výsledky 2022 za okres** – z téhož XML by šlo naplnit `vysledky_2022`
   všem obcím naráz (dnes se vkládá po obcích).
3. Ověřit, jestli prohlížeč pustí stahování přímo z volby.gov.cz (CORS).

## Poznámky k datům
- Změny v `hranice.json` se do Firebase dostanou importem kontaktů nebo tlačítkem
  „Srovnat podle hranice.json" v porovnání s AquaControlem.
- Kód obce v našich datech = kód ČSÚ = parametr `xobec` na volby.cz.
