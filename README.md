# Miniaturny-Automatizovany-Sklenik

## Cieľ projektu

Cieľom je navrhnúť a zostrojiť funkčný model automatizovaného skleníka.

STM32 meria teplotu a vlhkosť vzduchu, vlhkosť pôdy a osvetlenie. Aplikácia v Pythone pre Windows zobrazuje merania a stav zariadení a posiela nastavenia do STM32 cez UART (USB, virtuálny port COM).

## Režimy riadenia

| Zariadenie | Prahový alebo ručný režim | Podľa časovača |
| --- | --- | --- |
| Čerpadlo | Zapne sa, keď vlhkosť pôdy klesne pod nastavenú hranicu. | Denný čas spustenia a dĺžka polievania. |
| Ventilátor | Zapne sa pri prekročení nastavenej teploty. | Denný čas spustenia a dĺžka vetrania. |
| LED | Ručné zapnutie a vypnutie v aplikácii. | Denný čas zapnutia a vypnutia. |

Režim sa volí pre každé zariadenie zvlášť. STM32 obmedzuje dĺžku polievania a dodržiava minimálnu prestávku medzi cyklami v oboch režimoch. Aplikácia pri pripojení synchronizuje čas.

## Tím a úlohy

| Člen tímu | Úlohy |
| --- | --- |
| Kiriienko Yehor | Zapojí snímače teploty, vlhkosti vzduchu a osvetlenia, ventilátor a LED. Naprogramuje meranie, riadenie ventilátora podľa teploty alebo časovača, ručné a časované ovládanie LED a UART na strane STM32. |
| Ievgrafova Ievgeniia | Zapojí a skalibruje snímač vlhkosti pôdy. Zapojí čerpadlo a naprogramuje polievanie a ochranu proti preliatiu. Zostaví skleník a pripraví dokumentáciu. |
| Rudenko Roman | Vytvorí grafickú aplikáciu v Pythone pre Windows. Cez UART zobrazí merania a stav zariadení, umožní nastaviť prahy a časovače a ručne zapnúť alebo vypnúť LED. Pripraví návod na spustenie aplikácie. |

## Postup

1. Dohodnúť zapojenie a formát správ UART.
2. Zapojiť a overiť snímače a výstupy. Súbežne pripraviť rozhranie aplikácie.
3. Skalibrovať snímač pôdy a naprogramovať prahové a časované režimy a ručné ovládanie LED.
4. Zostaviť skleník a prepojiť aplikáciu so STM32.
5. Otestovať oba režimy všetkých zariadení, prenos nastavení a ochranu proti preliatiu. Zaznamenať výsledky.

## Čo potrebujeme od univerzity

Uvedené technické parametre sú orientačné. Možno použiť aj kompatibilné náhrady.

| Položka | Počet | Požiadavka |
| --- | ---: | --- |
| STM32 NUCLEO-F303K8 | 1 ks | S osadenými pinovými lištami. |
| Dátový USB kábel | 1 ks | USB-A → Micro-B, pre ST-LINK a virtuálny COM port. |
| Modul BME280 | 1 ks | I²C, napájanie a logika 3,3 V, osadené piny. |
| Modul BH1750 | 1 ks | I²C, napájanie a logika 3,3 V, osadené piny. |
| Kapacitný snímač vlhkosti pôdy | 1 ks | DFRobot SEN0193 alebo ekvivalent s analógovým výstupom 0–3,0 V, vrátane 3-pinového kábla. |
| Ventilátor | 1 ks | Dvojvodičový, 12 V DC, rozbehový prúd najviac 0,5 A. |
| Biely LED pásik s prívodnými vodičmi | 1 ks | 12 V DC, dĺžka 25 cm, odber najviac 0,5 A. |
| Mini ponorné čerpadlo | 1 ks | 12 V DC, rozbehový prúd najviac 1,5 A. |
| Hadička k čerpadlu | 1 m | Vnútorný priemer podľa vývodu dodaného čerpadla. |
| MOSFET spínací modul | 3 ks | Jednokanálový, aktívny pri logickej 1, vstup 3,3 V, záťaž 12 V DC, trvalý prúd aspoň 3 A, skrutkové svorky. |
| Ochranná Schottkyho dióda | 2 ks | 1N5822, 3 A / 40 V, jedna pre čerpadlo a jedna pre ventilátor. |
| Napájací adaptér | 1 ks | Stabilizovaný 12 V DC / 3 A, so zástrčkou DC 5,5 × 2,1 mm, plus v strede. |
| Adaptér DC konektora na svorky | 1 ks | Zásuvka 5,5 × 2,1 mm na dvojpólovú skrutkovú svorku, aspoň 3 A. |
| Rozbočovacia svorka | 2 ks | Päťpolohová, aspoň 3 A, pre kladnú a zápornú vetvu napájania. |
| Napájací vodič | 4 m | Lanko 0,5 mm², 2 m červený a 2 m čierny. |
| Breadboard | 1 ks | 830 kontaktov. |
| Prepojovacie vodiče Dupont | 30 ks | 10 M–M, 10 M–F, 10 F–F, dĺžka 20 cm. |
| Rezistor 4,7 kΩ | 2 ks | Pre SDA a SCL. |
| Rezistor 10 kΩ | 3 ks | Pre vstupy MOSFET modulov. |
| Multimeter | 1 ks | Na zapožičanie. |
| Referenčný teplomer s vlhkomerom | 1 ks | Na zapožičanie. |

Konštrukciu skleníka, nádrž na vodu a kvetináč si zabezpečí tím.
