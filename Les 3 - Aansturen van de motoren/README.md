#Aansturen van de Wink's motoren#

##Functies om de motor aan te sturen##

Het is tijd om de Wink te laten rijden! Het aansturen van de motoren is heel makkelijk. De motors worden aangestuurd door een simpele functie `motors()`. De functie werkt als volgt.

``` c
  motors(left, right); 	// de motors() functie kent 2 argumenten; de snelheid van de 
						// linker en rechter motor worden meegeven.
						// de waarde hiervan kan varieren van 0 tot 255.
						// Een positief getal zorgt voor voorwaardse beweging, een
						// negatief getal zorgt ervoor dat de Wink naar achter beweegt.

```

Laten we eens naar een voorbeeld kijken, dan zien we wat er gebeurt.

``` c
/*
 Zowel de linker als rechter motor bewegen voor 1 seconde naar voren met 
 een snelheid 150. Daarna gaan ze beide naar achter, ook voor 1 seconde. 
 Dit blijft zich continu herhalen.
*/
void loop() {
  motors(150,150); 	// Beide motoren gaan naar voren met de snelheid van 150
  delay(1000); 		// Wacht 1 seconde
  motors(-150,-150); // Beide motoren bewegen naar achter
  delay(1000);		// Wacht 1 seconde en begin opnieuw
}
```

Zie je wat er gebeurt is? De Wink beweegt zodra de motoren draaien. Als de linker en rechter motor beide naar voren draaien, zal de Wink naar voren gaan. Draaien ze naar achter, dan zal de Wink naar achter gaan.

![Wink motoren](https://github.com/meijerpeter/winktutorial-nl/blob/master/img/wink-motor-directions.png)

##Een bochtje maken##
We hebben net gezien wat er gebeurt als beide motoren dezelfde snelheid hebben. De Wink gaat dan meestal recht vooruit. Als we nu beide motoren ieder een andere kant op laten draaien, dan draait de Wink een rondje!

``` c
/*
 De positieve waarde voor de linker motor (1ste argument) zal de linker kant naar 
 voren bewegen, het negatieve nummer voor de rechter motor (2e argument) zal de 
 rechterkant naar achteren bewegen.
 
 Het omgekeerde zorgt voor een rondje de andere kant op.
*/
void loop() {
  motors(250,-250);	// Draai een rondje naar rechts
  delay(3000); 		// Wacht 3 seconden
  motors(-250,250); // Draai een rondje naar links
  delay(3000);		// Wacht 3 seconden en begin opnieuw 
}
```

![Wink rondje](https://github.com/meijerpeter/winktutorial-nl/blob/master/img/wink-motor-directions-2.png)

Met het volgende voorbeeld moet je voorzichtig zijn dat de Wink niet van tafel valt. Als we de motoren beide naar voren laten draaien, maar op verschillende snelheden dan zal de Wink een lange bocht maken. De Wink kan uiteraard ook een bocht naar achter maken door gebruik te maken van negatieve waardes in de `motors()` functie.

``` c
/*
 Als beide waarden positief zijn maar met een verschillende waarde zal de ene motor 
 sneller gaan dan andere, zodat de Wink een bocht maakt.
 
 Voorzichtig dat de Wink niet van de tafel afvalt!!
*/
void loop() {
  motors(150,100);	// Maak een bocht naar rechts
  delay(1000); 		// Wacht 1 seconde
  motors(100,150); 	// Maak een bocht naar links
  delay(1000);		// Wacht 1 seconde
}
```

![Wink bocht](https://github.com/meijerpeter/winktutorial-nl/blob/master/img/wink-motor-directions-3.png)

##Een paar andere functies om de motoren aan te sturen##
We hebben nog een paar andere functies gemaakt om het makkelijk te maken om de motoren aan te sturen.

Zo kan je de Wink laten draaien om zijn as door `spinRight()` en `spinLeft()` aan te roepen. Als argument kan je een waarde tussen de 0 en 255 meegeven. Met deze waarde bepaal je de snelheid waarmee de Wink draait. De spin functies laten de motoren beide een tegengestelde kant op draaien.

``` c
/*
 Gebruik de spin functies om de Wink om zijn as te laten draaien. Dit wordt gedaan door
 de motoren in tegengestelde richting te laten draaien.
*/
 void loop() {
   spinRight(200);	// De Wink draait naar rechts met een snelheid van 200
   delay(2000); 	// Wacht 2 seconden
   spinLeft(200); 	// Draai de Wink naar links met dezelfde snelheid
   delay(2000);		// Wacht 2 seconden en begin opnieuw
}
```

Je kan ook de Wink stoppen door de functie `beStill()` te gebruiken. In deze functie worden geen argumenten meegegeven en zorgt ervoor dat de Wink direct de beweging van de motoren stopt.

``` c
/*
 Als je de Wink wil stoppen, kan je eenvoudig gebruik maken van de beStill(); functie.
 Deze functie zorgt ervoor dat de motoren van Wink meteen stoppen.
*/
void loop() {
  motors(150,150);	// Beweeg beide motoren op snelheid 150
  delay(1000); 		// Wacht 1 seconde
  beStill(); 		// Stop met bewegen
  delay(3000);		// Wacht 3 seconden
}
```

Als laatste is er ook nog een functie om de Wink geleidelijk te laten versnellen, dit is de `accelerateMotors()` functie. Deze functie is handig voor de "drag race" in een latere oefening. Deze functie zorgt ervoor dat de Wink start met het draaien van de motoren met een bepaalde snelheid, waarna de snelheid van de motoren geleidelijk wordt verhoogd over een bepaalde periode. De `accelerateMotors()` functie kent 3 argumenten; de beginsnelheid, de eindsnelheid en de tijd waarin het versnelt naar de eindsnelheid. De tijd wordt in milliseconde meegegeven, dus een waarde van 1000 zal de Wink in 1 seconde van de begin- naar de eindsnelheid laten gaan. Een korte tijd zorgt voor een snelle acceleratie, een langere tijd zal de Wink rustiger laten versnellen. Meer hierover bij de drag race lessen.

``` c
/*
 Een geleidelijke versnelling van stilstand naar top snelheid, in een periode van 
 2 seconden (2000 milliseconden). Na 3 seconden gaat de Wink opnieuw versnellen.
*/
void loop(){
  accelerateMotors(0,250,2000); // Versnel de Wink van 0 naar 250 in 2 seconden
  beStill(); 					// Stop de Wink volledig
  delay(3000); 					// Wacht 3 seconden en begin opnieuw 
}
```

##Een paar opmerkingen over de motoren##
Wat je waarschijnlijk al wel gezien hebt is dat als je motoren op dezelfde snelheid zet, dat de Wink niet geheel in een rechte lijn rijdt. Waarschijnlijk zal de Wink een beetje naar links of rechts afwijken. Dit komt omdat de mechanische motoren nooit helemaal perfect zijn. De ene motor is misschien net iets krachtiger dan de andere, en misschien zal de andere motor net wat meer de oppervlakte van de vloer of tafel aanraken. Dit veroorzaakt de afwijkingen in de rechte lijn. Later zullen we zien hoe we dit moeten compenseren. s