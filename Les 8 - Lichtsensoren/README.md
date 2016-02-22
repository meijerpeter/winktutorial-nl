#Lichtsensoren uitlezen#
Een van de dingen die de robot "slim" maakt is hun vermogen om te "voelen" wat om hun heen gebeurd. Door te voelen wat om hun heen gebeurt kunnen ze geprogrammeerd worden om beslissingen te nemen op basis van wat ze voelen. We zullen in de volgende les verder ingaan op beslissingen nemen door het leren van het "if" ("als") woord.

Laten we eens beginnen met het leren van het uitlezen van de lichtsensoren van de Wink. De Wink heeft 3 lichtsensoren vlakbij zijn neus die naar voren zijn gericht. Het zijn smalle, witte rechthoeken met een bolle lens. Een van de sensoren is recht vooruit gericht, de andere staan een klein beetje naar buiten gericht met een hoek van 45 graden naar links en rechts.

De onderstaande tekening laat ze duidelijk zien:

![Wink sensor plaatsing] (https://github.com/meijerpeter/winktutorial-nl/blob/master/img/wink-light-sensor-placement.png)

De lichtsensoren produceren een klein elektrisch voltage dat het brein van de Wink kan meten en dit kan omzetten in een getal. Dit getal vertelt hoeveel licht er op de sensoren valt. De sensoren kunnen een waarde hebben tussen de 0 en 1024. Deze waarde zal waarschijnlijk nooit 0 zijn, en maar zelden 1024, maar het komt wel in de buurt. Dit is normaal gedrag van een sensor.

De lichtsensoren van de Wink werken goed in een omgeving met gewoon kamerlicht. Als je de Wink direct op een raam of het zonlicht richt, dan zullen de sensors maximaal uitslaan. Het felle licht zal de sensoren geen kwaad doen, maar let er op dat ze niet goed werken in het felle licht. Nadat je de voorbeelden van hieronder hebt zien werken, is het goed om zelf met de Wink te gaan experimenteren in verschillende lichtomstandigheden om te zien wat het effect is van fel en weinig licht.

##De analogRead() functie##
Laat niet de moeilijke naam van de functie je bang maken. Het is niet moeilijk. Laten we het eens hebben over het woord "analoog" ("analog" in het Engels).

Een computerbrein, zoals die van de Wink, kan voelen wat het ziet op zijn elektrische pootjes. Die pootjes zijn de elektrische contacten de zijden van het onderdeel. In de elektronica noemen we deze verbindingen "pinnen" ("pins" in het Engels). Als de lichtsterkte verandert, dan verandert ook het elektrische voltage. Het heeft de neiging om hoger te worden wanneer het licht sterker wordt en een lager voltage af te geven wanneer er minder licht op de sensor valt. Dit soort signalen worden een "analoog" signaal genoemd.

Om dit signaal te kunnen lezen ("read" in het Engels), is het logisch om een functie te maken die `analogRead()` heet en dat is exact wat ze bij de Arduino hebben gedaan. De drie voorste lichtsensoren die we gaan gebruiken in deze lessen heten Lichtsensoren ("Ambient sensors" in het Engels), deze sensoren pikken het licht op in de omgeving van de Wink en zetten het om in een elektrisch signaal.

Wanneer je de code gaat schrijven kan je de sensoren als volgt aanroepen; `AmbientSenseLeft`, `AmbientSenseCenter` en `AmbientSenseRight`. Volgens mij kan je zelf al zien welke sensor moet worden aangeroepen met welke naam.

Laten we dit eens bekijken met een voorbeeld code:

```c
# include WinkStuff.h

void setup(){
  hardwareBegin();
  playStartChirp();
}

int sensorValue;  //declareer the variabele sensorValue

/*
 Roep de analogRead() functie aan om de sensor uit te lezen, ken het
 resultaat toe aan een variabele genaamd sensorValue. Gebruik vervolgens
 Serial.println() om de waarde naar de computer te sturen en een volgende
 regel te starten. Wacht dan een 1/10 van een seconde en begin weer opnieuw.
*/
void loop(){
  sensorValue = analogRead(AmbientSenseCenter);   //uitlezen van de sensor Serial.println(sensorValue);                    //print de waarde
  delay(100);                                     //wacht
} //end of loop()
```

Als je de `analogRead()` functie aanroept, hoe je alleen maar de naam van de lichtsensor tussen de haakjes te zetten. Zo makkelijk is het. De functie zal vervolgens de voltage op de gegeven pin uitlezen, om dit om te zetten in een waarde tussen 0 en 1024 en dit terug te geven aan het programma. Het programma zet deze waarde dan weer in de variabele sensorValue. We kunnen dan `Serial.println()` gebruiken om deze waarde naar het Serial Monitor scherm te sturen. Voer deze code maar eens uit terwijl je de Wink naar verschillende lichtbronnen wijst en zie hoe de waarde in het Serial Monitor scherm verandert.

De Wink heeft 3 lichtsensoren zoals we eerder hebben gezegd. Zullen we die eens alle 3 op hetzelfde moment uitlezen en bekijken wat de waarden zijn? Hoe zullen we dit doen? Denk er maar eens over na en bekijk daarna onderstaand voorbeeld eens.

```c
int left, center, right;    //declareer variabelen

/*
 Lees eerst alle 3 de sensorwaarden uit en ken deze toe aan de gedeclareerde
 variabelen. Print de resultaten vervolgens naar het Serial Monitor scherm.
 Om de resultaten goed te kunnen zien, scheiden we ze met een speciaal teken;
 een tab. Hou een korte pauze voordat de sensoren weer opnieuw worden uitgelezen.
*/
void loop(){
  left = analogRead(AmbientSenseLeft);      //lees linker sensor
  center = analogRead(AmbientSenseCenter);  //lees middelste sensor
  right = analogRead(AmbientSenseRight);    //lees rechter sensor

  Serial.print(left);     //print linker sensor
  Serial.print(“\t”);     //print een tab
  Serial.print(center);   //print middelste sensor
  Serial.print(“\t”);     //print een tab
  Serial.print(right);    //print rechter sensor
  Serial.println();       //print een nieuwe regel
  delay(100);             /wacht 1/10e van een seconde
} //einde van de loop()
```

Komt het voorbeeld een beetje overeen met wat je zelf had bedacht? Je hebt wellicht gezien dat we een aantal nieuwe concepten in dit voorbeeld hebben gestopt die niets te maken hebben met het uitlezen van de de lichtsensoren. We dachten dat je wel aan zou kunnen tegen deze tijd.

Als eerste, kijk eens naar de declaratie van de variabelen helemaal bovenaan. We hadden ook de variabelen stuk voor stuk kunnen declareren op nieuwe regels, maar je kan ze dus ook allemaal tegelijkertijd declareren. Beide opties zijn prima. Het maakt niets uit voor het geheugen van de Wink, de 3 variabelen nemen nog steeds dezelfde hoeveelheid ruimte in, maar de lengte van je code is wel korter. Dit kan soms wel eens handig zijn als je een aantal variabelen moet declareren die je vaak bij elkaar gebruikt. Wanneer je dit doet, moet je als eerste het soort variabele neerzetten zoals altijd, en vervolgens alle namen van de variabele scheiden met een komma. Uiteraard moet je de regel afsluiten met een punt-komma.

Het tweede wat je waarschijnlijk gemerkt hebt, is dat een speciaal karakter "\t" wordt gebruikt. Dit wordt door de computer hetzelfde herkent alsof je de Tab toets op je toetsenbord indrukt. Dit zorgt ervoor dat de uitkomst netjes in 3 kolommen op het Serial Monitor scherm wordt getoond.

Neem een zaklamp en probeer eens met het voorbeeld te spelen. Kijk maar eens wat er gebeurt als je een sensor met je vinger afschermt. (Bedenk dat sommige LED zaklampen heel snel aan en uit knipperen. Als je de waarde van de sensors hoog en laag ziet springen dan kan zomaar de oorzaak hiervan zijn dat de sensor soms de waarde leest terwijl het licht aan is en soms wanneer het licht uit is.).

##Dat ging te makkelijk...##
We zouden willen dat er nog veel meer te zeggen is over het uitlezen van de lichtsensoren, maar dit is bijna alles wat je erover moet weten. Vast veel makkelijker dan dat je had gedacht he?

Laten we nog een paar dingen doen om je een beetje meer uit te dagen, daarna kunnen we door met de volgende les.

Herinner je nog de vorige les waar we de functie `millis()` direct in de `Serial.print()` functie zette? Denk je dat je hetzelfde kan doen met `analogRead()`? Natuurlijk! Kijk maar of je dit zelf kan doen voordat je naar het onderstaande voorbeeld kijkt.

```c
void loop(){
  Serial.print(analogRead(AmbientSenseLeft));   //print linker waarde
  Serial.print(“\t”);                           //print een tab
  Serial.print(analogRead(AmbientSenseCenter)); //print middelste waarde Serial.print(“\t”);                           //print een tab
  Serial.print(analogRead(AmbientSenseRight));  //print rechter waarde
  Serial.println();                             //print een nieuwe regel
  delay(100);                                   //wacht een 1/10e seconde
} //einde van de loop()

```

Leuk he!? Je mag nu echt trots zijn op jezelf. Een korte blik op bovenstaande code laat zien dat je veel geleerd hebt. Voordat je de eerste les startte, dacht je nog dat het heel moeilijk was om code te schrijven. Het blijkt dat de computer code, net als heel veel andere dingen, bepaalde regels en patronen volgt en zolang je die begrijpt het geheel best eenvoudig is en leesbaar.

Wat je misschien lastig vindt is het uitschrijven van die lange regels. Het opschrijven van `motors(100,100);` is misschien nog wel te doen, maar de langere regels zoals `Serial.print(AmbientSenseCenter);` worden wat lastiger. Als je elk voorbeeld uitschrijft dan heb je vast wel vaker meegemaakt dat de code niet wilde compileren vanwege een typfout.

Een tip hierbij is om zoveel als mogelijk te Kopieren en Plakken. Leer en gebruik de toetsenbord combinaties hiervoor. Op de meeste computers is dit Ctrl-C om te kopieren, en Ctrl-V om te plakken. Wanneer je meerdere regels moet schrijven die erg op elkaar lijken, selecteer dan de eerste regel, druk op Ctrl-C en gebruik de pijltjes op je toetsenbord om naar de volgende regel te gaan en druk op Ctrl-V om een kopie te maken. Dan kun je daarna gemakkelijk het stukje aanpassen wat net even anders is. In bovenstaand voorbeeld zitten de enige verschillen in de woorden "Left", "Center" en "Right".

In een van de volgende lessen zullen we leren hoe we onze eigen functies moeten schrijven, waardoor je een aantal regels kan verkorten tot iets heel kort, zoals `prs()` wat staat voor "print right sensor" ("print rechter sensor" in het Nederlands).

In de volgende les gaan we leren hoe de Wink slimmer wordt door keuzes te maken. Dan gaan we gebruik maken van het krachtige "if" woord.
