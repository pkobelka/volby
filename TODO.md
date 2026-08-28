# Kde jsme skončili (28. 8. 2026, verze v42)

## Hotové a nasazené v `main`
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
1. **Hromadný import kandidátek 2022 za okres.**
   - `vysledky_obce_okres?datumvoleb=20220923&nuts=CZ0533` (předvyplněné v importu)
     dává **výsledky a jen zvolené zastupitele**, ne celé kandidátní listiny.
   - Celé listiny mají být v **Registrech** (opendata KV2022 → Registry XML/Excel/CSV).
     Vyzkoušet, a když se sloupce netrefí, doplnit je do `KPOLE`.
   - Špatný import jde smazat: okno Kandidátky 2022 → 🗑 Smazat načtené kandidátky.
2. **Hromadné výsledky 2022 za okres** – z téhož XML by šlo naplnit `vysledky_2022`
   všem obcím naráz (dnes se vkládá po obcích).
3. Ověřit, jestli prohlížeč pustí stahování přímo z volby.gov.cz (CORS).

## Poznámky k datům
- Změny v `hranice.json` se do Firebase dostanou importem kontaktů nebo tlačítkem
  „Srovnat podle hranice.json" v porovnání s AquaControlem.
- Kód obce v našich datech = kód ČSÚ = parametr `xobec` na volby.cz.
