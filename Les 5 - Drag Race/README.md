#Les 5 - Drag Racen#

##Tijd voor iets leuks!##
Nu dat je de basis wat beter kent, wordt het tijd dat je alles gaat combineren in iets leuks. Laten we kijken hoe snel we de Wink kunnen laten rijden! Iedereen vind het leuk om te racen. In deze les gaan we wat je geleerd hebt toepassen om met de Wink een race programma te gaan maken.

Voordat we beginnen met het schrijven van de code, laten we eerst een bedenken wat we gaan doen. Het is altijd een goed idee om eerst een paar minuten van te voren te plannen wat we gaan doen. Dit voorkomt dat je allemaal onnodige code schrijft. Het helpt je ook bij het organiseren van je code als je een plan volgt.

Het plan wat we gaan volgens is als volgt:

1. Om onze race te gaan beginnen moeten we wachten totdat op het knopje van Wink is gedrukt. Dit zal ons race programma gaan starten.

2. Wanneer op het knopje wordt gedrukt willen we een soort van aftellen laten beginnen, iets van "een, twee, go"!

3. Na het aftellen moet de Wink zo snel mogelijk gaan rijden!

4. Nadat de race is begonnen willen de Wink weer stoppen zodat hij niet voor eeuwig blijft rijden.

Het plannen van je programma kan op verschillende manieren. Je kan bijvoorbeeld een simpele lijst maken zoals hierboven, of je kan een schema maken op papier. Voor complexe programma's is het handig om een stroomschema te maken die al je stappen van je programma weergeeft. Hieronder staat een stroomschema van alle stappen in je race programma.

![Schema drag race](https://github.com/meijerpeter/winktutorial-nl/blob/master/img/flowchart-drag-race.png)

Laten we een eenvoudig voorbeeld maken om mee te beginnen. Probeer deze code maar eens.

``` c
/*
 Nadat op het knopje is gedrukt start het aftellen (2 seconden op rood, daarna kort op
 groen en geef een geluidje bij de start), waarna de Wink zo hard als 
 mogelijk gaat rijden. Na 1 seconde stopt de Wink met de race.
*/
void loop() {
	waitForButton();// Wachten totdat op het knopje wordt gedrukt
	
	// Eerste keer knipperen
	eyesRed(100); 	// Maak de ogen rood
	beep(1000); 	// Geef een geluidje voor 1 seconde
	eyesOff(); 		// Zet de ogen uit
	delay(200);		// Wacht 2 seconden
	
	// Tweede keer knipperen
	eyesGreen(100); // Zet de ogen op groen
	beep(25);		// Kort geluidje

	// GO!!
	motors(255,255); // Beide motoren op volle snelheid
	
	// Wacht totdat de race over is
	delay(1000);	// Rijd de Wink voor 1 seconde
	
	//STOP! 
	beStill(); 		// Stop met bewegen
	eyesOff();		// Zet de ogen uit
}
```

Upload bovenstaande code in de Wink en probeer het eens uit. Je zal 2 dingen merken wanneer het programma wordt gestart. Het eerste is dat de Wink niet helemaal rechtuit gaat. De Wink heeft geen besef van rechtdoor, hij draait de motoren gewoon op volle snelheid. Zoals met alle mechanische apparaten, zal de ene motor net wat sneller draaien dan de ander, en zal net de ene motor een betere grip hebben dan de andere. Hier zullen we straks nog beter naar gaan kijken.

Het andere wat je wellicht hebt gemerkt is dat de Wink niet direct grip heeft en eventjes blijft spinnen en daarna de controle verliest. Dit is omdat de motoren heel snel van geen naar een snelle beweging gaan. Dit zorgt ervoor dat de motoren geen grip krijgen op de oppervlakte. Echte auto's hebben hetzelfde probleem als ze te hard versnellen.

Laten we eens kijken wat we kunnen aanpassen om deze problemen te verhelpen.

##De juiste versnelling##
Wanneer we de motoren met `motors(255,255)` op volle snelheid draaien dan beginnen ze direct te spinnen. Dit zorgt ervoor dat de uiteinde van de motoren geen grip hebben op het oppervlakte, net zoals een race auto de banden opwarmt. De truc is om de snelheid geleidelijk te versnellen. We kunnen dit doen door `accelerateMotors()` te gebruiken.

Deze functie heeft 3 argumenten nodig om te werken. Deze functie zorgt ervoor dat de snelheid steeds wordt verhoogd in de loop van de tijd. Om dit te laten werken, moet je als eerste de startsnelheid opgeven, vervolgens de eindsnelheid en als laatste de tijd waarin de versnelling van de begin- naar de eindsnelheid moet plaatsvinden.

Je kan de functie als volgt gebruiken.

`accelerateMotors(startSpeed, endSpeed, timePeriod);`

Wanneer je een functie ziet, zoals we `accelerateMotors()` hierboven hebben beschreven, zie je ook vaak dat de argumenten van de functie beschreven worden. Als eerste argument van de functie is 'startSpeed' beschreven, dit betekent beginsnelheid. Als je de functie gebruikt in je code, zal je niet 'startSpeed' gebruiken maar een getal zoals 0, 100 of iets anders. We gebruiken juist deze woorden om aan te geven waar de waarde voor wordt gebruikt, en wat de volgorde is van de argumenten in de functie. In dit geval zie je dat de eerste waarde de beginsnelheid is.

Omdat we stilstaan wanneer we de race beginnen zullen we de beginsnelheid (startSpeed) op 0 zetten. Het volgende argument is de eindsnelheid (endSpeed). Dit is de snelheid waarmee de motoren eindigen als de functie klaar is. Het laatste argument is 'timePeriod', dit is de tijd die het duurt (in milliseconden) om van de beginsnelheid naar de eindsnelheid te versnellen.

Laten we eens kijken naar een voorbeeld en deze daarna beter bekijken.

``` c
// Start met de snelheid 0, versnel naar 100 over een periode 
// van 500 milliseconden (1/2 seconde)
accelerateMotors(0, 100, 500)
```

In bovenstaand voorbeeld worden de motoren beide op 0 gezet wanneer de functie wordt aangeroepen. De motoren zullen dan op snelheid 1 worden gezet, daarna op 2, enzovoort. De functie zal de snelheid gelijkmatig ophogen in de tijd van de ingegeven 'timePeriod'. Bij een korte tijdsperiode zal de versnelling sneller gaan.

In ons race programma zou een langzame versnelling betekenen als het lang duurt voordat we de maximale snelheid hebben behaald, en dat we wellicht verliezen van een snellere robot. Aan de andere kant, als we de tijd van de versnelling te kort instellen zou het kunnen dat de motoren niet voldoende grip hebben. De truc is om de Wink zo snel mogelijk te laten gaan in zo kort mogelijke tijd met zo veel grip op de oppervlakte als mogelijk. Je zal zelf moeten experimenteren om dit goed te krijgen voor jouw eigen Wink.

In het algemeen werkt een versnelling van 0 tot 240 goed, en dat in een periode van 350 milliseconden. Laten we dit eens toevoegen aan onze code en kijken wat gebeurt. We zouden moeten zien dat de Wink niet meer gaat spinnen en de controle verliest. Probeer de waardes van `accelerateMotors()` maar eens aan te passen totdat de Wink goed versneld.

``` c
/*
 Nadat op het knopje is gedrukt start het aftellen (2 seconden op rood, daarna kort op
 groen en geef een geluidje bij de start), waarna de Wink zo hard als 
 mogelijk gaat versnellen om de spin bij de start te vermijden. 
 Na 1 seconde stopt de Wink met de race.
*/
void loop() {
	waitForButton();// Wachten totdat op het knopje wordt gedrukt
	
	// Eerste keer knipperen
	eyesRed(100); 	// Maak de ogen rood
	beep(1000); 	// Geef een geluidje voor 1 seconde
	eyesOff(); 		// Zet de ogen uit
	delay(200);		// Wacht 2 seconden
	
	// Tweede keer knipperen
	eyesGreen(100); // Zet de ogen op groen
	beep(25);		// Kort geluidje

	// GO!!
	accelerateMotors(0, 240, 350) // Versnel in 350 milliseconden van 0 naar 240
	motors(255,255); // Beide motoren op volle snelheid voor de rest van de tijd
	
	// Wacht totdat de race over is
	delay(1000);	// Rijd de Wink voor 1 seconde
	
	//STOP! 
	beStill(); 		// Stop met bewegen
	eyesOff();		// Zet de ogen uit
}
```

##De Wink op het rechte pad##
Zoals we al eerder hebben besproken worden de wielen (of voeten van de kever) door 2 verschillende motoren aangestuurd. Dit zorgt er vaak voor dat een van de motoren iets sneller gaat dan de ander. Er zijn kleine verschillen ontstaan tijdens het maken van de motoren waardoor ze niet exact hetzelfde zijn, waardoor we altijd wat verschillen zien zelfs als ze door dezelfde batterij worden gevoed. Elke Wink robot zal dus iets anders reageren dan de ander. Als je heel veel geluk hebt dan zal de Wink vanaf het begin in een rechte lijn rijden, maar meestal zal je zien dat jouw Wink iets meer naar rechts of links stuurt.

We kunnen de robot rechter laten rijden door de snelheid van de linker of rechter motor aan te passen in de code van ons race programma. Kijk maar naar het plaatje hieronder.

![Wink motor aanpassing](https://github.com/meijerpeter/winktutorial-nl/blob/master/img/wink-motor-directions-4.png)

Zoals je kan zien in dit plaatje, als de Wink de neiging heeft om meer naar links te gaan zal de RECHTER motor sneller draaien dan de linker. Andersom zal de LINKER motor iets harder draaien als de Wink naar rechts afwijkt.

We kunnen dit aanpassen in onze code. We kunnen verschillende snelheden aan de beide motoren meegeven in de `motors()` functie in de GO!! sectie van ons race programma. Probeer maar eens de waarde aan te passen, afhankelijk van of jouw Wink naar links of rechts afwijkt. 

Als je Wink meer naar de linkerkant moet sturen, probeer je het volgende.....

``` c
motors(255,245)	// De RECHTER motor zal iets langzamer draaien
```

Als je Wink meer naar de rechterkant moet sturen, probeer je het volgende.....

``` c
motors(245,255)	// De LINKER motor zal iets langzamer draaien
```

Door met de waardes van de `motors()` functie te spelen, zal je zien dat je Wink uiteindelijk redelijk rechtdoor kan rijden. Als het goed is hoeft je de waardes niet meer dan 30 te laten verschillen. Probeer in stapjes van 5 de waardes van de argumenten aan te passen totdat de Wink rechtdoor rijdt.

##Racende Winks!!##
Om met de robot te racen, zoek je een vriend op die ook een Wink heeft. Vind een lange ondergrond zoals bijvoorbeeld een tafel of een leeg stuk vloer. Als je de tafel gebruikt zorg dan voor een paar vrienden die zorgen dat de Wink niet op de grond valt. Als je de vloer gebruikt zorg dan voor een afgebakend gebied de duidelijk aangeeft dat er ge-raced gaat worden. We willen geen platgetrapte Winks!

Afhankelijk van de lengte van de racebaan zou je ook de `delay(1000);` kunnen aanpassen in het "Wacht tot de race over is" sectie van de code. Als je een ruime racebaan hebt zou je de waarde hoger kunnen zetten om de Wink langer te laten racen. Als je een kleine ruimte op een tafel hebt zou je het getal kunnen verlagen, zodat je niet het risico hebt dat de Wink van de tafel valt. Onthoud dat met `delay(1000);` de race 1 seconde duurt, als je de race 2 seconden wil laten duren kan dit met `delay(2000);`.

Zet je Wink robots klaar aan het begin van de racebaan, waarna 1 persoon gaat aftellen met "Klaar voor de start?, AF!". Bij het woord "AF!" druk je gelijktijdig het knopje van de Wink in. Daarna heb je 1 seconde om de Wink recht op de racebaan te zetten voordat de motoren gaan draaien.

Soms heb je geluk en heb je een mooie gelijkmatige race. Soms zal de Wink toch nog spinnen, of onbedoeld een andere kant op gaan. Dit gebeurt in een echte drag race ook wel eens. Je kan van te voren niet altijd voorspellen hoe de race zal verlopen.

Tussen de races door kan je natuurlijk je code aanpassen om de Wink beter te laten racen. Als de Wink bij de start nog een beetje spint en daardoor gaat draaien dan heb je nog niet voldoende grip en versnel je waarschijnlijk te snel. Om dit te voorkomen moet je de tijd (timePeriod) waarin de versnelling plaatsvindt wat langer maken in je `accelerateMotors()` functie. Als je geen last hebt van het spinnen van de wielen aan het begin, zou je de tijd juist wat korter kunnen zetten. Dit resulteert in een snellere versnelling en wellicht dat je hierdoor juist kan winnen, maar ook meer risico hebt op een spin bij de start. Dit zal je zelf moeten ontdekken wat het beste werkt!

Wellicht ontdek je ook wel dat je bij een lagere eindsnelheid een beter gecontroleerde race krijgt, waarbij de Wink zich beter gedraagt. Als jij namelijk wel de overkant haalt en je tegenstander niet, dan win je alsnog.

Voel je vrij om de getallen in het voorbeeld aan te passen. Je kan de kleuren van de ogen aanpassen, of de ogen van Wink laten knipperen tijdens de race door de functies die je hebt geleerd in de tweede les toe te passen. Je kan ook de ogen in verschillende ritmes laten knipperen tijdens het aftellen in de "Eerste keer knipperen" en de "Tweede keer knipperen" sectie in je race programma. Bijvoorbeeld snel achter elkaar, in verschillende kleuren. Pas het lekker aan zoals jij wil!

Later zullen we meer leren over het gebruik van de programmeertaal om bijvoorbeeld een leuke "for" loop te maken, waarmee we iets een aantal keren kunnen herhalen. Met de "for" loop kunnen we het aftellen voor de race wat leuker maken...

> Learn to Code - Ch05 Rev01.2 ~ Plum Geek
 


