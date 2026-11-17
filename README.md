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
| Ultrazvukový rozprašovač | Zapne sa, keď relatívna vlhkosť vzduchu klesne pod hranicu nastavenú v aplikácii. | — |

Režim sa volí pre každé zariadenie zvlášť. STM32 obmedzuje dĺžku polievania a dodržiava minimálnu prestávku medzi cyklami v oboch režimoch. Aplikácia pri pripojení synchronizuje čas. Rozprašovač sa vypne po dosiahnutí nastavenej vlhkosti, pri nedostatku vody alebo pri chybe merania. STM32 obmedzí dĺžku jedného cyklu a pred ďalším cyklom znova zmeria vlhkosť.

## Tím a úlohy

| Člen tímu | Úlohy |
| --- | --- |
| Kiriienko Yehor | Zapojí snímače teploty, vlhkosti vzduchu a osvetlenia, ventilátor a LED. Naprogramuje meranie, riadenie ventilátora podľa teploty alebo časovača, ručné a časované ovládanie LED, riadenie rozprašovača podľa vlhkosti vzduchu a UART na strane STM32. |
| Ievgrafova Ievgeniia | Zapojí a skalibruje snímač vlhkosti pôdy. Zapojí čerpadlo a naprogramuje polievanie a ochranu proti preliatiu. Zostaví skleník, osadí rozprašovač s nádržkou a pripraví dokumentáciu. |
| Rudenko Roman | Vytvorí grafickú aplikáciu v Pythone pre Windows. Cez UART zobrazí merania a stav zariadení, umožní nastaviť prahy a časovače a ručne zapnúť alebo vypnúť LED a nastaviť požadovanú vlhkosť vzduchu. Zobrazí stav rozprašovača. Pripraví návod na spustenie aplikácie. |

## Postup

1. Dohodnúť zapojenie a formát správ UART.
2. Zapojiť a overiť snímače a výstupy. Súbežne pripraviť rozhranie aplikácie.
3. Skalibrovať snímač pôdy a naprogramovať prahové a časované režimy a ručné ovládanie LED.
4. Zostaviť skleník a prepojiť aplikáciu so STM32.
5. V aplikácii overiť zobrazenie meraní a prenos nastavení do STM32. Vyskúšať čerpadlo podľa vlhkosti pôdy a časovača, ventilátor podľa teploty a časovača a LED ručne aj podľa časovača. Pri oboch režimoch polievania overiť maximálnu dĺžku chodu a minimálnu prestávku. Overiť zapnutie rozprašovača pri nízkej vlhkosti a jeho vypnutie pri dosiahnutí prahu alebo pri nedostatku vody. Zaznamenať výsledky.

## Čo potrebujeme

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
| Ultrazvukový rozprašovač | 1 sada | Grove Water Atomization alebo ekvivalent: 5 V DC, s riadiacou doskou a piezoelektrickým diskom. |
| Napájací zdroj pre rozprašovač | 1 ks | Stabilizovaný 5 V DC / 1 A alebo viac, s vývodmi na svorky. |
| Prevodník logických úrovní | 1 ks | Digitálny, 3,3 V → 5 V pre vstup EN modulu, napr. modul s 74AHCT125. |
| Kábel Grove na Dupont | 1 ks | Pre 5 V, GND a EN. |
| Plavákový snímač hladiny | 1 ks | Suchý kontakt pre 3,3 V vstup STM32, zopnutý pri dostatku vody. |
| Multimeter | 1 ks | Na zapožičanie. |
| Referenčný teplomer s vlhkomerom | 1 ks | Na zapožičanie. |

Konštrukciu skleníka, nádrž na polievanie, nádržku na rozprašovač a kvetináč s podmiskou zabezpečí tím.
