# Pumpy Medtronic

**>>>> Medtronic pump driver is from 2.5 version part of AndroidAPS (master). While this is the case, Medtronic driver should still be considered beta software. Please install only if you are expirenced user. At the moment we are still fighting with double Bolus issue (We get 2 boluses in treatments, which throws IOB calculation (if you experience this bug, please enable Double Bolus Logging in Medtronic configuration and provide your logs)), this should be fixed with upcomming release. <<<<**

* * *

Pracuje pouze se staršími pumpami Medtronic (podrobnosti viz níže). Nefunguje s Medtronic 640G nebo 670G.

* * *

If you started using Medtronic driver please add yourself to this [list](https://docs.google.com/spreadsheets/d/16XIjviXe8b-12PrB6brGubNFuAEsFZr10pjLt_SpSFQ/edit#gid=0). This is just so that we can see which Phones are good and which are not so good (or bad) for this driver. There is one column called "BT restart". This is to check if yourPhone supports BT enable/disable, which can be used when pump is no longer able to connect, that happens from time to time. If you notice any other problem, please write that in Comments column.

* * *

## Hardwarové a softwarové požadavky

- **Telefon:** Ovladač Medtronic by měl pracovat s jakýmkoli telefonem s podporou BLE. **DŮLEŽITÉ: Ačkoli ovladač pracuje správně na všech telefonech, zapnutí/vypnutí Bluetooth všude nefunguje (to je požadováno, když ztratíte připojení k RileyLink a systém se nemůže zotavit automaticky – čas od času se to stává). Takže budete potřebovat získat zařízení s Android 6.0-8.1, v nejhorším případě můžete na svůj telefon nainstalovat LineeaeOS 15.1 (povinné 15.1 nebo nižší). Zabýváme se problémem se systémem Android 9, ale dosud jsme nenalezli řešení (zdá se, že funguje na některých modelech a ne na jiných, a také někdy pracuje jen na některých modelech).**
- **RileyLink/Gnarl:** Pro komunikaci s pumpou je třeba zařízení, které převádí příkazy BT z telefonu na příkazy RF, kterým pumpa rozumí. Zařízení, které to dělá, se nazývá RileyLink (můžete jej získat zde [getrileylink.org](https://getrileylink.org/)). Potřebujete stabilní verzi zařízení, což je pro starší modely firmware 0.9 (starší verze nemusí fungovat správně) nebo pro novější modely 2.2 (existují možnosti upgradu dostupné na serveru RL). Pokud máte dobrodružnou povahu, můžete také zkusit Gnarl ([zde](https://github.com/ecc1/gnarl)), který je něco jako RileyLink klon. 
- **Pumpa:** Ovladač funguje pouze s následujícími modely a verzemi firmwaru: 
    - 512/712
    - 515/715
    - 522/722
    - 523/723 (firmware 2.4A nebo nižší)
    - 554/754 EU verze (firmware 2.6A nebo nižší)
    - 554/754 verze pro Kanadu (firmware 2.7A nebo nižší)

## Nastavení pumpy

- **Povolit vzdálený režim na pumpě** (Utilities -> Remote Options, vybrat Ano a na další obrazovce Přidat ID a přidat fiktivní ID (111111 nebo něco podobného). Musíte mít alespoň jedno ID na tomto seznamu vzdálených ID. Tyto volby mohou na jiném modelu pumpy vypadat jinak. Tento krok je důležitý, protože při nastavení bude pumpa naslouchat častěji kvůli vzdálené komunikaci.
- **Nastavte maximální hodnotu bazálu** na své pumpě na „maximální bazál ve vašem profilu STD“ * 4 (pokud chcete mít 400% TBR jako max). Toto číslo musí být pod 35 (jak můžete vidět na pumpě).
- **Nastavte maximální hodnotu bolusu** na své pumpě (maximum je 25)
- **Nastavte profil na STD**. To bude jediný profil, který budeme používat. Můžete to také zakázat.
- **Nastavit typ TBR** na absolutní hodnotu (nikoli v procentech)

## Konfigurace telefonu/AndroidAPS

- **Nepárujte RileyLink se svým telefonem.** Pokud jste spárovali RileyLink, pak ho AndroidAPS nedokáže najít v konfiguraci.
- Zakažte funkci Auto-rotate na telefonu (některé zařízení automaticky restartují BT spojení, což není něco, co bychom chtěli).
- Pumpu v AndroidAPS můžete nastavit dvěma způsoby: 

1. Použití průvodce (při nové instalaci)
2. Přímo na kartě Konfigurace (ikona ozubeného kola u ovladače Medtronic)

Pokud děláte novou instalaci, skočíte přímo do průvodce. Někdy, když vaše připojení BT není plně funkční (nelze se připojit k pumpě), nebudete možná moci úplně dokončit konfiguraci. V takovém případě vyberte virtuální pumpu a po dokončení průvodce můžete použít možnost 2, která obejde detekci pumpy.

![Nastavení MDT](../images/Medtronic01.png)

Je třeba nastavit následující položky: (viz obrázek výše)

- ** Sériové číslo pumpy**: Můžete ho najít na zadní straně, SN. Použijte pouze číslice, vaše sériové číslo je 6 čísel.
- **Typ pumpy**: Typ pumpy, který máte (tj. 522). 
- **Frekvence pumpy**: Podle frekvence pumpy existují dvě verze pumpy Medtronic (pokud si nejste jisti, jakou frekvenci využívá vaše pumpa, podívejte se na [FAQ](../Configuration/MedtronicPump#faq)): 
    - pro USA & Kanadu je frekvence 916 MHz
    - pro zbytek světa je frekvence 868 MHz
- **Maximální bolus na pumpě(U)** (za hodinu): Toto musí být nastaveno stejně jako na pumpě. Jde o nastavení omezující možnou velikost bolusu. Pokud zadáte větší hodnotu, bolus nebude proveden a bude vrácena chyba. Maximální hodnota, kterou lze použít, je 25. Prosím, nastavte správnou hodnotu pro sebe tak, aby nemohlo dojít k předávkování.
- **Maximální bazál na pumpě(U/h)**: Toto musí být nastaveno stejně jako na pumpě. Jde o nastavení omezující maximální hodinový bazál. Například, pokud chcete mít nastaveno maximální množství TBR na 500 % a nejvyšší bazál je 1,5 U, pak byste měli nastavit maximální bazál na alespoň 7,5. Pokud je toto nastavení chybné (například pokud by nějaký z vašich bazálů byl vyšší, pumpa by vrátila chybu).
- **Prodleva před spuštěním bolusu (s)**: Toto je prodleva před odesláním bolusu do pumpy, takže pokud změníte názor, můžete bolus zrušit. Zrušení bolusu po spuštění není pumpou podporováno (pokud chcete zastavit bolus během vydávání, musíte pozastavit pumpu a pak pokračovat).
- **Kódování Medtronic**: Toto nastavení určuje, zda se kódování 4b6b provádí v AndroidAPS nebo na RileyLink. Máte-li produkt RileyLink s firmwarem verze 2.x, výchozí hodnota bude používat kódování hardwarové (v RileyLinku), pokud máte firmware verze 0.x, toto nastavení bude ignorováno.
- **Typ baterie (Power View)**: Pokud chcete vidět stav baterie v pumpě, musíte vybrat typ baterie, kterou používáte (momentálně jsou podporované lithiové nebo alkalické), což změní zobrazení vypočítané z procent a voltů.
- **Konfigurace RieyLink**: Toto vyhledá vaše zařízení RileyLink/GNARL.

## Záložka MEDTRONIC (MDT)

![Záložka MDT](../images/Medtronic02.png)

Na záložce pumpy můžete vidět několik řádků, které zobrazují aktuální stav pumpy (a připojení).

- **RileyLink Status**: Zobrazuje stav připojení RileyLink. Telefon by měl být připojen k RileyLink celou dobu.
- **Stav pumpy**: Stav připojení pumpy může mít několik hodnot, ale většinou se zobrazí ikona spánku (když není aktivní připojení k pumpě). Když je příkaz spuštěn, možná uvidíte „Waking Up“, což znamená, že se AAPS snaží navázat spojení s pumpou, nebo popis jiného příkazu, který může být na pumpě spuštěn (např.: Get Time, Set TBR atd.).
- **Baterie**: Ukazuje stav baterie v závislosti na konfiguraci. To může být jednoduchá ikona zobrazující, zda je baterie prázdná nebo plná (červená, pokud je baterie kritická, pod 20 %), nebo procenta a napětí.
- **Poslední připojení**: Čas posledního úspěšného připojení k pumpě.
- **Poslední bolus**: Kdy byl vydán poslední bolus.
- **Základní bazál**: Toto je základní bazální dávka, která právě beží.
- **Dočasný bazál**: Dočasný bazál, který je právě spuštěn nebo je nulový.
- **Zásobník**: Kolik inzulínu je v zásobníku (aktualizováno nejméně každou hodinu).
- **Chyby**: Chyba, pokud existuje (většinou ukazuje, zda došlo k chybě v konfiguraci).

Ve spodní části máme 3 tlačítka:

- **Obnovit** pro obnovení stavu pumpy. To by mělo být použito až po dlouhé době bez připojení, protože tato akce resetuje data o pumpě (načtení historie, času, profilu, stavu baterie atd.).
- **Historie**: Zobrazí historii z pumpy (viz [níže](../Configuration/MedtronicPump#pump-history))
- **Statistiky RL**: Zobrazí statistiku RL (viz [níže](../Configuration/MedtronicPump#rl-status-rileylink-status))

## Historie pumpy

![Dialog Historie pumpy](../images/Medtronic03.png)

Historie pumpy se načítá každých 5 minut a ukládá se místně. Uchovává se pouze historie za posledních 24 hodin, takže při přidání nových položek jsou ty starší odstraněny. To je jednoduchý způsob, jak vidět historii pumpy (některé položky z pumpy se nemusí zobrazit, protože nejsou relevantní – například konfigurace funkcí, které nejsou používány programem AndroidAPS).

## Stav RL (Stav RileyLink)

![RileyLink Stav – Nastavení](../images/Medtronic04.png) ![Stav RileyLink – Historie](../images/Medtronic05.png)

Dialogové okno má dvě záložky:

- **Nastavení**: Zobrazí nastavení RileyLinku: Konfigurovaná adresa, Připojené zařízení, Stav připojení, Chyba připojení a verze firmwaru RileyLink. „Typ zařízení“ je vždy Medtronic, „model“ bude váš model, „sériové číslo“ je konfigurované sériové číslo, „frekvence“ udává, jakou frekvenci používáte, „poslední frekvence“ je poslední použitá frekvence.
- **Historie**: Zobrazuje historii komunikace, položky u RileyLink ukazují změny stavu pro RileyLink a položky Medtronic ukazují, které příkazy byly odeslány do pumpy.

## Akce

Je-li vybrán ovladač Medtronic, lze na kartu Akce přidat 3 možné akce:

- **Probudit a Naladit** - Pokud zjistíte, že AndroidAPS nekontaktoval vaší pumpu po nějakou dobu (měl by to dělat každých 5 minut), můžete vynutit Ladění. V tom případě se bude AndroidAPS snažit kontaktovat pumpu prohledáním všech dílčích frekvencí, na kterých lze pumpu kontaktovat. Pokud ji nalezne, nastaví ji jako výchozí frekvenci. 
- **Obnovit konfiguraci RileyLinku** - Pokud resetujete RileyLink/GNARL, musíte tuto akci použít, aby bylo možné překonfigurovat zařízení (sada frekvencí, sada typů frekvencí, kódování).
- **Vymazat blokování bolusu** - Když spustíte bolus, nastavíme blokování bolusu, které brání dalším příkazům, které by mohly být odeslány do pumpy. Pokud pumpu pozastavíte a znovu spustíte (chcete-li zrušit bolus), můžete toto blokování odstranit. Volba je tam jen tehdy, když je vydáván bolus... 

## Důležité poznámky

### OpenAPS users

When you start using AndroidAPS, primary controller is AndroidAPS and all commands should go through it. Sending boluses should go through AAPS and not be done on pump. We have code in place that will detect any command done on pump, but if you can you should avoid it (I think we fixed all the problems with pump history and AAPS history synchronization, but small issues still may arrise, especially if you use the "setup" as it was not intended to be used). Since I started using AndroidAPS with my pump, I haven't touched the pump, except when I have to change the reservoir, and this is the way that AndroidAPS should be used.

### Logging

Since Medtronic driver is very new, you need to enable logging, so that we can debug and fix problems, if they should arise. Click on icon on upper left corner, select Maintainance and Log Settings. Options Pump, PumpComm, PumpBTComm need to be checked.

### RileyLink/GNARL

When you restart RileyLink or GNARL, you need to either do new TuneUp (action "Wake and Tune Up") or resend communication parameters (action "Reset RileyLink Config"), or else communication will fail.

### CGMS

Medtronic CGMS is currently NOT supported.

### Manual use of pump

You should avoid manually doing treatments things on your pump. All commands (bolus, TBR) should go through AndroidAPS, but if it happens that you will do manual commands, do NOT run commands with frequency less than 3 minutes (so if you do 2 boluses (for whatever reason), second should be started at least 3 minutes after first one).

## Změna časového pásma a letní čas (Letní čas) nebo Cestování s Medtronic pumpou a AndroidAPS

Important thing to remember is that you should never disable loop when you are traveling (unless your CGMS can't do offline mode). AAPS will automatically detect Timezone changes and will send command to Pump to change time, when time on Phone is changed.

Now if you travel to East and your TZ changes with adding hours (ex. from GMT+0 to GMT+2), pump history won't have problem and you don't have to worry... but if you travel to West and your TZ changes by removing hours (GMT+2 to GMT-0), then sychronization might be little iffy. In clear text, that means that for next x hours you will have to be careful, because your IOB, might be little weird.

We are aware of this problem, and we are already looking into possible solution (see https://github.com/andyrozman/RileyLinkAAPS/issues/145), but for now, have that info in mind when traveling.

## Nejčastější dotazy

### Can I see the power of RileyLink/GNARL?

Ne. At the moment none of this devices support this and it probably won't even in the future.

### Is GNARL full replacement for RileyLink?

Yes. Author of GNARL added all functions used by Medtronic driver. All Medtronic communication is supported (at time of the writing (June/2019). GNARL can't be used for Omnipod communication. Downside of GNARL is that you have to build it yourself, and you have to have compatible version of hardware.

**Note from author:** Please note that the GNARL software is still experimental and lightly tested, and should not be considered as safe to use as a RileyLink.

### Where can I get RileyLink or GNARL?

Like mentioned before you can get devices here:

- RileyLink - Je možné získat zde - [getrileylink.org](https://getrileylink.org/).
- GNARL - Zde můžete získat informace, ale zařízení je třeba objednat jinde ([github.com/ecc1/gnarl](https://github.com/ecc1/gnarl)).

### What to do if I loose connection to RileyLink and/or pump?

1. Spusťte akci „Probouzení a ladění“. AAPS se pokusí najít správnou frekvenci pro komunikaci s pumpou.
2. Vypněte Bluetooth, počkejte 10 s a znovu zapněte. To vynutí opětovné připojení k RileyLinku.
3. Resetujte RileyLink. Poté, co to uděláte, nezapomeňte spustit akci „Reset RileyLink konfigurace“.
4. Zkuste body 3 a 2 dohromady.
5. Resetujte RileyLink a resetujte telefon.

### How to determine what Frequency my pump uses

![Pump Model](../images/Medtronic06.png)

If you turn your pump around in first line on right side you will see special 3 letter code. First two letters determine frequency type and last one determines color. Here are possible values for Frequency:

- NA - Severní Amerika (ve výběru frekvencí je třeba vybrat „US & Kanada (916 MHz)“)
- CA - Kanada (ve výběru frekvence je třeba vybrat „US & Kanada (916 MHz)“)
- WW - Worldwide (ve výběru frekvence je třeba vybrat „Worldwide (868 MHz)“)