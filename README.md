# Trend-spread
Simulation in NetLogo which is variation of epidemy. It shows how trend is spread in random and non-scale network with ability to attack or not attack hubs with many links.

## Project description in Czech:

### Úvod
V naší práci se zabýváme modelováním trendů. Model trendu je variací na model epidemie. Základní představa je ta, že chceme porovnat topologii dvou různých typů sítí na průběh šíření trendu. Prozkoumáváme, jaký průběh má šíření reklamy na náhodné a na bezškálové síti a zda se vyplatí při reklamě cílit na konkrétní huby s nejvíce spojeními, nebo je výsledek stejný jako když na náhodné síti rozprostřeme reklamu bez pravidel. 

Náhodná síť (random ER graph) je na začátku generovaná s nepropojenou sadou uzlů, kterým je přidělena stejná pravděpodobnost selekce. Taková náhodná síť má nízkou heterogenitu (většina uzlů má stejné číslo spojení), stupeň distribuce bude mít tvar Gaussovy křivky normálního rozložení. Náhodné sítě vytvořené dle ER algoritmu mají krátké průměrné cesty a nízkou míru shluků. 

Bezškálová síť (scale-free SF network) je charakterizována vysoce heterogenním stupněm distribuce, který umožňuje tzv. mocninný zákon (Barabasi & Albert 1999). Říká se jim bezškálové, protože přiblížení na jakoukoli část dané distribuce nezmění její celkový tvar: má několik významných uzlů s mnoha spojeními na každé úrovni zvětšení, o kterých v naší práci mluvíme jako o hubech. Takové sítě jsou typické pro stukturu, kterou má web, sémantické mapy nebo elektronické obvody. Struktura kombinuje náhodnost s heterogenitou, může mít nízkou nebo vysokou modularitu [1].

Formulace modelovaného problému 
Našim cílem bylo vytvořit model pro plánování marketingové kampaně s ohledem na typ zvolené sítě a její cílenost. Pro porovnání nejlepší strategie jsou naimplementovány dva typy výše popsaných sítí, náhodné a bezškálové. U obou sítí je pak možnost zapnutí napadání jen těch uzlů, které mají největší počet spojení, tedy hubů. Pro kontrolu je přítomen počet průměrného počtu stupňů na uzlech. 

V modelu jsou přítomny stupnice, u kterých můžeme ovlivňovat počet uzlů a počet jejich spojení. Počet spojení je nastaven jako minimální počet uzlů. Nastavitelná je i procentuální šance, že se trend od distributora rozšíří k dalšímu připojenému uzlu. Dále také šance, zda přijímající uzel trendu propadne. Konečně pak lze nastavit, kolik bude v počáteční fázi na síti uzlů, které šíří trend. 

### Popis zvoleného přístupu k modelování
Základní dynamika šíření trendu je postavená na modelu SIR (alias susceptible, ill a resistant). Pro lepší představu si náš abstraktní model vztáhneme na propagaci nově vydané knížky. V našem případě jsme si „susceptible“ vztáhly na normálního člověka, u kterého je možné, že si ve volném čase otevře knížku a začte se. „Ill“ je člověk, který knihu zrovna čte a dělí se o své poznatky se svým okolím (v každém kole se s určitou pravděpodobností pokusí nakazit všechny uzly, které jsou s ním spojeny). „Resistant“ je finální stádium. Je to čtenář, který již naši knížku dočetl a leží mu na poličce. „Resistant“ už k dalšímu šíření nepomáhají.

Přišlo nám zajímavé zkoumat, jak se šíření trendů liší na náhodné a bezškálové síti. Náhodná vzniká tak, že se vezmou všechny uživatelem zadaná spojení a uzly, a náhodně se spojí. Bezškálová začíná se dvěmi spojenými uzly a každý nový se připojuje na uzel, který musí být také připojený. Tento typ propojení více odpovídá většině sítí, se kterými se v běžném životě potkáváme. Pokud bychom chtěly náš model dát do kontextu reálného světa, mohly bychom použít například sociální sítě. Huby by v ní mohly představovat například fanouškovské stránky, uživatele mající blog o knížkách, youtubery a další uživatele s mnoha sledujícími.

### Verifikace modelu
Při verifikaci jsme ověřovaly, zda při všech možnostech nastavení uzlů je přístupná pouze hodnota spojení stejná nebo větší. Při postupném posouvání hodnoty uzlů jsme zjistily, že hodnota spojení občas přeskočí na číslo nižší, než je stanovené minimum. Tato vada je zřejmě způsobena softwarovou chybou, jelikož po překliknutí na posuvník se spojeními se číslo vrátí zpět na správnou pozici. Některé extrémní situace nejsou ošetřeny. Například po zadání příkazu s nulovým počtem uzlů a určitým počtem spojení program spadne. Při nastavení nulové hodnoty pro šanci šíření trendu se program chová korektně. Nakažené zůstanou pouze uzly, které byly na počátku a po určitém čase zešednou a stanou se rezistentními. Podobně se program chová při nastavení nulové šance propadnutí trendu. Žádný z uzlů se nestane rezistentní, nákaza trendem se bude šířit a uzly budou svítit žlutě.  Tato nastavení fungují stejně jak pro náhodnou, tak pro bezškálovou síť. 


### Ilustrace základního běhu modelu
Při nastavení modelu a zvolení typu sítě dojde k náhodnému pokrytí prostoru agenty, kteří jsou propojeni spojeními. Před spuštěním běhu je nastavitelný počet agentů obarven žlutou barvou. Tito agenti symbolizují distributory reklamy. Modré uzly symbolizují potenciální zákazníky. Každý žlutý agent má každý běh nějakou pravděpodobnost, se kterou trend rozšíří na sousedícího agenta a pravděpodobnost, že se z něj stane agent šedý. Šedý stav znamená, že podlehl trendu. 

![náhodná a neškílovitá síť](http://jyxo.info/uploads/C3/c30f097f713347915903b00cf383287dec7cdc5c.png)

### Analýza
V analytické části používáme data, která jsme získaly z NetLogo nástroje BehaviorSpace. Spustily jsme čtyři různé kombinace možností náhodná X bezškálová síť a iniciální napadnutí hubů X nenapadnutí hubů. Každou z těchto možností jsme odsimulovaly 1000x a zprůměrovaly hodnoty, které nám vyšly. Jako sledovanou hodnotu jsme si vybraly počet výskytů uzlů, které podlehly trendu (šedé barevné označení). Nastavení pro tuto simulaci obsahovalo 40 uzlů a mezi nimi 45 spojení.  Nakažené uzly byly na počátku vždy tři. Šance pro rozšíření trendu byla 2,3 % a pro již zasažený uzel byla každé kolo pravděpodobnost 2,1 %, že se stane rezistentní.

### Graf 1: Průběh počtu uživatelů, kteří podlehli trendu při jednotlivých bězích
![průběh šíření trendu](http://jyxo.info/uploads/CD/cd60fbfa4a3fade0fd246c6a6368bc24d5fe2cf8.png)

V grafu číslo 1 vidíme, že u náhodné sítě nehrálo počáteční nastavení, jestli cílit na huby nebo ne, příliš velkou roli. Rozdíl mezi attack_hubs? true a attack_hubs? false byl 1,95 uzlů, které v konečném důsledku podlehly trendu. U bezškálové sítě byl průběh relativně podobný, pokud nebyla použita možnost cílení reklamy. Pokud jsme se ovšem v počátku soustředily na huby, celý běh trval déle (126 ticků oproti 114 při attacka_hubs? false) a na konci přinesl více čtenářů. Při kombinaci bezškálové sítě a cílené reklamy jsme dostaly 15,85 čtenářů (o 3,57 oproti necílené).

Abychom si výsledky naší analýzy dokázaly představit na našem příkladu propagace knížky a zároveň ukázaly možné využití při plánování reklamní kampaně, určíme si, že prodejní cena jednoho výtisku je 200 Kč. Pokud bychom necílily reklamu na huby, cena počátečních nakažených uzlů je nízká. Řekněme, že náhodně oslovíme tři své přátele a za pozvání na pivo (30 Kč/ks) začnou knihu propagovat. V takovém případě by byl náš zisk 1764,46 Kč (počet „resistant“ na konci, kteří si zakoupili za 200 Kč knížku, mínus tři počáteční šiřitelé, kteří dostali každý 30 Kč a sami si knihu nekoupili.). V případě útočení na huby by se kniha rozšířila mezi více čtenářů. Při použití výše zmíněných hodnot a stejného výdělku bychom měly na cílenou reklamu k dispozici částku 804,6 Kč. Pokud by cena hubů byla nižší než 268,2 Kč na jednoho (což není nemožné, protože některé huby jsou ochotné například zrecenzovat knihu výměnou za její výtisk, jehož distributorská cena tuto částku nepřevýší), byly bychom v plusu oproti necílené reklamě.

### Zhodnocení závěrů simulace
V modelu jsme se zjišťovaly, jestli se vyplatí při marketingové kampani distribuovat produkt dle typu sítě náhodné a bezškálové spíše bez cílení na hlavní uzly, anebo se zaměřením na distributory. Nejhorších výsledku rozšíření reklamy dosáhla náhodná síť, která na významné uzly necílila a nejlépe dopadla síť bezškálová, která se zaměřovala na distribuci od hlavních uzlů. Běh vítězné kampaně také běžel nejdéle oproti všem ostatním. Sítě bezškálová bez napadání hlavních uzlů a náhodná s napadáním hlavních uzlů dopadly vzájemně velice podobně, přičemž bezškálová dopadla o něco lépe. 

Model samozřejmě simuluje ideální situaci, která není ohrožená žádnými vnějšími vlivy. Nedokáže tedy zohlednit mnoho takových vlivů, jako je jiný distributor se stejným produktem, ekonomická krize, roční období (období svátků, slev) nebo negativní marketingové kampaně jiného distributora vůči té naší. Velice zajímavé by pak bylo naimplementovat právě zmíněného oponenta na trhu a období svátků, kdy se prodej obecně navýší o desítky procent. 

Citace
[1] Nodus labs. Types of Networks: Random, Small-World, Scale-Free [online]. Special Agency Nodus Labs: ©2012 [cit. 25.5.2018]. Dostupné z: https://noduslabs.com/radar/types-networks-random-small-world-scale-free/
