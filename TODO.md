# Kde jsme skončili (12. 10. 2026, verze v45)

## Hotové a nasazené v `main`
- **Ceny svazků** (v77): `volby_ceny/sv_<id svazku>/<rok>`; obec ve svazku přebírá
  každou cenu svazku, kterou sama nemá (`cenaRok`). Zadání v detailu svazku (💧 Ceny
  vody svazku) nebo importem z Excelu – řádek jde přiřadit ke svazku. V mapě poznámka
  „vodné ze svazku …“, v přehledu značka sv.
- **Mapa** (v76): klik na obec = okénko se základními údaji + Zobrazit vše.
- **Vedení zůstává** (v74): v detailu obce u prázdného starosty/místostarosty 2026–2030
  tlačítko „↪ zůstává …“ (převezme jméno, tel., e-mail z 2022–26, jen prázdná pole,
  ukáže, zda byl zvolen 2026); v úpravě obce tlačítko „Vedení zůstává“; pro správce
  hromadně „↪ Starostové zůstávají“ s náhledem (předzaškrtnutí znovu zvolení 2026).
- **Firebase Hosting** (v73): `firebase.json` (web `volby-vhos` v projektu moje-budky),
  `.firebaserc`, akce `.github/workflows/firebase-hosting.yml` nasazuje při pushi do
  main. Potřebuje secret `FIREBASE_SERVICE_ACCOUNT_MOJE_BUDKY`, web `volby-vhos` ve
  Firebase Hosting a doménu `volby-vhos.web.app` v Authentication → Authorized domains.
  Po ověření: repo přepnout na soukromé (GitHub Pages pak skončí).
- **Ceny 2025** (v73): tooltip ukazuje poslední 2 roky, přehled sloupec předchozího roku
  s % změnou; složka Volby v detailu je vždy zabalená (otevře se jen při hledání).
- **Ceny – import z Excelu** (v70): v přehledu 💧 Ceny vody tlačítko ⬆️ Nahrát ceny
  z Excelu (jen správce). Tabulka VHOS (kód VF…/VO…, lokalita, druh, roky bez DPH a
  s DPH) – bere blok s DPH, vybraný rok; druh vf=vodné, vo=stočné, voda před.=
  `predana`, přev.k čištění=`cisteni`. Lokality páruje na obce podle názvu se
  zkratkami, náhled se zaškrtnutím. Předaná a čištění se ukazují jen kde jsou.
- **Vodovod × kanalizace** (v66): pole `kanal` ("" = stejně jako vodovod, `vhos`,
  `jiny`, `zadna`) + `provozovatel_kanal`. Detail (💧 Vodovod / 🚰 Kanalizace),
  štítky „jen vodovod“ / „kanalizace VHOS“, tooltip, přehled cen. Radiměř a Hradec
  nad Svitavou nastaveny na jen vodovod (`JEN_VODOVOD`). Čeká se na tabulku cen.
- **Ceny vody** (v65): `volby_ceny/<kod>/<rok> = {vodne, stocne}` Kč/m³ s DPH.
  Zadává správce v detailu obce (sekce 💧 Ceny vody), vidí všichni: tooltip v mapě
  (poslední rok), přehled 💧 Ceny vody nahoře (rok, řazení, průměr).
  Pravidlo: čtení se seznamem přístupů, zápis jen admin / `volby_spravci`.
- **Provozovatel vodovodu** (v63): u neprovozovaných obcí pole `provozovatel`
  (úprava ✏️ s našeptávačem dosavadních hodnot), ukazuje se ve štítku, detailu a
  v tooltipu mapy („Provozuje: …“).
- **Starostové z Wikidat** (v62, jen správce): tlačítko 👤 Doplnit starosty – SPARQL z
  prohlížeče (P7606/P782 → P6 s daty od/do), náhled, zapíše jen zaškrtnuté do
  `starosta` (2022–26) a `starosta_2026`, k tomu `*_zdroj: Wikidata`. Odsud
  (z cloudu) se na Wikidata nedá dostat, dotaz neověřen na živých datech.
- **Velké Opatovice** (v61, okres Blansko, kód 582646, neprovozováno): hranice v
  `hranice.json` (ČÚZK INSPIRE přes siwekm/czech-geojson), záznam ve `volby_obce`
  založí správce automaticky (`EXTRA_OBCE`). Import kandidátek/výsledků je dál jen
  za okres Svitavy. Mapa má vlastní popisky obcí od zoomu 11. 📝 Poznámky jsou
  nahoře vedle Seznam / Mapa.
- **Mapa** (v58): nad mapou hledání s našeptávačem (obec, starosta, místostarosta);
  klik/Enter obec zvýrazní. Horní hledání v režimu mapy plní totéž. Tooltip ukazuje
  starostu (nový 2026–2030 má přednost). U obce nová pole `starosta_2026`,
  `mistostarosta_2026` (+ `_tel`, `_email`) – sekce Vedení obce 2026–2030.
- **Poznámky k obcím** (v54): v detailu obce sekce Poznámky – 🔒 soukromé
  (`volby_poznamky_soukrome/<email>/<kod>/<id>`, vidí jen autor) a 👥 veřejné
  (`volby_poznamky_verejne/<kod>/<id>`, vidí všichni, mění autor + správce).
  Dole tlačítko 📝 Poznámky = přehled všech s filtrem a hledáním. Staré pole
  `poznamky` zůstává jako „Společná poznámka k obci“.
- **Kdo je online** (v53): každý přihlášený zapisuje `volby_presence/<email>/c/<spojeni>`
  (onDisconnect maže, `ts` = naposledy). Správce vidí vpravo nahoře 🟢 N online a seznam.
  Pravidlo: čte jen admin / `volby_spravci`, zapisuje každý jen svůj klíč.
- **Správa přístupů** (v51): tlačítko 👥 Přístupy vpravo nahoře vidí jen správci
  z uzlu `volby_spravci` (klíč = e-mail, tečky → čárky). Přidává/odebírá e-maily
  v `florian_login_email` (společné s Floriánem). **Ve Firebase je potřeba uzel
  `volby_spravci` a pravidla** – zápis do `florian_login_email` jen pro správce.
- **Výsledky voleb 2026** (v44): pod Volby 2026 podsložka *Výsledky voleb*, v detailu
  obce sekce *Výsledky voleb 2026* (✏️ = vložit stránku z volby.cz, jako u 2022)
  a dole tlačítko **📊 Výsledky voleb** = import za celý okres z XML
  „Obce – výsledky za okresy a obce" (`nuts=CZ0533`). Ukládá se do `vysledky_2026`
  (souhrn, strany, `zvoleni`); u načtené kandidátky 2026 doplní hlasy a ✔ zvolen.
  Funguje i pro 2022 (přepínač roku). `zastupitelstvo_2026` se zatím needituje.
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
- **Přílohy k volebním programům** (v43): v editoru programů u každé strany
  📎 Soubor (PDF/obrázek) a 📷 Vyfotit. Data jdou do uzlu `volby_soubory`
  (fotky zmenšené na 2000 px, limit 6 MB), u obce jen metadata
  `programy_soubory_2026`. **Ve Firebase je potřeba pravidlo pro
  `volby_soubory`** (stejné jako u `volby_obce`).
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
2. ~~Hromadné výsledky za okres~~ – hotové v v44 (📊 Výsledky voleb). Ověřit na ostrém XML
   Ověřeno 12. 10. 2026 na ostrém XML 2026 (načteno a uloženo). Adresa:
   `https://volby.gov.cz/appdata/kv2026/20261009/odata/okresy/vysledky_obce_okres_CZ0533.xml`
3. Ověřit, jestli prohlížeč pustí stahování přímo z volby.gov.cz (CORS).

## Poznámky k datům
- Změny v `hranice.json` se do Firebase dostanou importem kontaktů nebo tlačítkem
  „Srovnat podle hranice.json" v porovnání s AquaControlem.
- Kód obce v našich datech = kód ČSÚ = parametr `xobec` na volby.cz.
