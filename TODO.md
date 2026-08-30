# Kde jsme skončili (30. 8. 2026, verze v43)

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

## Nové ve v43
- **Registry KV2022** (celé kandidátní listiny): import poznává i sloupec
  `CVOLSTRANA`, kterým registry číslují volební stranu – bez něj se kandidáti
  slili do jedné bezejmenné strany. V okně Kandidátky 2022 jsou dva rychlé
  odkazy (registry × výsledky za okres), předvyplněná je adresa registrů.
- **📊 Výsledky 2022 hromadně** – nové tlačítko v liště. Ze souboru
  `vysledky_obce_okres` (XML za okres) naplní `vysledky_2022` všem obcím naráz;
  dřív se to vkládalo po jedné obci.
  - XML se čte **strukturou**, ne přes plochou tabulku jako kandidátky: atributy
    stejného jména se na různých úrovních přepisují (`POC_HLASU` má strana
    i kandidát), takže z ploché tabulky by hlasy za stranu vyšly jako hlasy
    posledního kandidáta.
  - Bere i tabulku (CSV/Excel/HTML), kde je jeden řádek = jedna volební strana
    v obci; tam se počet členů zastupitelstva dopočítá ze součtu mandátů.
  - Chybějící procenta se dopočítají z hlasů (součet hlasů stran = platné hlasy).
  - V náhledu je rozbalovací **„Co apka v souboru našla"** – vypíše názvy
    atributů/sloupců a k jakému poli se přiřadily. Když volby.cz něco pojmenují
    jinak, je hned vidět, co doplnit do `VOBEC` / `VSTR` v kódu.

## Rozdělané – pokračovat tady
1. **Ověřit registry KV2022 na skutečném souboru.** Adresa balíku
   `KV2022reg_csv.zip` (předvyplněná v okně) je odhad podle toho, jak se balíky
   jmenují u ostatních voleb – pokud nesedí, vzít ji ze stránky
   [opendata KV2022](https://www.volby.cz/opendata/kv2022/kv2022_opendata.htm),
   sekce **Registry**, a případně doplnit názvy sloupců do `KPOLE`.
   Špatný import jde smazat: okno Kandidátky 2022 → 🗑 Smazat načtené kandidátky.
2. **Ověřit hromadné výsledky 2022 na skutečném XML.** Kód počítá s atributy
   `CIS_OBEC`, `NAZ_OBEC`, `OKRSKY_CELKEM`, `OKRSKY_ZPRAC`, `ZAPSANI_VOLICI`,
   `VYDANE_OBALKY`, `VOLEBNI_UCAST_PROC`, `ODEVZDANE_OBALKY`, `PLATNE_HLASY`,
   `POR_STR_HL`, `NAZEV_STRK`, `POC_HLASU`, `HLASY_PROC`, `POC_KAND`,
   `POC_MANDATU` a k tomu s hromadou variant. Kdyby se něco nenačetlo, ukáže to
   ta rozbalovací diagnostika v náhledu.
3. Ověřit, jestli prohlížeč pustí stahování přímo z volby.gov.cz (CORS).
   Zatím se počítá s tím, že ne – proto je všude i nahrání souboru z disku.

## Poznámky k datům
- Změny v `hranice.json` se do Firebase dostanou importem kontaktů nebo tlačítkem
  „Srovnat podle hranice.json" v porovnání s AquaControlem.
- Kód obce v našich datech = kód ČSÚ = parametr `xobec` na volby.cz.
