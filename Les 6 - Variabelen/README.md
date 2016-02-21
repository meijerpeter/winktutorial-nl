#Skill Level 2#
#Les 6 - Variabelen#

##Het onthouden van getallen (en andere dingen)##
Laten we het eens hebben over de belangrijkste zaken in een programmeertaal. Het zijn de "variabelen". Laat de moeilijke naam je niet afschrikken. Wat het doet is redelijk eenvoudig. Een variabele is hetzelfde als een plakbriefje waarmee je een getal kan onthouden.

Stel je hebt de opdracht om te onthouden hoeveel vogels, eekhoorns en dinosauriers je buiten ziet gedurende een week. Ik zou dan mijn aantal vogels, eekhoorns en dinosauriers onthouden door middel van de plakbriefjes op de ramen. Op elk briefje staat dan de naam: "vogels", "eekhoorns" en "dinosauriers". Vervolgens kan ik de aantallen bijhouden op de plakbriefjes.

Computers onthouden de getallen op vergelijkbare manier, maar in plaats van plakbriefjes worden stukjes van het geheugen gebruikt. Een variabele is een manier op een stukje van het geheugen te gebruiken om een getal op te slaan, zodat je het later weer kan gebruiken.

Je kan een variabele bijna elke naam geven die je wil. Gewoonlijk neem je een naam die het getal het beste omschrijft. In ons geval is "vogels" een goede naam als je het aantal vogels wilt bijhouden die je deze week hebt gezien. Je zou ook gebruik kunnen maken van de variabele genaamd "vergetenSokken", dit zou niet echt handig zijn, maar het zou wel werken.

Laten we eens kijken naar een voorbeeld:

```c
 vogels = 10; //Het getal 10 wordt nu onthouden als variabele "vogels"
```

Bovenstaande regel code zal de alles verwijderen uit het stuk geheugen met de naam "vogels" en vervangen door het getal 10. Dit wordt ook wel een "toekenning" genoemd, zoals in "het getal 10 wordt aan de variabele "vogels" toegekend". Ervaren programmeurs zouden dit een "toekenningsoperatie" noemen, maar dat mag je voor nu vergeten.

Je kan ook het resultaat van een som in een variabele opslaan. Zie onderstaand voorbeeld...

```c
/*
 De tweede regel telt 2 bij 3 op, daarna wordt het resultaat hiervan opgeslagen 
 in "vogels". Het vorige getal van 10 wordt weggegooid en vervangen door een nieuwe waarde
 van 5.
*/
 vogels = 10; 	//Variabele vogels is nu 10
 vogels = 2 + 3; //Variabele vogels is nu 5
```

Als je wil kan je ook de variabele gebruiken in een berekening. Dit is meestal erg handig, bijvoorbeeld als je iets wil optellen. In het volgende voorbeeld geven we "birds" een startwaarde. In de tweede regel gebruiken we deze waarde in de variabele om er een berekening mee te doen en vervolgens het antwoord weer toe te kennen aan de variabele.

```c
/*
 De tweede regel neemt de waarde in de variabele "vogels", telt hier 1 bij op en kent het
 vervolgens weer toe aan vogels.
*/
 vogels = 10;		//Variabele vogels is nu 10
 vogels = vogels + 1;	//Variabele vogels is nu 11
```

##"Declareren" van variabelen##
Voordat je werkelijk de variabele voor het eerst kan gebruiken, moet je het programma van te voren vertellen dat je deze wil gaan gebruiken. Dit zorgt ervoor dat de processor van de computer een ruimte in het geheugen reserveert om de waarde die je aan de variabele toekent in op te slaan.

Het van te voren vertellen dat je een variabele gaat gebruiken heet "declareren". Dit is hetzelfde als je bijvoorbeeld knikkers wil gaan tellen, dan moet je eerst een briefje maken met de naam "knikkers", voordat je echt gaat tellen. Je kan een variabele maar een keer declareren.

```c
/*
 Dit is hoe je variabele "declareert". Je moet dit doen voordat je de variabele gaat 
 gebruiken.
*/ 
 int knikkers; //Dit is een variabele om knikkers op te tellen
```

Een variabele declaratie heeft minimaal 2 zaken nodig. Het eerste gedeelte vertelt wat voor "soort" variabele het is. Er zijn heel veel verschillende soorten variabelen die je kan declareren afhankelijk van wat je wilt opslaan. Het eerste gedeelte van de declaratie ("int" in dit geval) is het type van de gedeclareerde variabele, het tweede gedeelte ("knikkers" in dit geval) is de naam die je aan de variabele geeft.

Het soort "int" staat voor "integer" (dit is een Engels woord, niet te verwarren met het Nederlandse woord). Dit is een flexibele variabele soort en wordt veel gebruikt in Arduino programma's. De "int" variabele kan een geheel getal opslaan tussen de -32.786 en de 32.767. Je kan GEEN gebroken getallen (of komma-getallen) in een "int" opslaan.

Je kan een variabele bijna elke naam geven die je wil, zolang je maar een aantal simpele regels volgt:

1. Variabele namen kunnen bestaan uit kleine letters, hoofdletters, cijfers (0 t/m 9) en een "underscore" of liggend streepje (_). Andere karakters zijn niet toegestaan.

2. Variabele moeten beginnen met een letter of een underscore (_) karakter. Je kan de naam van een variabele niet beginnen met een cijfer. Als je een variabele naam toch wil laten beginnen met een cijfer, wordt gewoonlijk een underscore voor het cijfer gezet.

3. Spaties zijn niet toegestaan in de naam van een variabele. Alle karakters en cijfers moeten aan elkaar worden geschreven. Als je meerdere woorden wil gebruiken, wordt meestal de eerste letter van een nieuw woord met een hoofdletter geschreven.

4. Variabele namen kunnen maximaal uit 31 karakters bestaan. (In een aantal gevallen kunnen ze wel langer zijn, maar om verzekerd te zijn dat je code ook op andere platformen draait is dit maximum een veilige aanname).

5. De variabele kan niet worden genoemd naar bepaalde "gereserveerde woorden". Er zijn speciale woorden die iets betekenen voor de Arduino computer, zoals bijvoorbeeld "break". Als je dit als naam van de variabele typt en de kleur verandert op het scherm, dan is dit een goede aanwijzing dat dit een gereserveerd woord is en niet gebruikt kan worden. Je kan alsnog deze woorden gebruiken in een variabele naam, zolang het maar niet exact dat woord is. Als voorbeeld zou je wel een variabele "breakPoint" gebruiken, maar je zou het niet "break" kunnen noemen omdat dit iets speciaals betekent.

##Initiele waarde van een variabele##

Elke variabele bevat een waarde, zelfs direct nadat je het gedeclareerd hebt. Normaal gesproken zou dit nul zijn, maar dit is niet gegarandeerd. In de meeste gevallen wil je dat je programma de initiele waarde zet voordat je die daadwerkelijk gaat gebruiken. Tenzij je bijvoorbeeld de waarde van de lichtsensor in een variabele toekent, dan wordt de initiele waarde altijd overschreven. Maar in het andere geval, als je bijvoorbeeld wilt tellen hoeveel dinosauriers je deze week hebt gezien, dan wil je waarschijnlijk dat je begint op 0. Je kan de variabele een initiele waarde geven op hetzelfde moment als je de variabele declareert. Dat hoeft niet, maar is wel een goede gewoonte.

```c
/*
 Dit stukje code declareert de variabele loopCount (aantal keren door de loop functie) 
 en kent het gelijk een initiele waarde toe.
*/
int loopCount = 0;	//Declareert loopCount en kent de initiele waarde van 0 toe
```

##Een werkend voorbeeld##

Laten we eens kijken naar een werkend voorbeeld. Dit is vergelijkbaar met de voorbeelden die je eerder hebt gezien. Het declareert de variabele 'loopCount' en kent het een startwaarde van 0 toe. Daarna gaat de `loop()` functie beginnen. Elke keer als de functie weer opnieuw begint, wordt `loopCount` opgehoogd met 1. Het is logisch dat we deze variabele "loopCount" hebben genoemd, omdat dit exact is wat we bedoelen; "loop" betekent "herhalen" en "count" betekent "tellen", dus we tellen hoe vaak de `loop()` functie is begonnen.

```c
#include WinkStuff.h

void setup(){
  hardwareBegin();
}

int loopCount = 0;	//Declareer de variabele loopCount en zet deze op 0

void loop(){
  loopCount = loopCount + 1; //Tel 1 op bij de huidige waarde van loopCount
} //einde van de loop()
```

Als je dit upload naar je Wink, lijkt het alsof het programma niets doet, maar in feite is de Wink alleen maar zo snel als mogelijk aan het tellen hoe vaak de de `loop()` functie wordt afgespeeld. In de volgende les zullen we laten zien hoe je deze waarde op je computerscherm kan afdrukken om te zien wat de Wink "denkt". Dit is alleen een simpel voorbeeld om te laten zien hoe je een variabele kan gebruiken.

##Een paar weetjes over variabelen##
Hier zijn nog een paar weetjes over variabelen die handig zijn om te weten.

*Omrollen:* Een variabele zal "omrollen" als je het een waarde geeft buiten de grens die het kan opslaan. Bijvoorbeeld, als je de variabele de hoogste waarde toekent die mogelijk is en je telt er 1 bij op, dan zal de waarde "omrollen" en wordt het de laagste waarde die het kan opslaan. Dit werkt op dezelfde manier bij een negatief getal, dan wordt het de vervolgens hoogste waarde die het kan opslaan.

Als je ooit met een programma werkt waarbij de variabelen vreemde waarden aannemen, dan zou het "omrollen" wel eens de oorzaak kunnen zijn. De taal C (waarin de Arduino wordt geprogrammeerd) zal niets doen om het omrollen te voorkomen, het laat het aan jou om deze fout te maken.

```c
 int x;
 x = -32768;
 x = x - 1;	// x heeft nu de waarde 32.767 - is omgerold in de negatieve kant
 
 x = 32767;
 x = x + 1; // x heeft nu de waarde -32768
```
> Source: Official Arduino Website (https://www.arduino.cc/en/Reference/Int)

*Geheugen limiet:* Misschien had je jezelf al afgevraagd hoeveel variabelen je kan declareren. Dit hangt af van de hoeveelheid geheugen die je beschikbaar hebt op de Arduino processor die je gebruikt. De Wink heeft 2 KB RAM geheugen (dat is ongeveer 2000 bytes). Elke "int" heeft 2 bytes nodig, dus in principe zou je 1000 verschillende "int" variabelen kunnen gebruiken. Maar, de Arduino, samen met de achtergrond code van de Wink (in WinkStuff.h) gebruikt al 300 bytes van de beschikbare 2000 bytes, dus dat laat nog genoeg ruimte over voor je eigen programma (ongeveer 1700 bytes dus 850 "int" variabelen).

Het is onwaarschijnlijk dat je niet voldoende geheugen hebt op de Wink. De enige keer dat je tegen de geheugen grens aanloopt is als je grote "arrays" gaat gebruiken (dat is een skill level 3 onderwerp, dus daar hoef je nu geen zorgen om te maken).

*Geheugen hergebruik:* Hou goed in gedachten dat elke keer als je een programma upload naar de Wink, al het geheugen wordt gewist en opnieuw wordt gebruikt. (Behalve voor een speciaal soort geheugen die EEPROM wordt genoemd, die onthoudt de waarden voor eeuwig - dit wordt later behandeld). Voor nu, onthoud dat je het geheugen continu opnieuw kan overschrijven. Als je veel variabelen gebruikt in een sketch dan hoef je je geen zorgen te maken dat je tegen de limiet van je geheugen aanloopt. 

##Andere soorten variabelen##
We hebben eerder gezegd dat er verschillende soorten variabelen zijn, die zullen we hier kort behandelen. Er zijn er nog veel meer, maar dit zijn de voornaamste die je het meest nodig zult hebben.

| Soort variabele | Waarden reeks | Bits | Omschrijving |
|-----------------|---------------|------|--------------|
| byte            | 0 tot 255     | 8    | Nummer van 0 tot 255, geen negatieve nummers toegestaan |
| char            | =128 tot 127  | 8    | Sommige compilers zullen dit interpreteren als een karakter (zoals een letter op je toetstenbord)|
| word            | 0 tot 65535   | 16   | Dit kan hogere waardes bevatten dan "int", behalve dat je geen negatieve waardes kan opslaan |
| int             | -32768 tot 32767 | 16 | Dit is het meest gebruikte soort variabele. Het kan zowel grote positieve als negatieve getallen opslaan |
| unsigned long   | 0 tot 4.294.967.295 | 32 | Dit soort variabele is nodig om het resultaat van de functie `millis()` op te slaan, zodat je kan zien hoe lang het programma heeft gedraaid. |
| long            | -2.147.483.648 tot 2.147.483.647 | 32 | Handig om hele grote getallen mee op te slaan die zowel positief als negatief kunnen zijn |
| float           | -3.4028235 e38 tot 3.4028235 e 38 | 32 | De "Floating Point" datatype kan zeer grote getallen opslaan, zowel geheel als gebroken. Het is een zeer flexibel, maar de processor heeft meer tijd nodig dan de andere soorten. Gebruik float data alleen wanneer je getallen nodig hebt met een gedeelte achter de komma. |

*Opmerking over de variabele Bits-lengte:* Je hebt gezien dat in de tabel "Bits" worden genoemd. We gaan wat dieper hierop in in de volgende lessen, maar hier komt toch een kleine introductie. Computers slaan waardes op in achtereenvolgende 1-en en 0-en. De "byte" variabele kan in een keer een serie van acht 1-en en 0-en opslaan, vandaar dat we zeggen dan deze "8-bits lang" is. Om grotere getallen op te slaan, zoals het soort variabele `word`, dan is 8-bits niet genoeg. Dan hebben we een serie nodig van zestien 1-en en 0-en om een `word` op te slaan. Een `float` variabele heeft genoeg ruimte om achtereenvolgens twee-en-dertig 1-en en 0-en op te slaan.

Voor nu maakt het niet veel uit in onze voorbeelden, maar weet dat het brein van de Wink (en alle andere 8-bit processoren) alleen 8-bits informatie tegelijkertijd kan verwerken. Meestal verwerkt de Wink het optellen van een paar van 8-bit getallen in 1 cyclus. De Wink kan ook 16-bit cijfers optellen, maar moet deze opbreken in 8-bits per cyclus, en om berekeningen van 32-bits uit te voeren moeten deze in een aantal cycli worden uitgevoerd. De Wink voert 8 miljoen (!) cycli per seconden uit, dus zelfs het rekenen met 32-bit getallen gaat zeer snel....

In het algemeen geldt dat het een goed idee is bij 8-bit variabelen te blijven, als tweede keus 16-bit variabelen te kiezen, en de 32-bit getallen alleen te gebruiken wanneer je ze echt nodig hebt.

> Learn to Code - Ch06 Rev01.1 ~ Plum Geek