#Les 2 - Aansturing van de ogen#

##Functies om de ogen te veranderen##

Laten we eens met de ogen van de Wink gaan spelen. 
Het is heel makkelijk, je zal verbaasd zijn!

``` c
/*
Hier gebeurt het! Alles binnen de loop() functie wordt continu uitgevoerd. 
De meeste code schrijf je binnen deze functie.
*/
void loop(){
  eyesPurple(100); //both eyes purple at 100 brightness

  delay(3000); //3 seconden wachten
  rightOff(); //uitzetten van het rechter oog
  delay(250); //1/4 seconde wachten
}
```

De *loop* functie doorloopt elke regel code van boven naar onder. Wanneer de laatste regel is uitgevoerd binnen de `loop()` functie, zal de eerste regel weer beginnen en begint het van voor af aan.

De functie `eyesPurple();` zet beide ogen aan in de kleur paars. De `delay()` functie zorgt ervoor dat de computer een bepaald aantal millisecondes wacht. Er zijn 1000 milliseconden in 1 seconde. Je kan allerlei verschillende oog functies en wachttijden binnen de *loop* functie zetten om verschillende interessante oogkleur combinaties te maken.

Hieronder is een lijst van de functies die er zijn om de kleuren van de ogen te veranderen.

**Beide ogen in dezelfde kleur:**
`eyesRed(); eyesGreen(); eyesBlue(); eyesPurple(); eyesPink(); eyesYellow(); eyesOrange(); eyesCyan(); eyesWhite();`

**Alleen het LINKER oog veranderen:**
`leftRed(); leftGreen(); leftBlue(); leftPurple(); leftPink(); leftYellow(); leftOrange(); leftCyan(); leftWhite();`

**Alleen het RECHTER oog veranderen:**
`rightRed(); rightGreen(); rightBlue(); rightPurple(); rightPink(); rightYellow(); rightOrange(); rightCyan(); rightWhite();`

**De exacte R(ood)G(roen)B(lauw)-kleur aansturen. Toegestane waardes liggen tussen de 0 en 255:**
``` c
 eyesRGB(red,green,blue); //beide ogen dezelfde kleur
 leftRGB(red,green,blue); //kleur het linker oog
 rightRGB(red,green,blue); //kleur het rechter oog
```

**Uitzetten van de ogen**
``` c
 eyesOff(); //uitzetten van beide ogen
 leftOff(); //uitzetten van het linker oog
 rightOff(); //uitzetten van het rechter oog
```

**Terugzetten van de vorige kleur van het oog**
``` c
 eyesPrevCol(); //zet de kleur van de ogen naar de voorgaande kleur
 leftPrevCol(); //zet de kleur van het LINKER oog naar de voorgaande kleur
 rightPrevCol(); //zet de kleur van het RECHTER oog naar de voorgaande kleur
```

##Aansturen van de lichtsterkte##

Wanneer we de Wink vertellen om een kleur van het oog te zetten, moeten we ook vertellen hoe sterk het licht moet zijn. Om dit te doen moet een waarde worden meegegeven in deze functie. In bovenstaand code voorbeeld staat `eyesPurple(100);` die vertelt dat de ogen paars moeten worden met een lichtsterkte van 100. Elk oog kan een lichtsterkte aannemen tussen de 0 en 255, waarbij 0 het oog uit zet en bij 255 de lichtsterkte maximaal is. Je kan de lichtsterkte aanpassen door de waarde tussen de haakjes te zetten. Een beginwaarde van 100 is prima om mee te starten. De ogen geven behoorlijk veel licht, dus normaliter zijn de hoge waardes niet nodig en zal daarnaast ook de batterij sneller leeg raken. In sommige gevallen zal het handig zijn om de waarde toch hoger te maken om de ogen feller te laten schijnen.

##Probeer eens een ander voorbeeld##
We hebben al de Wink zien *knipogen*, laten we nu eens een langer voorbeeld proberen. Kijk maar eens naar onderstaande code en pas dit eens zelf aan. Probeer maar eens de `leftCyan(100)` functie aan te passen naar een functie uit de bovenstaande lijst. Ook kan je eens de waarde in de `delay()` functie aanpassen. Als je compiler errors krijgt, kijk dan hieronder eens voor tips om deze op te lossen.

``` c
void loop() {
 /*
 Knipper tweemaal met het linkeroog. De code voor regel voor regel uitgevoerd.
 Elke regel wordt een *statement* genoemd, die altijd met een punt-komma 
 moet worden beeindigd. Dit is het ; symbool
 */
 leftCyan(100); //linker oog wordt cyaan (turquoise)
 delay(20); //wacht een korte tijd
 eyesOff(); //beide ogen uit
 delay(100);  //wacht tussen het knipperen
 leftCyan(100); //linker oog wordt cyaan
 delay(20); //wacht weer een korte tijd
 eyesOff(); //beide ogen weer uit

 delay(2000); //wacht 2 seconden
 
 /*
 Knipper nu tweemaal het rechteroog. De functies zijn hoofdletter-gevoelig,
 dit wil zeggen dat je precies de juiste kleine- en hoofdletters moet gebruiken.
 */
 rightCyan(100); 	//kleur nu het rechter oog cyaan
 delay(20); 		//wacht een korte tijd
 eyesOff(); 		//beide ogen uit
 delay(100); 		//wacht tussen het knipperen
 rightCyan(100); 	//rechter oog wordt cyaan
 delay(20); 		//wacht weer een korte tijd
 eyesOff(); 		//beide ogen uit
 
 delay(2000); //wacht 2 seconden
}
```

##Het onthouden van de vorige kleur##
Je kan `eyesPrevCol()`, `leftPrevCol()`, and `rightPrevCol()` gebruiken om de kleur van de ogen terug te zetten naar de vorige kleur. Dit is handig als je de ogen wil laten knipperen. Je hoeft geen lichtsterkte mee te geven met deze functies, ze zetten de kleur en de lichtsterkte precies zoals jij het de voorgaande keer hebt gezet.

Kijk maar eens naar dit voorbeeld.

``` c
/*
Wanneer je eyesOff(); gebruikt onthoudt Wink welke kleur en lichtsterkte 
werd gebruikt voordat ze uit gaan.
*/
void loop() {

 eyesRed(100); 	//maak de beide ogen rood
 delay(20); 	//knipper even kort
 eyesOff(); 	//beide ogen uit
 delay(100); 	//wacht even tussen het knipperen
 
 /*
 Wanneer je eyesPreCol(); gebruikt kan je de kleur en lichtsterkte
 weer terughalen van de vorige keer.
 */ 
 eyesPrevCol(); //zet de ogen aan met de vorige kleur (rood, 100)
 delay(20);		//knipper even kort
 eyesOff(); 	//beide ogen weer uit
 delay(2000);	//wacht 2 seconden
}
```

##Het aanpassen van de lichtsterkte##
Laten we eens kijken wat er gebeurt als we de lichtsterkte van de ogen aanpassen. Gebruik onderstaande code voorbeeld en pas eens iets aan om te zien wat er bij de Wink veranderd.

``` c
/*
In dit programma worden de ogen van de Wink van zwak naar fel gemaakt.
Elke lichtsterkte wordt even getoond, het wordt steeds iets sterker.
*/
void loop() {
 eyesBlue(25); 	// maak beide ogen blauw, lichtsterkte is 25
 delay(200); 	// korte pauze
 eyesBlue(75); 	// maak beide ogen blauw, nu met lichtsterkte 75
 delay(200); 	// korte pauze
 eyesBlue(125); // maak beide ogen blauw, nu met lichtsterkte 125
 delay(200); 	// korte pauze
 eyesBlue(175); // maak beide ogen blauw, nu met lichtsterkte 175
 delay(200); 	// korte pauze
 eyesBlue(225); // maak beide ogen blauw, nu met maximale lichtsterkte 255
 delay(200);	// korte pauze

 /*
 Aan het einde van het programma worden de ogen uitgezet en na een korte pauze
 start het programma opnieuw
 */
 eyesOff(); 	// beide ogen uit
 delay(1000);	// 1 seconde wachten voordat het opnieuw start
}
```

##Maak je eigen kleur##
Met de methodes zoals `eyesBlue()` kan je eenvoudig de ogen kleuren, maar je kan ook de ogen elke kleur geven die je wil. Elk oog bestaat eigenlijk uit 3 individuele kleuren; een rode, een groene en een blauwe. Door elke kleur in lichtsterkte te varieren kan je elke kleur maken die je kan bedenken. Je kan zelf de exacte waardes van de rode, groene en blauwe kleur zetten met de `eyesRGB()` functie. Kijk maar...

``` c
/*
De eyesRGB() functie accepteert 3 argumenten. Deze argumenten zijn de 3 waardes die
je in de functie meegeeft. Ze worden door komma's gescheiden. De eerste waarde is de
kleur rood (220 in dit geval), de tweede is de groene kleur (waarde 20) en als laatste 
de kleur blauw (waarde 160). De waarde van deze argumenten liggen tussen de 0 en 255.

Als je ze allemaal dezelfde waarde geeft wordt het licht wit! Cool he?!
*/
void loop() {
 //zet rood op 220, groen op 20 en blauw op 160
 eyesRGB(220, 30, 160); 	// Pruimen paars!!
 delay(300);
 
 eyesRGB(100, 100, 100);	// zet ze allemaal tegelijk op wit! 
 delay(300);
}
```

Je kan ook afzonderlijk de kleur van de ogen zetten, dit doe je eenvoudig met de functies `leftRGB()` en `rightRGB()`.

``` c
/*
Je kan de ogen afzonderlijk aanpassen. In dit voorbeeld laten we het linker en rechter
oog in verschillende kleuren knipperen.
*/
void loop() {
 leftRGB(220, 30, 160);		// linker oog paars
 rightRGB(100, 100, 100);   // rechter oog wit
 delay(500);
 
 leftRGB(100, 100, 100); 	// linker oog wit
 rightRGB(220, 30, 160);	// rechter oog paars
 delay(500);
}
```

De functies `eyesRGB()`, `leftRGB()` en `rightRGB()` zijn de meest krachtige methodes om de kleur van de ogen aan te sturen omdat je hiermee exact de waardes kan bepalen.

##Wat te doen bij een compileer error?##
Om de leesbare broncode om te zetten in instructies die het brein van de robot begrijpt, moeten we de code op de juiste manier schrijven. Hierbij moeten bepaalde regels worden gevolgd.
Als je een fout in je code maakt, dan zal de Arduino het niet compileren en dus niet kunnen omzetten naar de instructies die de robot begrijpt. De fouten worden getoond in het berichten scherm in oranje meldingen. Laten we eens kijken naar veelgemaakte fouten die je tegen kan komen.

###Sluit je regel altijd af met een punt-komma###
``` c
eyesBlue(50); // dit is juist
eyesBlue(50)  // zonder punt-komma gaat het niet werken
eyesBlue(50): // dit is een dubbele punt, geen punt-komma, incorrect
eyesBlue(50), // dit is een komma, geen punt-komma, ook incorrect
```

###Kijk goed naar je kleine en hoofdletters###
Sommige functies gebruiken alleen kleine letters zoals `delay()`, andere starten met kleine letters en gebruiken ook een hoofdletter zoals `eyesBlue()`.

``` c
eyesBlue(50); // correct gebruik van kleine en hoofdletter. Dit werkt!
EyesBlue(50); // Werkt niet, onjuist gebruik van de hoofdletter aan het begin
eyesblue(50); // kleine letters werkt ook niet
EYESBLUE(50); // alleen hoofdletters is ook niet correct

delay(100);   // correct, de functie "delay" schrijf je met kleine letters
Delay(100);   // incorrect
```

###Gebruik van haakjes###
Je moet normale haakjes `()` gebruiken om argumenten in een functie mee te geven.

```c
eyesRGB(120, 50, 90); // correcte haakjes, dit gaat werken!
eyesRGB{120, 50, 90}; // je mag geen accolades gebruiken
eyesRGB[120, 50, 90]; // ook vierkante haken mogen niet
```

###Spaties in je code###
Extra spaties in je code worden "white spaces" genoemd in het engels. In de taal C, die je nu aan het leren bent, zijn white spaces meestal toegestaan. Leer jezelf aan om leesbare code te schrijven door op zo veel mogelijk dezelfde manier met spaties om te gaan.

```c
eyesRGB(120,50,90); 	// Dit is goed
eyesRGB( 120, 50, 90);  // Dit mag ook
eyesRGB (120,  50,  90)	// Ook dit mag, maar wordt niet veel gebruikt
```

###Hoe ziet een foutmelding er uit?###

![Arduino foutmelding](https://github.com/meijerpeter/winktutorial-nl/blob/master/img/arduino-compile-error.png)

Hierboven zie je een voorbeeld van een foutmelding in de Arduino IDE. In dit voorbeeld zijn we vergeten een punt-komma achter de eerste `delay()` te zetten. Vaak wordt hierdoor de regel eronder in het rood aangegeven. Bekijk de regel boven de rode regel om te zien waar de fout zit.

Ook kan je de foutmelding lezen, deze wordt in het oranje onderaan weergegeven. Deze staan wel in Engels, dus pak je woordenboek erbij, gebruik https://translate.google.nl, of vraag het iemand in de buurt!