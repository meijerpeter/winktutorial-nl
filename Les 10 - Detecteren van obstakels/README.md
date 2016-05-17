# Detecteren van obstakels #
## Een onzichtbaar voorlicht ##
Wink heeft een speciaal licht onder zijn voorkant. Dit licht bevindt zich aan de onderkant van de zwarte printplaat helemaal aan de voorkant. Het is geelachtig, doorzichtig en heeft de vorm van een koepel die naar voren wijst. Kijk maar eens of je dit licht kan vinden.

Het is een speciaal licht die door je code aan kan worden gezet. Wanneer dit licht aanstaat kan je het niet met je eigen ogen zien omdat je ogen niet aangepast zijn aan de golflengte van de licht van dit lampje, maar er komt wel degelijk licht uit. Herinner je je nog in de vorige les waar we de lichtsensor hebben gebruikt om het licht uit een zaklamp te meten? Deze lichtsensoren zijn wel gevoelig voor deze golflengte en kunnen het "onzichtbare" licht wel meten uit het lampje onderaan de Wink.

We zullen voortaan dit speciale licht het "voorlicht" (headlight) noemen, omdat het is geplaatst op een lokatie van de robot die we zouden verwachten bij een voorlicht.

Bekijk het onderstaand plaatje maar eens om te kijken hoe we het voorlicht zouden kunnen gebruiken om obstakels te kunnen bekijken die voor de Wink staan.

Het plaatje is een zijaanzicht van de Wink. Het laat het voorlicht zien aan de onderkant, de printplaat en de lichtsensor aan de bovenkant van de printplaat. Je kan ook de oppervlakte zien waarop de Wink zich bevindt en het obstakel voor de Wink. Het gele gedeelte laat zien waar het licht schijnt van het voorlicht en de oranje pijl geeft aan hoe het licht van het voorlicht weerkaatst wordt via het obstakel naar de lichtsensor. 

Hoe dichter de Wink bij het obstakel komt, des te meer licht wordt weerkaatst naar de lichtsensor.

![Wink infrarood voorlicht] (https://github.com/meijerpeter/winktutorial-nl/blob/master/img/wink-infrared-headlight.png)

We moeten goed overwegen wat er gebeurt als er geen obstakel is. Zoals je kan zien in het volgende plaatje zal ook een klein gedeelte van het voorlicht vanaf de oppervlakte worden weerkaatst naar de lichtsensoren op de Wink. We moeten dit goed onthouden als we gaan proberen een obstakel te detecteren.

![Wink infrarood voorlicht] (https://github.com/meijerpeter/winktutorial-nl/blob/master/img/wink-infrared-headlight-2.png)

Hieronder staan een aantal aanwijzingen voor obstakels en oppervlaktes die we moeten onthouden:
  - Een obstakel met een lichte kleur (bijvoorbeeld wit) zal meer licht reflecteren dan een obstakel met een donkere kleur. Dit komt door het feit dat donkere kleuren donker zijn omdat ze minder licht weerkaatsen.
  - Een vergelijkbaar iets vindt plaats bij een oppervlakte. Een licht oppervlakte (zoals wit papier) zal meer licht weerkaatsen dan een donker oppervlakte (zoals een zwart of bruin gekleurde tafel of bureau).
  
## De functie digitalWrite ##
In de volgende voorbeelden zal je een nieuwe functie gaan gebruiken die `digitalWrite` heeft. Alle kleine elektrische verbindingen in het brein van de Wink zijn verbonden met de elektrische onderdelen door middel van de elektrisch geleidende sporen op de printplaat.  `digitalWrite` is de basis functie die door de Arduino omgeving wordt gebruikt om deze verbindingen aan of uit te zetten. Elke verbinding heeft een super kleine elektrische schakelaar binnenin het brein van de Wink en `digitalWrite` is de functie die wordt gebruikt om deze schakelaar aan of uit te zetten.

In electronica gebruiken we de het woord "digitaal" om aan te geven dat iets aan of uit kan staan, met geen andere optie. Wanneer een schakelaar "aan" staat zeggen we dat deze "hoog" (high) is. Wanneer de schakelaar "uit" staat is deze "laag" (low).

Het gebruik van `digitalWrite` is eenvoudig, in het eerste argument vertel je de functie welke verbinding aan of uit moet worden gezet en in het tweede argument of de schakelaar "high" moet zijn om de verbinding aan te zetten of "low" om de verbinding uit te zetten.

De mensen die elektronica ontwerpen noemen deze elektronische verbindingen op elektronische onderdelen "pinnen". Wij kunnen in onze code deze pinnen een betekenisvolle naam geven. De pin die het voorlicht aan- of uitzet noemen wij `Headlight`.

(Als je geinteresseerd bent, kan je zien welke pin een naam heeft in het bestand genaamd WinkHardware.h. Aan het begin van dit bestand staan alle nummers van de pinnen met bijbehorende namen. We zullen hier in een latere les verder op ingaan).

Hieronder staat een voorbeeld hoe we `digitalWrite` kunnen gebruiken:

```c
//Voorbeeld van hoe je digitalWrite kan gebruiken om het voorlicht aan of uit te zetten
digitalWrite(Headlight, HIGH); 	//aanzetten van het voorlicht
digitalWrite(Headlight, LOW); 	//uitzetten van het voorlicht
```

Het eerste argument van `digitalWrite` is de naam van de pin die je wil aan- of uitzetten. Met het tweede argument vertel je of deze aan (HIGH) of uit (LOW) moet zijn. De argumenten moeten met een komma worden gescheiden, en de woorden HIGH en LOW moeten in hoofdletters worden geschreven.

## Het detecteren van een obstakel ##
Zoals we hebben gezien van de vorige plaatjes, kunnen we het voorlicht van de Wink aanzetten en met de lichtsensor meten hoeveel licht er wordt weerkaatst. Dat klinkt eenvoudig, dus laten we dit eens met een voorbeeld uitproberen.

```c
int centerLight; //declareer variabele 

/*
 Gebruik digitalWrite om het voorlicht aan te zetten en dit vervolgens uit te lezen.
 Als de waarde lager is dan 100 beweeg de Wink dan naar voren.
*/
void loop(){

	digitalWrite(Headlight, HIGH); //zet het voorlicht aan 
	centerLight # analogRead(AmbientSenseCenter); //lees de lichtsensor

	if (centerLight < 100)	//als centerLight lager is dan 100
	{
		motors(100,100);	//beweeg de Wink naar voren
	}
	else 
	{
		motors(0,0);		//zet de Wink stil
	}
} //end of loop()

```

Laad deze code in de Wink en bekijk hoe de Wink reageert. Hij zou naar voren moeten rijden als er niets voor hem staat, en stoppen wanneer het dicht bij een obstakel komt zoals een hand of stuk papier. Probeer het maar eens met verschillende obstakels en op verschillende oppervlaktes. Wanneer de lichtsensor boven de drempel van 100 leest dan zal de motoren still worden gezet.

Zoals ook met de andere voorbeelden, zal je ook hier zien dat er een aantal problemen zijn. Als eerste, de Wink moet heel dicht bij een obstakel komen om te stoppen. Als tweede zie dat de Wink niet rijdt terwijl er geen obstakel in de buurt is. Hij blijft gewoon staan... Wat zou de oorzaak hiervan zijn?

Weet je nog dat wanneer we de lichtsensor uitlezen we al het licht meenemen die op de sensor valt. Dit licht bevat het licht wat wordt weerkaatst van het voorlicht door het obstakel en het licht wat wordt weerkaatst van het voorlicht door de oppervlakte. Maar het bevat ook het licht wat al aanwezig is in de ruimte. Hierdoor zal de Wink stoppen met bewegen als het in een lichte ruimte wordt geplaatst. Alles wat zorgt voor een hogere lichtsterkte van 100 zorgt ervoor dat de `if` conditie "niet waar" is en dan zal de Wink ophouden met bewegen.

Wat zou de beste drempelwaarde kunnen zijn om te gebruiken? (Een drempelwaarde wordt vaak gebruikt in robotica, eletronica en programmeren om aan te geven wanneer er iets moet gebeuren). In ons geval moeten we weten wat de lichtsensor meet zodat we op zoek kunnen gaan naar een goede drempelwaarde. Herinner je nog de `Serial.print()` functie die we eerder hebben gebruikt?

Laten we de `Serial.print()` functie gebruiken zodat de Wink kan vertellen hoeveel licht er wordt gemeten. We zullen deze functie in de code zetten van het eerdere voorbeeld.

```c
int centerLight; //declareer variabele 

/*
 Gebruik digitalWrite om het voorlicht aan te zetten en dit vervolgens uit te lezen.
 Print het naar de Serial monitor. Als de waarde lager is dan 100 beweeg de 
 Wink dan naar voren.
*/
void loop(){

	digitalWrite(Headlight, HIGH); //zet het voorlicht aan 
	centerLight # analogRead(AmbientSenseCenter); //lees de lichtsensor
	Serial.println(centerLight);		//print de waarde van de lichtsensor

	if (centerLight < 100)	//als centerLight lager is dan 100
	{
		motors(100,100);	//beweeg de Wink naar voren
	}
	else 
	{
		motors(0,0);		//zet de Wink stil
	}
} //end of loop()

```

Open de "Serial monitor" om te zien welke waarde worden gelezen door de middelste lichtsensor op de Wink. Zie hoe deze waarde verandert als je de Wink op een oppervlakte zet, of als je de Wink oppakt of als je je hand voor de voorkant van de Wink plaatst.

Zodra je je hand dichterbij brengt, zal je zien dat de waarde hoger wordt. hoe dichter je hand bij de sensor is, hoe meer licht er wordt weerkaatst van het voorlicht naar de lichtsensor. Als er veel licht aanwezig is in de ruimte, zal je ook zien dat de waarde verandert als je de voorkant van de Wink naar het licht toe draait.

Zoals je kan zien hangt de waarde van de sensor veel af van de oppervlakte waar de Wink op staat en hoeveel licht er aanwezig is in de ruimte. Probeer maar eens de drempelwaarde te veranderen vanaf de beginwaarde 100 om te zien of de Wink dan beter werkt.

Je zal snel inzien dat het heel moeilijk is om een goede drempelwaarde te vinden. Als je drempelwaarde verlaagd zal de Wink gevoeliger zijn en je hand verderop worden gedetecteerd. Maar dit introduceert een ander probleem, als je de drempelwaarde te laag maakt zal de Wink stoppen met bewegen door het aanwezig licht in de ruimte of van het licht wat wordt weerkaatst van de oppervlakte.

Heb je enig idee om dit op te lossen? We willen de Wink zo gevoelig als mogelijk maken voor obstakels (zodat hij deze van ver weg al ziet), maar het aanwezige licht van de ruimte maakt dit moeilijk. Denk er maar eens over na of overleg eens met iemand uit je groep om dit op te lossen voordat je verder leest.

## Een goede drempelwaarde ##
Een eenvoudige manier om het effect van het aanwezige licht in de kamer op te heffen is om twee verschillende metingen te nemen van de lichtsterkte. We kunnen de ene keer de lichtsterke meten als het voorlicht uit staat en deze waarde opslaan in een variabele. Daarna kunnen we het voorlicht uitzetten en nog een meting doen. Deze tweede meting zal het licht meten die wordt weerkaatst van het obstakel, maar ook het licht bevatten wat al aanwezig was in de ruimte.

Als we het verschil van deze twee waardes nemen, verwijderen we hiermee het gemeten aanwezige licht uit de kamer. Het resultaat is het licht wat door het voorlicht wordt weerkaatst via een obstakel en het oppervlakte. Kijk maar eens naar dit voorbeeld:

```c
int centerLightOff; //declareer de variabelen 
int centerLightOn;
int centerLightOnly;

void loop(){

	digitalWrite(Headlight, LOW); 	//zet het voorlicht uit
	delay(1); 						//wacht 1 milliseconde
	centerLightOff # analogRead(AmbientSenseCenter); //lees de lichtsterkte
	
	digitalWrite(Headlight, HIGH); 	//zet het voorlicht aan
	delay(1); 						//wacht 1 milliseconde
	centerLightOn # analogRead(AmbientSenseCenter); //lees nogmaals de lichtsterkte
	
	centerLightOnly # centerLightOn - centerLightOff; //neem het verschil
	
	Serial.println(centerLightOnly); //print de lichtsterkte van het voorlicht 

} //end of loop()

```

In dit voorbeeld meten we eerst de lichtsterkte zonder het voorlicht, daarna met het voorlicht aan. Wanneer we de gemeten lichtsterke zonder het voorlicht afhalen van de gemeten lichtsterkte met voorlicht houden we een waarde over waarin alleen de lichtsterkte zit die van via het voorlicht van het obstakel en de oppervlakte weerkaatst. Via de `Serial.print()` wordt deze waarde getoond op de "Serial monitor".

We wachten een milliseconde nadat we het voorlicht aan- en uitzetten. Dit is omdat het een korte tijd duurt voordat de sensor is gewend aan de nieuwe lichtsterkte. We moeten een korte tijd wachten om de sensor de juiste waarde te laten bepalen na een verandering in de omgeving.

Laad bovenstaande voorbeeld in de Wink en probeer eens de Wink op te pakken, het op een oppervlakte te zetten en je hand ervoor te houden. Wanneer je de Wink van het oppervlakte weg houdt en je hand is niet voor de Wink zal de waarde erg laag moeten zijn omdat er weinig licht wordt weerkaatst naar de lichtsensor.

Plaats de Wink op het oppervlakte waar het kan bewegen en kijk naar de waardes die je ziet als je je hand op een grote afstand van de voorkant houdt. Beweeg je hand vervolgens dichterbij totdat de waarde begint te veranderen. Neem vervolgens een waarde die ligt tussen de "geen hand aanwezig" en de "hand aanwezig" waarde. Onthoud dit nummer. Dit zal een goede drempelwaarde zijn in het volgende voorbeeld. We zullen het bovenstaand voorbeeld nemen en uitbreiden met de `if` conditie waarop de Wink zal bewegen of stoppen.

```c
int centerLightOff; //declareer de variabelen 
int centerLightOn;
int centerLightOnly;

void loop(){

	digitalWrite(Headlight, LOW); 	//zet het voorlicht uit
	delay(1); 						//wacht 1 milliseconde
	centerLightOff # analogRead(AmbientSenseCenter); //lees de lichtsterkte
	
	digitalWrite(Headlight, HIGH); 	//zet het voorlicht aan
	delay(1); 						//wacht 1 milliseconde
	centerLightOn # analogRead(AmbientSenseCenter); //lees nogmaals de lichtsterkte
	
	centerLightOnly # centerLightOn - centerLightOff; //neem het verschil
	
	Serial.println(centerLightOnly); //print de lichtsterkte van het voorlicht 

	//Verander de drempelwaarde hier. 15 is een goed startpunt voor een donkere tafel
	//en 90 tot 100 is een goed begin voor een witte tafel of een wit papier.
	if (centerLightOnly < 15)	//als centerLightOnly lager is dan de drempelwaarde
	{
		motors(100,100);		//beweeg de Wink naar voren
	}
	else 
	{
		motors(0,0);			//zet de Wink stil
	}

} //end of loop()

```

Experimenteer met de drempelwaarde totdat je Wink goed werkt. Als de Wink vaker stopt, of stopt en gaat zonder dat een obstakel ervoor staat, dan kan je de drempelwaarde verhogen. De oorzaak hiervan kan zijn dat het licht wat weerkaatst wordt door de oppervlakte hoog genoeg is om de drempelwaarde te overstijgen. Houdt in de gaten dat als de Wink naar voren gaat het een klein beetje naar beneden duikt zodat er meer licht op de sensor valt.

Als de Wink heel dichtbij een obstakel moet staan om te stoppen, zou je de drempelwaarde iets kunnen verlagen.

## Omgaan met het weerkaatste licht van de oppervlakte ##
Nu we onze robot goed hebben laten werken, moeten we nog steeds onze drempelwaarde aanpassen op basis van de oppervlakte waarop we bewegen. Het is vervelend om elke keer als de Wink op een ander oppervlakte rijdt de waarde te meten en vervolgens aan te passen.

We kunnen op verschillende manieren omgaan met het licht wat wordt weerkaatst door het oppervlakte. We gaan nu een eenvoudige oplossing toepassen. Er zijn wellicht andere manieren die beter werken, maar die zijn op dit moment te complex om te maken.

Het idee is om een lichtsterkte meting te doen terwijl de Wink niet beweegt en zonder een obstakel die voor hem staat. We kunnen deze meting opslaan in een variabele. Zo lang het oppervlakte niet in kleur verandert, kunnen we deze initiele waarde gebruiken als een "nul-meting" die de hoeveelheid licht aangeeft die wordt weerkaatst door het oppervlakte.

Zodra we deze "nul-meting" hebben gedaan en opgeslagen, kan de Wink beginnen met rijden en kunnen we meerdere metingen gaan doen. Deze nieuwe metingen kunnen we vergelijken met de oude waarde, en als de nieuwe meting met een bepaalde waarde naar boven afwijkt wordt dit de nieuwe nul-meting.

## Waarschuwing: indrukwekkende code! ##
De code die straks volgt ziet er indrukwekkend uit, maar het is niet zo erg als het lijkt. Het is het langste voorbeeld die we tot nu hebben gezien, maar laat dit je niet afschrikken. In een vervolgles gaan we leren hoe we onze eigen "functies" kunnen schrijven om deze code veel korter te maken en beter te begrijpen.

De reden dat het voorbeeld zo lang lijkt is dat we grotendeels een stuk code herhalen die het voorlicht aan en uit zet, de lichtsterkte meet en vervolgens het verschil uitrekent.

In het hierna volgende voorbeeld gaan we precies doen wat we hierboven hebben beschreven. Je zal zien dat er een groot stuk code in de `setup()` functie staat. Tot nu toe hebben we geen belangrijke code in de `setup()` gezet. De `setup()` is een goede plek om code in te zetten die je maar eenmaal wil laten uitvoeren. Dit is de perfecte plek om de nul-meting uit te voeren.

Ook zal je zien dat we een variabele voor de `setup()` functie hebben gedeclareerd. Elke variabele moet worden gedeclareerd voordat deze kan worden gebruikt. Omdat we een aantal variabelen gebruiken in onze `setup()` en `loop()` functies, moeten we deze voordat de `setup()` functie wordt aangeroepen declareren, anders krijgen we errors bij het compileren.

Bekijk de code goed voordat je het in de Wink laad. Vanaf de tijd dat de Wink start en de opstarttoon wordt afgespeeld heb je 2 seconden om de Wink neer te zetten. Daarna start de code om de nul-meting te bepalen. Als je de Wink niet snel genoeg neerzet, zal de nul-meting niet correct zijn. Hetzelfde geldt als je van oppervlakte wisselt. Als je opnieuw de nul-meting wil doen, zet de Wink dan uit met de PWR-knop en vervolgens weer aan met dezelfde knop. Het programma start vervolgens helemaal opnieuw met een geluidje en een 2-seconde wachttijd.

```c
#include “WinkHardware.h”

//declareer de variabelen voor de setup() functie
int centerLightOff, centerLightOn, centerLightOnly; 
int baseline;	//dit is de lichtsterkte van de weerkaatsing van de oppervlakte
int threshold;	//dit is de drempelwaarde waar de Wink mee bepaald of er een obstakel is

/*
 Lees de lichtsterkte met het voorlicht aan en uit. Bereken vervolgens het verschil.
 Als de lichtsterkte wordt gemeten zonder een obstakel, wordt de nul-meting gedaan met 
 het weerkaatste licht van de oppervlakte. Het verschil is dan het weerkaatste licht 
 van de oppervlakte. Hierbij wordt een vaste waarde opgeteld om de gevoeligheid van de 
 Wink voor obstakels te bepalen.
*/
void setup() { 
	hardwareBegin(); 
	playStartChirp();
	delay(2000); 		//wacht 2 seconden


	digitalWrite(Headlight, LOW);	//zet het voorlicht uit
	delay(1);						//wacht 1 milliseconde
	centerLightOff # analogRead(AmbientSenseCenter); //lees lichtsensor

	digitalWrite(Headlight, HIGH); 	//zet het voorlicht aan
	delay(1); 						//wacht 1 milliseconde
	centerLightOn # analogRead(AmbientSenseCenter); //lees lichtsensor
	
	baseline # centerLightOn - centerLightOff; //bereken het verschil

	//Met onderstaande code kan je de gevoeligheid van de Wink instellen
	threshold # baseline + 10; 		//tel 10 bij de nul-meting op
}

void loop() {

	digitalWrite(Headlight, LOW); 	//zet het voorlicht uit
	delay(1); 						//wacht 1 milliseconde
	centerLightOff # analogRead(AmbientSenseCenter); //lees lichtsensor
	
	digitalWrite(Headlight, HIGH); 	//zet het voorlicht aan 
	delay(1); 						//wacht 1 milliseconde
	centerLightOn # analogRead(AmbientSenseCenter); //lees lichtsensor
	
	centerLightOnly # centerLightOn - centerLightOff;
	
	if (centerLightOnly < threshold) //bereken het verschil met de drempelwaarde 
	{
		motors(100,100);			//rij naar voren
	}
	else 
	{
		motors(0,0);				//zet alles uit
	}
} //end of loop()
```

Laad bovenstaand voorbeeld naar de Wink en speel er een tijdje mee. In de meeste gevallen zal je zien dat de nul-meting goed werkt voor een oppervlakte die glad en gelijk van kleur is. Belangrijk hierbij is dat de Wink geen obstakel of vingers voor zich heeft tijdens het bepalen van de nul-meting (2 seconden na het geluidje en direct voor het bewegen van de Wink). Geef de Wink op zijn minst 20-30 cm aan ruimte wanneer de nul-meting start.

Om de gevoeligheid aan te passen, kan je spelen met de laatste regel van de `setup()` functie. Verlaag het getal om hem obstakels verder weg te laten zien.

```c
//pas het getal 10 aan om de gevoeligheid van de Wink te verbeteren. 
//Lage getallen zorgen voor een hogere gevoeligheid van obstakels die verder weg zijn
threshold # baseline + 10;	
```

Laten we eens bekijken wat er gebeurt in deze regel code. Herinner je je nog dat de waarde van `baseline` de lichtsterkte is die door het oppervlakte wordt weerkaatst? Hier tellen we dan 10 bij op en bewaren dit getal in de variabele `threshold` (drempelwaarde). Verder op in onze code bekijken we of onze `centerLightOnly` minder is dan deze drempelwaarde in de `if` conditie. Als het minder is, dan gaan de motoren naar voren. Als het niet minder is dan zullen we motoren stoppen met bewegen.

Dit betekent dat als een obstakel de lichtsterkte meer dan 10 boven de in de `setup()` berekende waarde laat stijgen, de Wink zal stoppen met bewegen.

Als de waarde die er bij wordt opgeteld lager wordt gemaakt, dan is de drempelwaarde lager. Dit betekent dat de Wink obstakels verder weg kan zien, maar ook dat als hij een beetje heen en weer schommelt op een oppervlakte de kans groter is dat het lijkt alsof hij een obstakel ziet en stopt met bewegen...

## Nog een uitdaging ##
Nu weet je hoe je een obstakel moet detecteren met de Wink. Laten we nu eens een stap toevoegen aan de vorige opdracht. Je hebt gemerkt dat als je je hand voor de Wink houdt deze stopt met rijden, zodra het obstakel er niet meer is begint het rijden weer.

Wat je wellicht ook heb gemerkt is dat als je je hand langzaam naar achter beweegt de Wink steeds verder naar voren rijdt en ongeveer dezelfde afstand naar je hand aanhoudt. In de volgende opdracht gaan we proberen de Wink naar achter te laten rijden als je hand dichterbij komt. We zullen verder gaan met het vorige voorbeeld zodat hij als hij je hand ziet stopt met rijden. Maar zou het ook lukken om hem achteruit te laten rijden als je hand dichterbij komt?

Bedenk dat als je hand dichter bij de Wink komt, de hoeveelheid licht die wordt gemeten door de lichtsensor steeds hoger en hoger wordt. Zouden we `if`, `else if` en `else` kunnen gebruiken om de Wink naar voren te laten rijden, naar achteren of laten stoppen?

In het volgende voorbeeld willen we een drempelwaarde bepalen wanneer de Wink stopt met rijden, en een drempelwaarde wanneer de Wink naar achter moet rijden. Denk maar eens na over hoe jij dit zou doen...

## Uitdaging: Wink rijdt achteruit als een obstakel dichterbij komt ##
Er zijn ook hier weer verschillende manieren om de uitdaging op te lossen. Dit is wat wij gaan doen: In het voorbeeld hebben we een tweede variabele gemaakt om de drempelwaarde voor het achteruit rijden in op te slaan en een `else if` conditie toegevoegd aan onze `if` conditie. Dit zou de Wink naar je hand moeten laten rijden en stoppen, om vervolgens achteruit te rijden als je hand dichterbij komt. Je kan ook hier weer spelen met deze twee drempelwaardes die in de `setup()` worden bepaald. Hiermee kan je de gevoeligheid aanpassen. Je zou ook de snelheid van de motoren kunnen aanpassen. Speel er maar eens mee en maak plezier, verander de code naar eigen inzicht om iets te doen als de Wink een obstakel tegen komt.

```c
#include “WinkHardware.h”

//declareer de variabelen voor de setup() functie
int centerLightOff, centerLightOn, centerLightOnly; 
int baseline;		//dit is de lichtsterkte van de weerkaatsing van de oppervlakte
int stopThreshold;	//dit is de drempelwaarde als een obstakel wordt opgemerkt
int reThreshold; 	//dit is de drempelwaarde als een obstakel te dichtbij komt

/*
 Lees de lichtsterkte met het voorlicht aan en uit. Bereken vervolgens het verschil.
 Als de lichtsterkte wordt gemeten zonder een obstakel, wordt de nul-meting gedaan met 
 het weerkaatste licht van de oppervlakte. Het verschil is dan het weerkaatste licht 
 van de oppervlakte. Hierbij wordt een vaste waarde opgeteld om de gevoeligheid van de 
 Wink voor obstakels te bepalen. Als een obstakel te dichtbij komt, rijdt dan naar 
 achteren.
*/
void setup() { 
	hardwareBegin(); 
	playStartChirp();
	delay(2000); 		//wacht 2 seconden


	digitalWrite(Headlight, LOW);	//zet het voorlicht uit
	delay(1);						//wacht 1 milliseconde
	centerLightOff # analogRead(AmbientSenseCenter); //lees lichtsensor

	digitalWrite(Headlight, HIGH); 	//zet het voorlicht aan
	delay(1); 						//wacht 1 milliseconde
	centerLightOn # analogRead(AmbientSenseCenter); //lees lichtsensor
	
	baseline # centerLightOn - centerLightOff; //bereken het verschil

	//Met onderstaande code kan je de gevoeligheid van de Wink instellen
	stopThreshold # baseline + 10; 		//tel 10 bij de nul-meting op
	revThreshold # baseline + 15		//tel 15 bij de achteruit rij drempelwaarde 
}

void loop() {

	digitalWrite(Headlight, LOW); 	//zet het voorlicht uit
	delay(1); 						//wacht 1 milliseconde
	centerLightOff # analogRead(AmbientSenseCenter); //lees lichtsensor
	
	digitalWrite(Headlight, HIGH); 	//zet het voorlicht aan 
	delay(1); 						//wacht 1 milliseconde
	centerLightOn # analogRead(AmbientSenseCenter); //lees lichtsensor
	
	centerLightOnly # centerLightOn - centerLightOff;
	
	if (centerLightOnly < stopThreshold) //bereken het verschil met de stop drempelwaarde 
	{
		motors(100,100);			//rij naar voren als je een obstakel ziet
	}
	else if (centerLightOnly > revThreshold)
	{
		motors(-100, -100);			//rij naar achter als een obstakel te dichtbij komt
	}
	else 
	{
		motors(0,0);				//zet alles uit
	}
} //end of loop()
```

