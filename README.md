Názov projektu:
Larnia – Smart AI Teacher
Stručná anotácia:
Larnia je dotykové zariadenie s hlasovou interakciou (full voice + touch), ktoré slúži ako “smart AI teacher” pre študentov. Zariadenie umožní prirodzený dialóg so študentom, vysvetľovanie učiva, generovanie príkladov a kvízov a poskytne moderné UI s avatarom. Dôraz kladieme na intuitívnosť, rýchlu odozvu, profesionálny vzhľad a reálnu použiteľnosť v školskom prostredí.

1. Cieľ projektu
Navrhnúť a zrealizovať funkčný prototyp HMI/IoT zariadenia s dotykovým displejom a hlasovým ovládaním.
Integrovať AI asistenta napojeného cez serverovú bránu (gateway) na cloudové AI modely.
Vytvoriť UI/UX s personalizovateľným avatarom a hlasom, vhodné pre výučbu.

2. Prečo ESP32-P4 a zvolený prístup
Zvolili sme platformu ESP32-P4 najmä kvôli tomu, že je vhodná pre výkonné HMI aplikácie:
umožňuje plynulejšie grafické rozhranie a prácu s vyšším rozlíšením,
na použitej doske je 7" IPS dotykový displej s rozlíšením 1024×600, čo výrazne zvyšuje “wow efekt” aj čitateľnosť UI,
konkrétne zariadenie je postavené na kombinácii ESP32-P4 + ESP32-C6 (bezdrôtové pripojenie cez Wi-Fi 6 a Bluetooth 5.3). 
Tento prístup je pre nás výhodný: výkon využijeme na UI a multimédiá, zatiaľ čo AI spracovanie prebieha mimo zariadenia (bezpečnejšie, flexibilnejšie a lepšie škálovateľné).

3. Zariadenie a komponenty (stručne)
Základný hardware (front-end zariadenie): (može sa prehodnotiť pri vývoji aplikácie)
Elecrow CrowPanel Advanced 7" (ESP32-P4) – 7" IPS capacitive touch, 1024×600, výkonný HMI základ (16 MB Flash, 32 MB PSRAM) a externý bezdrôtový modul ESP32-C6 (Wi-Fi 6 + Bluetooth 5.3). 
Audio vstup/výstup: mikrofón + výstup na reproduktory (reálne voice použitie).
Všetky komponenty budú integrované do jednej 3D tlačenej krabičky (estetika, ochrana, akustika, jednoduché používanie).
Doplňujúca elektronika (voliteľne pre profesionálny vnútorný dizajn):
plánujeme malú “dcérsku” dosku (mezzanine) na prehľadné prepojenia (napr. audio line-out / konektory), ktorú vieme dať vyrobiť a osadiť cez PCB/PCBA služby (napr. JLCPCB). (Nie je to povinné pre prvý prototyp, ale zvýši profesionalitu a zníži kabeláž.)

4. Použité technológie a jazyky
Firmware + UI na zariadení: C/C++ (ESP-IDF) + LVGL (Light and Versatile Graphics Library – knižnica na tvorbu grafického rozhrania pre embedded displeje). 
Serverová brána (gateway): Python (FastAPI) – zabezpečí komunikáciu, spracovanie požiadaviek a napojenie na AI API.
Verzionovanie a spolupráca: Git/GitHub.

5. Aké AI bude Larnia používať
Riešenie bude kombinovať:
GPT-5.2 ako hlavný model pre textové vysvetľovanie, generovanie príkladov, tvorbu kvízov a pedagogickú logiku. 
Realtime model (gpt-realtime) cez OpenAI Realtime API pre nízkolatenčnú hlasovú komunikáciu (speech-to-speech / audio interakcia). 
Pozn.: kľúče a citlivé nastavenia nebudú uložené priamo v zariadení – komunikácia pôjde cez server (bezpečnosť a jednoduchšia správa).

6. Funkcionalita aplikácie (čo bude vedieť)
Základné režimy:
Tutor mód: študent sa pýta hlasom alebo dotykom, Larnia odpovedá hlasom aj textom, doplní príklady a vysvetlí “iným spôsobom”.
Quiz mód: generovanie krátkych otázok a úloh, vyhodnotenie a spätná väzba.
Rýchle menu (touch): preddefinované akcie (zopakuj, daj príklad, sprav kvíz, vysvetli stručne/podrobne).
Nastavenia + personalizácia:
personalizovaná konfigurácia avatara (témy, skin, vizuálne štýly),
personalizácia hlasu (výber hlasu, tempo/štýl podľa režimu),
voľba režimu hlasu: najprv “push-to-talk”, neskôr rozšírenie o hands-free.
Pridaná funkcionalita – Bluetooth slúchadlá:
Pre možnosť používať bežné BT slúchadlá plánujeme integrovať do krabičky externý Bluetooth audio transmitter (A2DP), ktorý bude napájaný priamo v zariadení. Z pohľadu používateľa ide o natívnu funkciu “pripoj slúchadlá”, technicky je to spoľahlivejší prístup než spoliehať sa na samotné BLE(nefunguje ako klasický bluethoth).

7. Plán vývoja (milníky)
Návrh architektúry, UI flow a scenárov použitia.
Bring-up zariadenia: stabilné UI demo (touch + obrazovky).
Audio pipeline: test mikrofón ↔ reproduktor, následne komunikácia so serverom.
Server gateway: bezpečná komunikácia a napojenie na AI (GPT-5.2 + realtime voice).
Implementácia režimov Tutor/Quiz, história a základné nastavenia.
Personalizácia avatara a hlasu + UX doladenie.
Integrácia BT slúchadiel (externý transmitter) a finálne zloženie do krabičky.
Testovanie, dokumentácia, demo scenáre, GitHub, poster a prezentácia.