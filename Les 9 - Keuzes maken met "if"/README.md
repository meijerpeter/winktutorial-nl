#Les 9 - Keuzes maken met "if"#

##Voorwaardelijke instructies##
Tot nu toe hebben we de Wink niet echt zelf keuzes laten maken. Alle programma's die we tot nu hebben geschreven volgen alleen maar de functies. Dit is leuk, maar een robot wordt veel nuttiger als het zijn gedrag kan aanpassen aan de hand van de dingen om hem heen.

Er zijn een paar verschillende mogelijkheden om te zorgen dat een computerprogramma aanpassingen maakt aan de code die wordt uitgevoerd. Deze stukken in de code worden voorwaardelijke instructies (in het Engels "control structures") genoemd, omdat zij bepalen hoe een programma uitgevoerd wordt. Sterker nog, deze voorwaardelijke instructies bepalen welke regel(s) code wel en welke niet worden uitgevoerd.

Door gebruik te maken van deze voorwaardelijke instructies kan je bijvoorbeeld een licht laten aangaan als een knopje wordt ingedrukt, en het licht uit laten gaan wanneer het knopje niet wordt ingedrukt.

Een van de meest gebruikte en krachtige voorwaardelijke instructies in elke programmeertaal is de 'if' instructie (in het Nederlands "als"), waar we veel van gaan leren in deze les.

De 'if' instructie bekijkt of iets waar (true) of niet waar (false) is en als iets waar is wordt de code uitgevoerd, en als iets niet waar is dan wordt de code niet uitgevoerd.

Weet je nog van de vorige les dat we het aantal keer dat de functie 'loop()' zich herhaalde hebben opgeteld? We zouden bijvoorbeeld de 'if' instructie kunnen gebruiken om te bekijken of 'loopCount' groter is dan 5, en als 'loopCount' daadwerkelijk groter is de ogen van de Wink aan te zetten. Dit gaan we straks in ons voorbeeld doen, maar eerst gaan we kijken hoe je een 'if' instructie gebruikt in je code.

De 'if' instructie kijkt naar iets als een voorwaarde, en bepaald of deze voorwaarde waar of niet waar is. Als de voorwaarde _waar_ is dan wordt alle code binnen de if-accolades ({...}) uitgevoerd, als de voorwaarde _niet waar_ is, dan wordt de code die binnen de if-accolades staat niet uitgevoerd.

Het is eenvoudig te zien in onderstaand voorbeeld:

```c
/*
 Dit is een voorbeeld van de voorwaardelijke "if' instructie
*/
 if (2 > 1) {
   // als de voorwaarde waar is, wordt de code die hier is geplaatst uitgevoerd
 }
```

Het lijkt ingewikkeld, maar dat valt in de praktijk best mee. Laten we een de onderdelen van de 'if' instructie bespreken...

Het begint met het woord "if", gevolgd door een voorwaarde. De voorwaarde staat binnen de haakjes ((...)). In ons voorbeeld is dit "2 is groter dan 1". Veel verschillende voorwaarden kunnen worden gebruikt, dit is alleen een voorbeeld om je te helpen bij het begrijpen van de 'if' instructie.

Na de voorwaarde wordt een accolade geopend ({), die het begin aangeeft van de code die moet worden uitgevoerd als de voorwaarde waar is. Het einde van de code die wordt uitgevoerd als de voorwaarde waar is wordt aangegeven met een gesloten accolade (}).

'if' vraagt zich altijd af of een voorwaarde _waar_ is. In ons voorbeeld wordt de vraag "is het waar dat twee groter is dan een?" gesteld. Omdat twee inderdaad groter is dan een, is de voorwaarde dus _waar_ (true), en omdat het waar is, zal de alle code die binnen de accolades staat worden uitgevoerd.

Let op dat er geen punt-komma (;) wordt gebruikt voor de de 'if' instructie, de regels code die binnen de accolades staan moeten wel worden afgesloten met een punt-komma.

Laten we nu eens ons eerste voorbeeld maken. Dit voorbeeld is gebaseerd op een voorbeeld uit de vorige les waar de Wink het aantal keren telt dat het door de 'loop()' functie is gegaan.

```c
# include WinkHardware.h

void setup(){
   hardwareBegin();
   playStartChirp();
}


int loopCount = 0; //declareer de loopCount variabele

/*
  De functie eyesCyan(100); wordt uitgevoerd als het waar is dat
  loopCount groter dan 5 is
*/
void loop(){
  if (loopCount > 5){ //als loopCount groter is dan 5...
    eyesCyan(100); //voer dan de code tussen de accolades uit
}

  loopCount = loopCount + 1; //tel 1 bij loopCount op
  delay(1000); //wacht 1 seconde
} //einde van de loop()

```

Laten we nu eens kijken wat er hierboven is gebeurd.

Wanneer loopCount wordt gedeclareerd, wordt de waarde op 0 gezet. De eerste keer dat de 'loop()' functie wordt uitgevoerd is 'loopCount' 0. Wanneer de 'if' instructie wordt aangeroepen, wordt de voorwaarde binnen de haakjes bekenen. Het programma bekijkt of "is het waar dat loopCount groter is dan 5?" klopt. In ons geval, dit is niet waar omdat 'loopCount' nul is. Omdat de conditie niet waar is, wordt de code binnen de accolades niet uitgevoerd. Alles binnen de accolades wordt overgeslagen en de code na de gesloten accolade (}) wordt uitgevoerd.

'loopCount' wordt vervolgens opgehoogd met 1, dus nu is het de waarde 1 geworden. Dit wordt elke keer herhaald, totdat 'loopCount' 6 wordt. Op dat moment, de zesde keer dat de 'loop()' functie wordt herhaald, zal weer de 'if' instructie zich afvragen of "is het waar dat loopCount groter is dan 5?", en omdat 'loopCount' nu 6 is op dit moment wordt de voorwaarde _waar_ omdat 6 daadwerkelijk groter is dan 5. Omdat het waar is zal de code binnen de accolades, 'eyesCyan(100);', nu wel worden uitgevoerd, zodat in ons geval de ogen van de Wink cyan worden gekleurd.

###Meer over de "voorwaarde"###
De "voorwaarde" is het gedeelte wat wordt bekeken of het waar (true) of niet waar (false) is. Het staat tussen haakjes. In het vorige voorbeeld wilden we eigenlijk de ogen aanzetten na 5 seconden, maar je zal hebben gezien dat het eigenlijk 6 seconde duurde voordat de ogen aangezet werden. Dit komt omdat we de 'if' instructie hebben verteld waar te zijn als 'loopCount' __groter__ is dan 5. Dus het zal niet eerder uitgevoerd worden totdat de waarde van 'loopCount' 6 wordt.

Soms willen we iets uitvoeren als een getal groter of __gelijk__ is aan een ander getal. Dit kunnen we eenvoudig doen door het "groter dan" teken te wijzigen in een "groter en gelijk aan" teken. Zoals in dit voorbeeld...

```c

int loopCount = 0; //declareer de loopCount variabele

/*
  De voorwaarde is nu "groter of gelijk aan". Hierdoor wordt de functie
  eyesCyan(100); pas uitgevoerd als het waar is dat
  loopCount gelijk aan 5 is, of de waarde groter is.
*/
void loop(){
  if (loopCount >= 5){ //als loopCount groter of gelijk is dan 5...
    eyesCyan(100); //voer dan de code tussen de accolades uit
}

  loopCount = loopCount + 1; //tel 1 bij loopCount op
  delay(1000); //wacht 1 seconde
} //einde van de loop()

```

Merkt op dat nu het "groter dan" teken (>) nu gevolgd wordt door een "gelijk aan" teken (=), zodat de voorwaarde nu waar wordt als 'loopCount' __groter of gelijk aan__ 5 is.

Het teken dat wordt gebruikt in de voorwaarde heet een "vergelijkingsoperator". Dit betekent dat de operator wordt gebruikt om de waarde te vergelijken die in de voorwaarde staan. Er zijn zes verschillende vergelijkings operatoren die je kan gebruiken in de voorwaarde van je 'if' instructie.

Hieronder staan deze alle zes uitgelegd:

|Vergelijksoperator|Wat betekent het?|
|------------------|-----------------|
|==|gelijk aan|
|!=|niet gelijk aan|
|<|kleiner dan|
|>|groter dan|
|<=|kleiner of gelijk aan|
|>=|groter of gelijk aan|

De meeste vergelijkingsoperatoren in de tabel zijn te begrijpen, maar je hebt ook gezien dat het "gelijk aan" teken bestaat uit twee "is-gelijk" aan tekens, eens? Waarom is dat? Je zou denken dat "gelijk aan" zou moeten bestaan uit 1 "=" teken, toch?

We zullen uitleggen waarom dit is.

Je hebt waarschijnlijk van de Variabelen les onthouden dat wanneer je een waarde toekent aan een variabele, je ook een is-gelijk teken (=) gebruikt. Hierbij gebruikte je maar 1 is-gelijk teken. Kijk maar...

```c
/*
  Een enkel is-gelijk teken is een toekenning, een dubbele is-gelijk teken
  vergelijkt twee waarden.
*/
  birds = 10; //enkelvoudige is-gelijk teken is een "toewijzing"
  if (birds == 10){ //dubbele is-gelijk teken is een "vergelijking"
    eyesRed(100);
  }
```

In de eerste regel van bovenstaand voorbeeld gebruiken we een enkel is-gelijk teken om een waarde van 10 toe te kennen aan de variabele 'bird'. Een enkele is-gelijk teken is een toekenningsoperator.

Daarna volgt de 'if' instructie waarin we met een dubbel is-gelijk teken een vergelijking tussen twee waarden uitvoeren om te kijken of een bepaalde voorwaarde geldt. In dit geval vergelijken we de variable 'birds' met het getal 10.

Als het klopt dat 'birds' gelijk is aan 10, dan is de voorwaarde waar (true) en zal de code tussen de accolades uitgevoerd worden. Als de waarde niet gelijk is aan 10, dan is de voorwaarde niet waar (false) en zal de code tussen de accolades niet uitgevoerd worden.

###Een andere opmaak voor de "if" instructie###
Je kan de opmaak (de manier waarop je iets schrijft) van de 'if' instructie op verschillende manieren weergeven. Sommige programmeurs houden ervan om de accolades op aparte regels te zetten, waardoor de code beter leesbaar wordt. Tot op dit moment schreven wij de openings accolade op dezelfde regel als de voorwaarde. Beide manieren mogen. Hier is een voorbeeld:

```c
/*
 Voorbeeld waarin de geopende accolade op een eigen regel wordt geplaatst. Sommige programmeurs vinden dit makkelijk te lezen.
*/
  if (birds == 10)  // de voorwaarde staat op een eigen regel
  {                 // de accolade staat ook op een eigen regel
    eyesRed(100);   // de code binnen de accolades
  }                 // afsluiten met de gesloten accolade

  if (birds == 10){ // hier wordt de openings accolade op dezelgde regel gezet
    eyesRed(100);   // de code binnen de accolades
  }                 // afsluiten met de gesloten accolade
```
###Een tweede keuze maken met "else"###
Nu weet je hoe je code kan uitvoeren als een bepaalde voorwaarde waar is. Soms is dit voldoende om je programme uit te voeren, maar soms wil je ook dat iets wordt uitgevoerd als de voorwaarde waar is, en dat iets anders wordt uitgevoerd als de voorwaarde niet waar is.

Bijvoorbeeld, je wil het lampje aanzetten als een knopje wordt ingedrukt en als de knop niet wordt ingedrukt het lampje weer uitzetten. We zullen je later laten zien hoe je het knopje in je 'if' instructie kan gebruiken. Voor nu zullen we het gebruik van 'else' demonstreren met ons eerder voorbeeld gebruikmakend van 'loopCount'.

Onthoud dat 'else' de code uitvoert als 'if' niet waar is. Kijk maar naar onderstaand voorbeeld.

```c
# include WinkHardware.h

/*
 Normale setup
*/
void setup(){
  hardwareBegin();
  playStartChirp();
}


int loopCount = 0; //declareer loopCount variabele

/*
  De ogen worden cyan gekleurd als de loop 3 keer is uitgevoerd. Als dit niet
  waar is, dan worden de ogen uitgezet.
*/
void loop(){
  if (loopCount == 3) //als loopCount gelijk is aan 3
  {                   //open de accolade
    eyesCyan(100);    //voer de code uit tussen de accolades
  }                   //sluit de accolade
  else                //als het niet waar is, voer dan de code hieronder uit
  {                   //open de accolade
    eyesOff();        //zet de ogen uit
  }                   //sluit de accolade

  loopCount = loopCount + 1;  //tel 1 op bij loopCount
  delay(1000);                //wacht 1 seconde
} //einde van de loop()
```

Wanneer je deze code uitvoert, dan zal de ogen van de Wink voor 3 seconden uit blijven. Daarna zullen de ogen gedurende 1 seconde worden aangezet, om vervolgens de ogen weer uit te zetten. Dit gebeurt omdat de eerste drie keer dat de 'if' instructie wordt aangeroepen, 'loopCount' niet gelijk is aan 3. Hierdoor wordt wel de code in het 'else' blok (alles tussen de accolades) uitgevoerd, in het voorbeeld is dit 'eyesOff();' zodat de ogen van de Wink uit blijven. Nadat de 'loop()' drie keer is uitgevoerd zal 'loopCount' gelijk zijn aan 3. Op dat moment wordt als de 'if' instructie wordt uitgevoerd en de voorwaarde waar is, 'eyesCyan(100);' uitgevoerd om de ogen aan te zetten. Daarna wordt weer 1 wordt opgeteld bij 'loopCount' en zal de 'loop' functie zich weer herhalen. De volgende keer is 'loopCount' 4 en is de voorwaarde niet langer waar, dus wordt  de code binnen het 'else' blok weer uitgevoerd en gaan de ogen vervolgens uit.

Laten we eens goed kijken hoe de 'else' instructie wordt geschreven. Een 'else' volgt altijd na een 'if'. De 'else' heeft geen voorwaarde (geen vergelijking tussen haakjes) omdat de 'else' altijd wordt uitgevoerd als de 'if' niet waar is. De 'else' heeft zijn eigen accolades, die het begin en einde markeren van de code die wordt uitgevoerd door de 'else'.

Nadat de 'if' en 'else' instructies klaar zijn, wordt de regel eronder uitgevoerd en gaat het programma verder zoals je zou verwachten.

Het is wellicht een beetje veel informatie in korte tijd, dus als je het nog niet helemaal snapt is dit niet erg! Lees gerust het stuk nog eens rustig door, en denk na bij elke stap. Je zal misschien het hoofdstuk een paar keer moeten lezen om het goed te begrijpen. Het is een lastig stuk om te leren, dus neem je tijd!

__Goede tip...__ Je hebt straks veel accolades in je code, waarbij de Arduino IDE je kan helpen. Wanneer je de cursor op een van de accolades of haakjes plaatst, zal de Arduino IDE de bijbehorende accolade of haakje omcirkelen. Dit helpt met het aanwijzen van welk stuk code tussen de accolades of haakjes staat als de programma steeds ingewikkelder wordt. Ook het plaatsen van de accolades op een nieuwe regel helpt hierbij.

##Eenvoudig het licht zoeken##
Nu kunnen we iets ingewikkelds met de Wink gaat doen, met wat we zojuist geleerd hebben. We weten nu hoe we de 'if' en 'else' instructie moeten gebruiken, we weten hoe we de motoren moeten aansturen en hoe we de lichtsensoren moeten uitlezen. Nu we dit allemaal weten gaan we een heel eenvoudig programma schrijven die de Wink het licht laat opzoeken.

Voordat we het programma gaan schrijven, laten we eerst nadenken hoe we dit kunnen laten werken...

Het idee is om de Wink om zijn as te laten draaien en tegelijkertijd naar te zoeken naar het felste licht. Om dit te doen, kunnen we de linker en rechter lichtsensoren uitlezen en dan bepalen welke het meeste licht ziet. Daarna kunnen we de Wink een keuze laten maken en de motoren of naar links of naar rechts laten draaien.

Omdat we beide sensoren gaan uitlezen, zullen we hiervoor een aantal variabelen nodig hebben om de waarden in op te slaan. In onze voorwaardelijke 'if' instructie willen we beide waarden vergelijken, als een van de sensor waarde (bijvoorbeeld de rechter), dan willen we de code uitvoeren die er voor zorgt dat de Wink naar de rechterkant draait. We kunnen de 'else' gebruiken om de Wink de andere kant op te laten draaien.

Denk eens na hoe je dit zou maken, en kijk pas daarna naar het voorbeeld hieronder of dit overeenkomt met hoe jij het zou hebbeb gemaakt. Als je je wil uitdagen, open dan de Wink Base Sketch en schrijf dit programma dan eens helemaal zelf en kijk pas daarna naar het voorbeeld.

###Het voorbeeld###
Ik raad je aan om eerst zelf uit te zoeken hoe je het lichtzoek probleem zou oplossen voordat je verder gaat. Als je deze lessen in een groep volgt, bespreek dan eerst eens met elkaar hoe je de oplossing zou realiseren.

Hier is het voorbeeld hoe wij het hebben opgelost:

```c
# include WinkHardware.h

/*
 Normale setup
*/
void setup(){
  hardwareBegin();
  playStartChirp();
}

int leftLight, rightLight; //Declareer de benodigde variabelen

/*
  Als het licht aan de rechterkant feller is dan aan de linkerkant,
  voer dan de code uit om de Wink naar rechts te laten draaien. Als deze
  voorwaarde niet waar is, is het licht aan de linkerkant of gelijk of sterker.
  Draai de Wink dan naar links. Blijf dit herhalen zodat de Wink continu
  naar het licht draait.
*/
void loop(){
  leftLight = analogRead(AmbientSenseLeft);   //uitlezen linker lichtsensor
  rightLight = analogRead(AmbientSenseRight); //uitlezen rechter lichtsensor

  if (rightLight > leftLight) //als rechts groter is dan links
  {                           //open de accolade voor de 'if'
    motors(100,-100);         //draai naar rechts
  }                           //sluit de accolade voor de 'if'
  else
  {                           //open de accolade voor de 'else'
    motors(-100,100);         //draai naar links
  }                           //sluit de accolade voor de 'else'
} //einde van de loop()
```

Is het niet fantastisch dat je robot zo iets slims kan doen met een klein beetje code?

Probeer eens bovenstaande code te uploaden en uit te voeren om te zien om de Wink het doet. Het helpt wellicht als je met een zaklampje schijnt op en in de buurt van de voorkant van de Wink. Dit werkt het beste als je het direct op het oppervlakte rondom de Wink schijnt, in plaats van bovenop de Wink. De sensoren zijn het meest gevoelig voor licht wat vanaf de oppervlakte weerkaatst.

Wanneer je gaat experimenteren met bovenstaande code zal je ook een aantal gekke dingen zien, maar we zullen daar later op terugkomen. Als je dit gedrag ziet, denk dan goed na over de code en waarom dit "vreemde" gedrag getoond wordt. Vaak zal een programma niet precies doen wat je zou verwachten of willen, dus is het goed om over dit "vreemd" gedrag goed na te denken.

###Wat is je opgevallen?###
Nu heb je code geschreven die de Wink echt slimmer maakt. Laten we eens over een aantal dingen gaan praten die je misschien zijn opgevallen.

####Eindeloos draaien####
De Wink zal soms in een rondje draaien. Waarom is dit? Als de verlichting in de ruimte redelijk hetzelfde is, dan zal de Wink niet zien dat de ene kant lichter is dan de andere kant. In onze code hebben we de Wink niet verteld om "stil te staan als het licht redelijk gelijk is", in plaats daarvan hebben we de Wink geprogrammeerd om continu te blijven draaien. Zelfs als de waardes van de linker en rechter sensor hetzelfde zijn, dan wordt de 'else' te worden uitgevoerd elke keer dat de 'loop()' functie wordt doorlopen zodat de Wink altijd naar een kant blijft draaien.

Een andere reden is dat de sensoren niet perfect zijn en ook niet identiek. Tijdens de fabricage (het maken) van de sensoren zal altijd de ene sensor iets meer sensitiever zijn dan de andere. Dit kan worden gecorrigeerd door dure sensoren en filters, maar zelfs dan zullen ze bijna nooit exact dezelfde waarde teruggeven, zelf als het licht perfect is.

Als je een uitdaging zoekt, gebruik dan de 'Serial.print()' functies die we eerder geleerd hebben om te zien welke waarde er worden gelezen. _Je kan dan het beste de code voor de aansturing van de motor uitzetten zodat de Wink niet gaat draaien. Dit kan je gemakkelijk doen door een paar "forward slashes" (//) voor de twee 'motors()' regels te zetten. Dit zorgt ervoor dat de code als commentaar wordt behandeld en niet wordt uitgevoerd. Dit is een gebruikelijke manier om iets tijdelijk te testen zonder het helemaal weg te halen._
Bekijk de waarde van de 'leftLight' en 'rightLight' en probeer eens een gelijke belichting van de sensoren te krijgen. Je zal zien dat in een gelijke situatie de een altijd hoger is dan de andere. Op basis hiervan zou je dit kunnen compenseren in de code, bijvoorbeeld als de 'leftLight' altijd 5 hoger is dan de 'rightLight', kan je bijvoorbeeld in een nieuwe regel net voor de 'if' instructie 5 bij 'rightLight' optellen.

####De Wink gaat heen en weer####
Dit noemen we "oscilatie". Wanneer iets aan het oscilleren is, dan beweegt het heen en weer tussen twee dingen. Als de Wink het licht aan de ene kant sterker ziet, dan zal het die kant gaan opdraaien met een het aanzetten van de motoren. Als hij draait, zal hij voorbij het licht draaien zodat de andere sensor het licht ziet en vervolgens wordt de beweging de andere kant ingezet. Omdat hij al in beweging is zal hij er een klein beetje voorbij bewegen en daarna weer richting het licht bewegen. Dit zal beide kanten op gebeuren, waardoor de Wink om en om heen en weer blijft bewegen naar de linker en rechter kant. Dit kunnen we op een aantal manieren compenseren. Een optie is om de snelheid van de motoren aan te passen op basis van het verschil tussen de twee lichtsensoren. Dit is een wat geavanceerde optie die we pas tijdens een moeilijkere les zullen behandelen.

####Wink zet zich "vast" in een richting, en richt zich opeens op een andere lichtbron####
De Wink kan zich richten op een bepaalde lichtbron en die richting vast blijven houden zonder te oscilleren. Mocht er een schaduw over de Wink vallen, zal de Wink wellicht op zoek gaan naar een andere lichtbron en zich daar op vast zetten. Het hangt veel af van waar het licht vandaan komt in de ruimte waar de Wink zich in bevindt. Probeer maar eens de Wink aan te zetten in een ruimte met gelijk licht en dan je hand over de Wink te bewegen zodat er een schaduw over de lichtsensoren valt.

##De opmaak van je code##
Het zal je wellicht zijn opgevallen dat sommige regels code zijn "ingesprongen". Dit kan je doen met de TAB-toets op je toetsenbord. Voor de taal C maakt het niet uit of je met inspringingen werkt of niet, maar het maakt het wel gemakkelijker voor (andere) mensen om de code te lezen als je je aan een aantal standaard regels houdt.

Normaal gesproken, wanneer je een voorwaardelijke instructie (bijv. de 'if') gebruikt, lijn je de accolade open en sluiten gelijk met de "i" in het woord "if" uit. Hetzelfde geldt voor de 'else' instructie, de open en sluit accolades worden hier ook uitgelijnd met het begin van het woord "else".

Je zal ook zien dat de code binnen de accolades nog een beetje verder is ingesprongen. Dit helpt je om te zien welke code er bij elkaar hoort. Je kan namelijk meerdere 'if' instructies gebruiken binnen een andere 'if' instructie (of andere voorwaardelijke instructies). Dit wordt "nesten" genoemd. Normaliter zal elke "geneste" voorwaardelijke instructie een stukje verder ingesprongen worden dan de vorige blok code. Hierdoor kan je in een oogopslag zien welke code bij elkaar hoort.

Daarnaast, heeft de 'loop()' functie ook een accolades, eentje in het begin en eentje aan het einde. Elke 'if' instructie heeft ook een paar accolades, en elke 'else' instructie ook. Het is belangrijk dat de haakjes altijd bij elkaar horen. Als je een haakje vergeet wordt je code niet gecompileerd omdat de computer niet weet waar een blok code start of eindigt. Als je je aan de opmaakregels houdt, dan zal je sneller zien waar je haakje vergeten bent.

##Het gebruik van "else-if" voor nog meer controle##
Aan het begin van de les hebben we gezegd dat de 'if' instructie zeer krachtig is. We zullen je nu nog een andere manier laten zien hoe je deze instructie kan gebruiken. In ons eerste voorbeeld lieten we een simpele 'if' zien, daarna gaven we het programma een tweede optie wanneer de 'if' niet waar was, dit is de 'else' instructie. Nu laten we je nog een optie zien die je kan gebruiken, dit is de 'else if'.

'else if' is een tweede voorwaarde, dit wordt bekeken als de eerste voorwaarde niet waar is. Kijk maar eens naar deze code:

```c
birds = 5;

 //als birds gelijk is aan 10, wordt eyesRed(100); uitgevoerd
if (birds == 10)  
{
  eyesRed(100);
}
//als de eerste "if" niet waar is, wordt gekeken of de tweede "else if"
//voorwaarde waar is. Als dat zo is, wordt eyesGreen(100); uitgevoerd
else if (birds < 10)
{
  eyesGreen(100);
}
//als de eerste "if" niet waar was, en ook de tweede en volgende "else if" niet
//waar zijn, dan wordt alles wat in het "else" blok staat uitgevoerd.
else {
  eyesBlue(100);
}
```

De 'else if' is als een tweede 'if' instructie onder de eerste 'if'. Als de eerste 'if' niet waar is, gaat het programma verder met de volgende 'else if'. Als die voorwaarde waar is, wordt de code binnen dit blok uitgevoerd en de hele 'if' instructie stopt en gaat verder met de code na de 'else' instructie.

Het is hetzelfde alsof we aan jou zouden vragen "Wil je een chocolade koekje?", en jij dan "nee" zou zeggen. Als tweede optie vraag ik je "Wil je een aardbeien koekje?". Als je dan "ja" zegt dan krijg je een koekje en verder niets meer. Als je nou ook "nee" zou zeggen tegen het aardbeien koekje, dan zou ik je bijvoorbeeld een vanille koekje geven omdat dit de smaak is die we aan iedereen geven als ze geen chocolade of aarbeien smaak willen.

Je kan zo veel 'else if' instructies gebruiken als je wil. Je begint altijd met een 'if', daarna met zoveel 'else if' instructies als je wil en optioneel sluit je af met een 'else' instructie die pas wordt uitgevoerd als de voorgaande 'if' en 'else if' instructies niet waar zijn.

Zie onderstaand voorbeeld:
```c
buttonPress = 2;

if (buttonPress == 1)
{
  eyesRed(100);
}
else if (buttonPress == 2) //in dit geval wordt eyesGreen(100); uitgevoerd
{
  eyesGreen(100);
}
else if (buttonPress == 3)
{
  eyesBlue(100);
}
//in dit geval willen we niets doen met "else". Je kan "else" volledig weglaten,
//of zoals hier leeglaten met wat commentaar erin waarin je zegt dat je "niets doet"
else  
{
  //doe niets
}
```

Merk op dat 'else' eigenlijk niet verplicht is. Het maakt je code misschien een beetje kleiner als je het weglaat (de meeste compilers zijn slim genoeg om dit niet mee te nemen), maar het is een goed gebruik om het toch erin te zetten zodat je laat zien dat je niets wil doen als de eerste 'if' en de opvolgende 'else if' instructies niet waar zijn.

##Uitdaging: toevoegen van een "stille zone" aan het lichtzoeken##
Ik weet dat het een lange les is, dus als je hoofd begint te tollen dan moet je maar even een lange pauze nemen en even gaan spelen. Als je klaar voor de laatste uitdaging bent dan gaan we weer verder.

Laten we eens 'if', 'else if' en 'else' gaan combineren om een "stille zone" toe te voegen in het lichtzoeken. Een "stille zone" ("dead band" in het engels) is een term die wordt gebruikt in robotica en elektronica om te refereren naar een gebied waar geen activiteit plaatsvindt. In ons vorige voorbeeld zou de Wink blijven draaien, zelfs al zou de Wink gelijkwaardige licht van beide kanten zien. Dit komt omdat we de Wink geen optie gaven om stil te zitten.

In de volgende uitdaging gaan we de Wink naar het licht laten bewegen, maar als de beide sensoren ongeveer gelijk zijn moet de Wink niet meer bewegen en juist stilstaan.

Als je er klaar voor bent, kan je het misschien ook zelf gaan proberen voordat je naar het onderstaande voorbeeld kijkt:

```c
int leftLight, rightLight;    //declareer de variables die we nodig hebben

/*
 Eerst lezen we beide sensoren uit. Als de rechtersensor 10 meer is dan de
 linkersensor, dan moet de code worden uitgevoerd om de Wink naar rechts
 te laten draaien. Als de linkersensor meer dan 10 groter is dan de rechtersensor, dan moet de code de Wink juist naar links laten draaien.

 Als dit beide niet waar is, en het verschil dus minder dan 10 is, dan is dit
 de "stille zone" en moeten de motoren stoppen met draaien.
*/
void loop(){
  leftLight = analogRead(AmbientSenseLeft);   //uitlezen linker lichtsensor
  rightLight = analogRead(AmbientSenseRight); //uitlezen rechter lichtsensor

  if (rightLight-10 > leftLight)              //als rechts groter is
  {
    motors(100,-100);                         //draai naar rechts
  }
  else if (leftLight-10 > rightLight)         //als links groter is
  {
    motors(-100,100);                         //draai naar links
  }
  else
  {
    motors(0,0);                              //zet de motoren uit
  }
} //end of loop()
```

###Berekening in de voorwaarde###
Bekijk bovenstaand voorbeeld en probeer te begrijpen wat hier gebeurt.

We hebben een nieuw idee geintroduceerd in het voorbeeld. Heb je gezien dat we een berekening uitvoeren in de voorwaarde van de 'if' en 'else if'? Cool he? Het programma zal eerst de berekening uitvoeren, daarna zal het resultaat van de berekening worden gebruikt om te vergelijken.

In dit geval, in de eerste voorwaarde, kijken we of het waar is dat "rightLight minus 10 groter is dan leftLight". Denk er maar eens over na. Deze voorwaarde is waar ("true") als de waarde van de rechtersensor minstens 10 hoger is dan de linkersensor. Dit komt omdat we eerst 10 van de rechtersensor aftrekken voordat we deze vergelijken met de linkersensor. Als de waarde dan nog steeds groter is dan de linkersensor is de uitkomst van de vergelijking "waar".

Je kan allerlei soorten berekeningen uitvoeren in de voorwaarde zelf.

Een andere (meer ingewikkelde) manier zou kunnen zijn met behulp van een nieuwe variabele, waarin de waarde van de berekening wordt toegekend en vervolgens wordt gebruikt in de 'if' instructie. Dit is veel ingewikkelder en gebruikt ook nog eens meer geheugen van de Wink. Dit is de reden dat het uitvoeren van een berekening in de voorwaarde veel gebruikt wordt, net zoals in het voorbeeld.

###Experimenteer eens met de waardes###
Nu dat we het programma hebben werken, probeer eens met de waardes te experimenteren. Speel eens met de waardes van de motoren. Wat gebeurt er als je ze allemaal op 250 zet? Veel plezier hiermee, want de Wink wordt veel moeilijker bestuurbaarder omdat hij waarschijnlijk vaker verder door zal schieten bij het draaien. Probeer het maar eens om te zien wat er gebeurt.

Speel ook eens met de stille zone getallen. Wat gebeurt en als je de cijfers verandert van 10 naar 1? Wat als je het 50, of 200 maakt? Experimenteer maar eens met deze getallen en een zaklamp om te zien wat het effect op de Wink is.

##In een keer alle getallen aanpassen...##
Als je met de getallen hebt geexperimenteerd van het vorige voorbeeld, dan zal je iets vervelends hebben gemerkt. Om de draaisnelheid aan te passen, moest je de getallen in vier verschillende plaatsen aanpassen. En als je een getal vergeten was, dan zou de Wink in een grote bocht hebben gereden in plaats van te spinnen. Als je de waardes van de stille zone had willen aanpassen, moest je dit in twee verschillende plaatsen doen.

Soms, in het bijzonder met robotica, moet je vaak aanpassingen maken aan een stuk code. Bijvoorbeeld, bij het maken van een beweging van een robotarm, zou je dan de snelheid "10" of "500" gebruiken? Je weet wellicht niet de juiste snelheid totdat je een aantal verschillende waarden hebt uitgeprobeerd. Misschien ontdek je dat een snelheid van meer dan "500" de robotarm zo snel laat bewegen dat het omvalt, of dat er onderdelen kapot gaan. Je wil waarschijnlijk de maximale snelheid van de robotarm beperken, en die kan misschien in 37 verschllende plekken op je code voorkomen. Als je die allemaal in een keer zou moeten aanpassen!

In toepassingen zoals hierboven moet je regelmatig een waarde aanpassen om te experimenteren. Het is een goed gebruik om deze waarde als variabele te declareren, dan de waarde toe te kennen aan deze variabele en vervolgens de variabele te gebruiken in plaats van de actuele waarde in de code. Als je deze variabele declareert aan het begin van je code, kan je de aanpassingen in een plaats maken die vervolgens in de rest van je code doorwerkt. Het is ook een goed gebruik om deze variabelen van commentaar te voorzien zodat een andere gebruiker van je code precies weet welke waarde moeten worden aangepast en wat deze waarden aansturen. Je kan ook een beginwaarde aangeven, of de bandbreedte van de waarden in het commentaar.

```c
int dBand = 10;           //pas deze waarde aan om de stille zone te veranderen
int mSpeed = 100;         //pas deze waarde aan om de snelheid van de motoren te veranderen

int leftLight, rightLight;  //declareer de variables die we nodig hebben

/*
 In plaats van het getal "10" te schrijven, gebruiken we nu variabele dBand.
 Hetzelfde doen we met de snelheid van de motoren, in plaats van "100" te
 schrijven gebruiken we nu de variabele mSpeed.
*/
void loop(){
  leftLight = analogRead(AmbientSenseLeft);   //uitlezen linker lichtsensor
  rightLight = analogRead(AmbientSenseRight); //uitlezen rechter lichtsensor

  if (rightLight-dBand > leftLight)           //als rechts groter is
  {
    motors(mSpeed,-mSpeed);                   //draai naar rechts
  }
  else if (leftLight-dBand > rightLight)      //als links groter is
  {
    motors(-mSpeed,mSpeed);                   //draai naar links
  }
  else
  {
    motors(0,0);                              //zet de motoren uit
  }
} //einde van de loop()
```

##Samenvattend##
Wow. Dat is een lange les, maar nu heb je wel een van de meest belangrijke programmeer concepten geleerd - hoe een computer keuzes kan maken op basis van elke voorwaarde. Het is zeer belangrijk om dit te begrijpen en bekend mee te raken, dus misschien moet je nog een paar keer door deze les heen gaan om dit goed te begrijpen. Als je het niet in een keer begrijpt, neem dat even een paar dagen rust om vervolgens weer met een frisse blik hiernaar te kijken.

Voordat we de volgende les gaan starten kan je eerst nog even spelen met wat je tot nu hebt geleerd. Wat kan je nog meer doen met de 'if' en de andere dingen die je geleerd hebt? Kan je misschien een alarm maken die geluid maakt als de lichten aangaan? Kan je de Wink in verschillende snelheden laten rijden op basis van de lichtsterkte in je kamer? (Hou wel in gaten dat de lichtsensoren tot 1024 gaan en de motoren tot 255, je moet misschien wat berekeningen uitvoeren hiervoor).

Wat gebeurt er als je de ogen van de Wink aanstuurt terwijl je een lichtsterke aan het uitlezen bent, of de lichtzoek voorbeelden van deze les uitvoert? Je zal waarschijnlijk een aantal problemen tegenkomen. Hoe kan je die oplossen? We gaan hier verder op in bij de volgende les maar het zou een goede uitdaging zijn om dit eerst zelf op te lossen...
