# Miniaturny-Automatizovany-Sklenik

## Cieľ projektu

Cieľom je navrhnúť a zostrojiť funkčný model malého skleníka. Riadiaca jednotka priebežne meria teplotu a vlhkosť vzduchu, vlhkosť pôdy a intenzitu osvetlenia. Podľa nameraných hodnôt automaticky ovláda ventilátor, zavlažovanie a doplnkové LED osvetlenie.

Používateľ môže sledovať aktuálne hodnoty a upravovať požadované medzné hodnoty. Súčasťou riešenia je kalibrácia snímačov, ochrana proti nadmernému zavlažovaniu a vyhodnotenie priebehu regulácie.

## Funkcie

- Meranie teploty a relatívnej vlhkosti vzduchu.
- Meranie vlhkosti pôdy.
- Meranie intenzity okolitého svetla.
- Automatické osvetlenie: pri nedostatku svetla sa zapne LED osvetlenie.
- Automatické vetranie: pri prekročení nastavenej teploty sa zapne ventilátor.
- Automatické zavlažovanie: pri suchej pôde sa zapne čerpadlo.
- Nastaviteľné prahové hodnoty a zobrazenie aktuálneho stavu.
- Časový limit zavlažovania a minimálna pauza medzi cyklami ako ochrana proti preliatiu.
- Kalibrácia snímača vlhkosti pôdy a overenie správnosti meraní.

## Princíp riadenia

| Meraná veličina | Podmienka | Reakcia systému |
| --- | --- | --- |
| Osvetlenie | intenzita je pod nastaveným limitom | zapne sa LED osvetlenie |
| Teplota | teplota je nad nastaveným limitom | zapne sa ventilátor |
| Vlhkosť pôdy | vlhkosť je pod nastaveným limitom | na obmedzený čas sa zapne čerpadlo |

## Tím a zodpovednosti

| Člen tímu | Hlavná oblasť zodpovednosti |
| --- | --- |
| **Kiriienko Yehor** | Pripojenie snímačov BME280, BH1750 a snímača vlhkosti pôdy; kalibrácia; zostavenie konštrukcie a umiestnenie snímačov; reálne merania a fotografie. |
| **Ievgrafova Ievgeniia** | Pripojenie LED, MOSFET modulov, ventilátora a čerpadla; PWM riadenie a kontrola napájania; integračné testy; finálne spracovanie README, správy a prípadnej prezentácie. |
| **Rudenko Roman** | Hlavný firmvér: I²C, ADC, PWM, získavanie meraní, algoritmus regulácie, hysterezia a ochrana proti nadmernému zavlažovaniu; správa zdrojového kódu v GitHube. |

### Výstupy jednotlivých členov

| Člen tímu | Povinné podklady pre výslednú dokumentáciu |
| --- | --- |
| **Kiriienko Yehor** | Schéma pripojenia snímačov, výsledky kalibrácie vlhkosti pôdy, fotografie konštrukcie a tabuľka reálnych nameraných hodnôt. |
| **Ievgrafova Ievgeniia** | Schéma napájania a MOSFET zapojenia, výsledky bezpečnostných a integračných testov, finálne zjednotenie dokumentácie. |
| **Rudenko Roman** | Pracovný kód, opis regulačného algoritmu, prahových hodnôt, hysterezie a ochrany proti preliatiu, záznamy z programu počas testov. |

### Postup práce v etapách

| Etapa | Kiriienko Yehor — snímače a konštrukcia | Ievgrafova Ievgeniia — aktuátory a dokumentácia | Rudenko Roman — firmvér |
| --- | --- | --- | --- |
| **1. Návrh** | Pripraví zapojenie a umiestnenie snímačov v modeli. | Navrhne napájanie a zapojenie MOSFET modulov, ventilátora, čerpadla a LED. | Pripraví projekt v STM32CubeIDE, repozitár GitHub a návrh regulačného algoritmu. |
| **2. Samostatné moduly** | Pripojí BME280, BH1750 a snímač pôdy; overí namerané hodnoty. | Pripojí LED, ventilátor a čerpadlo cez MOSFET; overí PWM a bezpečné napájanie. | Implementuje I²C, ADC a PWM ovládače a spracovanie nameraných údajov. |
| **3. Kalibrácia a regulácia** | Zmeria hodnoty snímača pôdy v suchej a mokrej pôde a vytvorí kalibračné údaje. | Overí pracovné režimy ventilátora a čerpadla a zaznamená bezpečné limity. | Implementuje prepočet ADC na vlhkosť, prahové hodnoty, hystereziu a časové obmedzenie zavlažovania. |
| **4. Integrácia** | Umiestni snímače do konštrukcie a kontroluje správnosť meraní. | Zostaví fyzický model, kontroluje kabeláž a vykoná integračné testy aktuátorov. | Spojí moduly do jednej aplikácie: tma → LED, vysoká teplota → ventilátor, suchá pôda → zavlažovanie. |
| **5. Testovanie** | Simuluje zmenu svetla, teploty a vlhkosti pôdy; zaznamenáva hodnoty a fotografie. | Kontroluje bezpečnosť a reakcie LED, ventilátora a čerpadla; zaznamenáva výsledky testov. | Analyzuje logy, opravuje chyby programu a overuje ochranu proti nadmernému zavlažovaniu. |
| **6. Odovzdanie a obhajoba** | Dodá schémy, kalibračné údaje a fotografie. | Zjednotí README, správu a prípadnú prezentáciu. | Dodá finálny zdrojový kód a opis regulačného algoritmu. |

## Potrebný hardvér

| Položka | Počet | Rozhranie / riadenie | Účel | Zabezpečí |
| --- | ---: | --- | --- | --- |
| Vývojová doska STM32 Nucleo (napr. NUCLEO-F303K8) | 1 | — | hlavná riadiaca jednotka | univerzita |
| BME280 | 1 | I²C | meranie teploty a relatívnej vlhkosti vzduchu | univerzita |
| BH1750 | 1 | I²C | meranie intenzity okolitého svetla | univerzita |
| Kapacitný snímač vlhkosti pôdy | 1 | ADC | meranie vlhkosti substrátu; kapacitná verzia je odolnejšia než odporová | univerzita |
| LED alebo LED pásik pre rastliny | 1 | digitálny výstup alebo PWM | doplnkové osvetlenie | univerzita |
| DC ventilátor 5 V / 12 V | 1 | PWM cez MOSFET | vetranie a možnosť regulácie otáčok | univerzita |
| Mini ponorné DC čerpadlo s hadičkou | 1 | PWM cez MOSFET | zavlažovanie a možnosť regulácie výkonu | univerzita |
| MOSFET moduly | 2 až 3 | ovládanie záťaží | bezpečné spínanie ventilátora, čerpadla a prípadne LED | univerzita |
| Externý zdroj pre záťaže | 1 | — | napájanie čerpadla, ventilátora a LED podľa ich napätia | univerzita |
| Dióda proti spätnému napätiu | 2 | pri DC motoroch | ochrana pri ventilátore a čerpadle | univerzita |
| Rezistory, vodiče a breadboard | podľa potreby | — | prepojovacie a pomocné obvody | univerzita |
| Nádoba na vodu, kvetináč, substrát a rastlina | 1 sada | — | fyzický model skleníka | tím má k dispozícii |
| Konštrukcia skleníka | 1 | — | upevnenie LED, ventilátora a snímačov okolo rastliny | tím má k dispozícii |
| USB kábel pre Nucleo | 1 | USB | programovanie a komunikácia s počítačom | univerzita |


## Kalibrácia a testovanie

1. Porovnať teplotu a vlhkosť vzduchu s referenčným teplomerom/vlhkomerom.
2. Pre snímač pôdy zaznamenať hodnotu v suchej pôde a vo vlhkej pôde a z týchto hodnôt vytvoriť percentuálnu škálu.
3. Overiť reakciu osvetlenia pri zakrytí snímača svetla.
4. Overiť zapnutie a vypnutie ventilátora pri zmene teplotného prahu.
5. Overiť automatické zavlažovanie v suchej pôde a maximálny čas činnosti čerpadla.
6. Zaznamenať namerané hodnoty a stavy aktuátorov počas testu a vyhodnotiť stabilitu regulácie.

## Softvér

- STM32CubeIDE / STM32CubeMX
- programovací jazyk C
- Git a GitHub pre správu zdrojového kódu a dokumentácie

## Plánovaný výstup

- Funkčný fyzický model skleníka.
- Zdrojový kód firmvéru a schéma zapojenia v tomto repozitári.
- Popis kalibrácie, testovacie výsledky a stručné vyhodnotenie regulácie.
- Prezentácia a praktická ukážka funkcií systému.
