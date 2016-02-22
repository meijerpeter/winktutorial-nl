#Les 7 - Debuggen (met de SerialPrint functie)#
##Laat je Wink tegen je praten##

Zou het niet super leuk zijn als de Wink tegen je kan vertellen wat hij denkt? Nou dat kan, en we gaan in deze les vertellen hoe je dat kan doen. Meestal is het gebruikelijk voor een computerprogramma om iets terug te geven aan de gebruiker. Dit is zeer handig als je wat ingewikkelde programma's aan het schrijven bent, dan kan het programma je vertellen wat er precies gebeurt. Soms heb je een blok code die niet helemaal precies doet wat je had verwacht, dan kan juist die informatie vanuit de computer je helpen om het probleem op te lossen. Dit noemen we het "debuggen" van je programma.

We gaan gebruik maken van de `Serial.print` functie in deze les. Het woord "serial" (of "serieel" in het Nederlands) in computertermen betekent meestal dat je kleine stukjes informatie via een verbinding kan versturen. Wanneer je de Wink met de programmeer adapter verbindt, en de adapter is verbonden met de USB poort van je computer, dan kan de Wink via deze connectie informatie vanuit zijn brein terugsturen naar jouw computer. Serial kan voor verschillende doeleinden worden gebruikt, maar in ons geval gaan we het gebruiken om informatie op je computerscherm te "printen", dus `Serial.print` beschrijft goed wat we doen.

![Serial.print monitor](https://github.com/meijerpeter/winktutorial-nl/blob/master/img/serial-print-monitor.png)

Je computer zal de uitkomst van `Serial.print` in het Arduino Serial Monitor scherm laten zien. Om dit scherm te openen, moet je op het vergrootglas klikken rechtsboven in van de Arduino IDE. Hierna opent een wit scherm. Je kan dit scherm verplaatsen en van grootte veranderen, net zoals jij het wil. Zorg dat rechtsonder in het scherm de snelheid (speed) op 57600 Baud is gezet.

##Serial.print functies##
Nu dat we het Serial Monitor scherm open hebben, kunnen we eens kijken hoe we deze functie moeten gebruiken. `Serial.print` kan gebruikt worden om tekst (zoals letters en cijfers) te versturen, maar ook de waarde van variabelen. Laten we eens naar een voorbeeld gaan kijken...

```c
#include WinkStuff.h

/*
 Normale setup
*/
void setup(){
  hardwareBegin();
  playStartChirp();
}

/*
 Verzend een tekst "My name is Wink" via de seriele poort, wacht vervolgens
 1 seconde voordat we opnieuw beginnen.
*/
void loop(){
  Serial.print("My name is Wink");
  delay(1000);
} //einde van de loop
```
In dit voorbeeld zal de functie `Serial.print` alles "printen" wat binnen de aanhalingstekens (") staat. De aanhalingstekens worden zelf niet geprint, deze vertellen het programma dat de teksts tussen de aanhalingstekens moeten worden geinterpreteerd als een serie van letters en niet als een variabele.

Probeer bovenstaand voorbeeld maar eens te draaien en kijk maar wat er gebeurt. Je zal zien dat `My name is Wink` elke seconde wordt geprint in je Serial Monitor scherm. Je ziet ook dat het rode Tx lampje op de programmeer adapter elke keer oplicht. Dit lichtje knippert elke keer als de Wink iets naar je computer verstuurt over de seriele poort.

Misschien heb je ook opgemerkt dat elke keer als de tekst wordt geprint dit over de vorige regel heen wordt geschreven. Er verschijnt geen spatie, return of nieuwe regel in het scherm. De reden hiervoor is dat we niet tegen het programma hebben verteld om dit te gebruiken. `Serial.print` verzendt exact wat je het vertelt en niets meer. Als je elke keer een nieuwe regel wil maken als je `Serial.print` gebruikt, dan zal je dit aan de functie kenbaar moeten maken door een speciaal teken te gebruiken.

Om een nieuwe regel te maken moet je een back-slash met de kleine letter "n" versturen. Wanneer het programma de back-slash (\)) ziet, dan zal het in het echt niet de back-slash maar een speciaal teken versturen naar de computer. Laten we dit voorbeeld eens uitproberen:

```c
/*
 Verzend het speciale teken voor een "nieuwe regel" aan het einde van
 de tekst. Dit zorgt ervoor dat de Serial Monitor een nieuwe regel start.
*/
void loop(){
  Serial.print("My name is Wink!\n");
  delay(1000);
} //einde van de loop
```

Je kan ook een nieuwe regel beginnen met een functie die net een klein beetje anders is, genaamd `Serial.println()`. De functie print met een "ln" erachter betekent "Serial Print Line", dit werkt hetzelfde als de functie `Serial.print` maar dan wordt er elke keer een nieuwe regel aangemaakt.

Deze nieuwe functie met `Serial.println` werkt net zoals in het vorige voorbeeld waarbij we de "\n" toevoegen aan het einde van de series met karakters. Je kan je code op beide manieren schrijven, maar `Serial.printnl` ziet er net iets mooier uit en is wellicht handiger om te gebruiken.

Probeer dit maar eens...

```c
/*
 Serial.println maakt automatisch een nieuwe regel aan.
 Dit zorgt ervoor dat de Serial Monitor een nieuwe regel start.
*/
void loop(){
  Serial.println("My name is Wink!");
  delay(1000);
} //einde van de loop
```

Je kan ook een series van karakters versturen met de normale `Serial.print()` zonder de speciale "\n", om in de volgende regel code de `Serial.println()` aan te roepen zonder argument om een nieuwe regel aan te maken. Kijk hier maar naar:

```c
/*
 Serial.println zonder argument maakt ook automatisch een nieuwe regel aan.
 Dit zorgt ervoor dat de Serial Monitor een nieuwe regel start.
*/
void loop(){
  Serial.print("My name is Wink!");
  Serial.println();
  delay(1000);
} //einde van de loop
```

##Printen van de variabelen##
Je kan ook de waarde van een variabele printen op dezelfde manier, behalve dat je de naam van de variabele zonder aanhalingstekens moet gebruiken. Herinner je de vorige les nog waarbij we het aantal keer dat de `loop()` functie was gestart moesten onthouden? Laten we dit voorbeeld eens gebruiken, maar nu laten we de Wink de waarde vertellen elke keer als de functie opnieuw begint. Zoals dit:

```c
int loopCount = 0;

/*
 Dit stukje code print het aantal keer dat het de functie loop() doorloopt,
 daarna stuurt het een nieuwe regel. Vervolgens telt het 1 op bij de vorige
 waarde van loopCount en slaat dit op in loopCount.
*/
void loop(){
  Serial.print(loopCount);
  Serial.println();
  delay(1000);
  loopCount = loopCount + 1; //Tel 1 op bij de huidige waarde van loopCount.
} //einde van de loop
```

Zou je wel eens willen weten hoe snel je Wink kan tellen? Wat als we de `delay(1000)` eens verwijderen van het vorige voorbeeld?

Voordat we dit proberen, laten we een paar dingen bekijken over de `Serial.print` functies. De tijd die de Wink nodig heeft om iets met 1 op te hogen duurt ongeveer een miljoenste van een seconde. Vervolgens wordt het resultaat naar je computer verzonden, dan weer opnieuw opgehoogd, daarna weer opnieuw verstuurd.

Dit zorgt voor een zeer grote overvloed aan seriele data die naar je computer wordt verstuurd. Als je computer deze informatie niet snel genoeg kan verwerken, dan zou je coputer heel langzaam kunnen worden. Het zou zelfs het Arduino programma kunnen crashen (dit is niet heel waarschijnlijk). Je zal ook zien dat het Serial Monitor scherm de teksten niet zo snel kan bijhouden, en dat de data veel sneller binnenkomt dan dat het scherm kan laten zien. Je zal zien dat het een stuk per keer ververst.

Als je onderstaand voorbeeld uitprobeert en je computer wordt erg traag, dan kan je de Wink uitzetten zodat er geen berichten meer worden verstuurd. Dan kan je de Arduino IDE opnieuw starten als het vast is gelopen (niet waarschijnlijk maar wel mogelijk) en het Serial Monitor scherm sluiten zodat het niet meer te zien is. Dit maakt het makkelijker om de Wink opnieuw te programmeren met een ander programma die niet je computer laat vastlopen.

Probeer het maar eens (waarschijnlijk levert het geen problemen op).

```c
int loopCount = 0;

/*
 Dit stukje code print het aantal keer dat het de functie loop() doorloopt,
 daarna stuurt het een nieuwe regel. Vervolgens telt het 1 op bij de vorige
 waarde van loopCount en slaat dit op in loopCount.
*/
void loop(){
  Serial.println(loopCount);
  delay(1000);
  loopCount = loopCount + 1; //Tel 1 op bij de huidige waarde van loopCount.
} //einde van de loop
```

Wanneer je deze code zal uitvoeren, dan zal je waarschijnlijk een paar interessante dingen zien als je naar het Serial Monitor scherm kijkt. Het eerste is dat het optellen zeer snel gaat, wat we al verwachten. Maar de tijd die het kost voor de Wink om iets op te tellen is een miljoenste van een seconde. Dit betekent dat de Wink een miljoen keer iets kan optellen in 1 seconde. Maar je ziet dat het niet zo snel gebeurt. De belangrijkste reden hiervoor is dat het ook een bepaalde tijd nodig heeft om het bericht naar de computer te versturen, bit voor bit over de seriele verbinding.

Het tweede wat je zal opmerken is dat als je wacht totdat de optelsom 32.767 bereikt het opeens negatief 32.768 (dit wordt getoond als -32768) wordt. Dit komt omdat, zoals we dat in de vorige les over variabelen hebben geleerd, de waarde "omrolt" zodra het hoogste getal is bereikt naar het laagste getal die in de variabele past. Voor de "int" variabele is dit -32.768. Elke keer dat `loop()` wordt uitgevoerd, wordt 1 bij de negatieve waarde opgeteld waardoor deze langzaam minder negatief wordt en naar 0 gaat om vervolgens weer positief te worden.

##Mixen van String en Variabelen##
Tot nu toe hebben we gesproken over de waarde binnen de aanhalingstekens als een serie van karakters. Nu je een beetje weet hoe je de functie moet gebruiken, laten we eens praten over wat een "string" of "serie van karakters" eigenlijk is.

Een string is een verzameling van karakters (zoals letters, nummers, spaties, symbolen zoals punten en komma's, uitroeptekens, dollar tekens, etc.). Het woord "konijn" is een string. Je kan ook een getal in een string zetten, zoals "Ik heb 2 konijnen". Dit is prima, zolang het getal 2 maar niet verandert.

Maar wat als je nu een getal wil printen die continu verandert als je programma wordt uigevoerd?

Er zijn verschillende mogelijkheden om dit te doen, sommige zijn zeer complex, maar er is ook een makkelijke manier om dit te doen die je waarschijnlijk al had geraden toen je dit aan het lezen was. Laten we dit eens proberen:

```c
int loopCount = 0;

/*
 Dit stukje code print eerst het eerste gedeelte van de string met een extra
 spatie aan het einde. Vervolgens wordt het aantal keer dat het de functie
 loop() doorloopt geprint, daarna het tweede gedeelte met een extra spaties
 ervoor. Dan stuurt het een nieuwe regel. Vervolgens telt het 1 op bij de
 vorige waarde van loopCount en slaat dit op in loopCount.
*/
void loop(){
  Serial.print("Loop has run "); //Eerste gedeelte van de string
  Serial.print(loopCount);      //De waarde van loopCount
  Serial.print(" times");       //Het tweede gedeelte van de string
  Serial.println();             //Print een nieuwe regel
  delay(1000);                  //Wacht 1 seconde
  loopCount = loopCount + 1;    //Tel 1 op bij de huidige waarde van loopCount
} //einde van de loop
```

##Het resultaat van een functie printen##
Je kan ook het resulaat van functies printen, maar laten we eerst even kijken naar "functies" om te zien wat ze doen. We zullen er later nog dieper op ingaan, dus als je het nu niet helemaal begrijpt geeft dat niets.

Gedurende alle lessen heb je al vele functies gebruikt, `motors()` bijvoorbeeld is ook een functie. Een functie kan iets nuttigs doen, bijvoorbeeld de snelheid van de motoren aanpassen. Een functie kan bijvoorbeeld ook de ogen rood maken, en nog veel meer andere nuttige dingen doen. De functies die je tot nu toe hebt gebruikt geven geen waarde terug ("return" in het Engels). Deze functies worden aangeroepen, voeren vervolgens wat uit en als ze klaar zijn gaat het programma verder waar het was gebleven. Maar soms is het juist de bedoeling dat een functie een waarde retourneert. Bijvoorbeeld, je zou een functie kunnen maken die de waarde van een temperatuursensor uitleest, dan terugkomt met een waarde in "graden Celsius" van de huidige temperatuur.

Er is een interessante functie die met de Arduino wordt meegeleverd genaamd `millis()`. De `millis()` functie lijkt op een klokje in het brein van de Wink dat begint met tikken als de Wink wordt aangezet. De `millis()` "returns" het aantal milliseconden die er verstreken zijn na het aanzetten van de Wink.

Dit concept kunnen we beter uitleggen aan de hand van een tweetal stappen. Begin eens met deze code:

```c
unsigned long onTime; //declareer de variabele “onTime”.

/*
 De waarde die wordt geretourneerd door de functie millis() wordt toegekend
 aan de variabele onTime. Deze waarde wordt vervolgens geprint.
*/
void loop(){
  onTime = millis();
  Serial.print(“Wink has been running for “);
  Serial.print(onTime);   //print de waarde van de onTime variabele
  Serial.print(“ milliseconds.”);
  Serial.println();       //print een nieuwe regel
  delay(1000);            //wacht 1 seconde
} //end of loop()
```

Laten we nu eens bekijken wat er met de bovenstaande code gebeurd.

Het eerste wat opvalt is dat als we de variabele onTime declareren, we niet met de "int" variabele type gebruiken, maar we de computer vertellen om een variabele te maken van het type "unsigned long". Dit type staat in de tabel van de les over variabelen. Het moet een type zijn van "unsigned long" omdat dit het type is wat ook de functie `millis()` retourneert. Omdat de millis() teller van de Wink zeer groot kan worden als de Wink voor een langere periode wordt aangezet, moet wel een speciaal soort type variabele gebruikt worden omdat het type "int" niet genoeg geheugen reserveert om deze grote waarde in op te slaan.

Interessanter is wat in de eerste regel van de `loop()` functie gebeurd. Dit vertelt de Wink om de speciale functie `millis()` uit te voeren. Wanneer `millis()` wordt uitgevoerd zal het naar de speciale teller kijken die binnen in het brein van de Wink start met tellen zodra de Wink wordt aangezet, om vervolgens terug te keren naar de loop functie. Het keert niet alleen terug, maar het komt terug met een waarde, in dit geval de waarde van het aantal milliseconden die zijn verstreken terwijl de Wink aan stond. Het "is" teken (=) verteld om de Wink de waarde toe te kennen aan de variabele genaamd "onTime".

In de volgende regels code wordt de string "Wink has been running for " geprint, vervolgens de waarde van `onTime` aan `Serial.print` meegegeven om ook te printen. Daarna wordt " milliseconds" geprint.

Als je het niet helemaal kan volgen geeft dat niets, zoals we eerder hebben gezegd zullen we later dieper ingaan op deze materie. Het belangrijkste van dit voorbeeld is dat een functie een waarde retourneerd en dit toe kent aan een variabele.

Wanneer je deze functie daadwerkelijk uitvoert en je het Serial Monitor scherm opent, dan zal je zien dat de Wink elke seconde verteld hoe lang het al aan staat. Als het goed is zal de waarde ongeveer met 1000 omhoog gaan.

Laten we nu eens kijken naar de tweede stap van dit concept. Zoals we eerder al hebben verteld, kan je ook het resultaat van een functie direct in de `Serial.print` functie meegeven. Dan wordt de code alsvolgt:

```c
/*
 De uitkomst die wordt geretourneerd door de functie millis() wordt geprint
met Serial.print
*/
void loop(){
  Serial.print(“Wink has been running for “);
  Serial.print(millis());   //print de uitkomst van de millis() functie
  Serial.print(“ milliseconds.”);
  Serial.println();         //print een nieuwe regel
  delay(1000);              //wacht 1 seconde
} //end of loop()
```

Het interessante gedeelte van dit voorbeeld is de tweede regel, `Serial.print(millis());` Laten we eens kijken naar deze code en uitleggen wat hier gebeurt. In het vorige voorbeeld, hebben we een variabele gebruikt om de uitkomst van de functie `millis()` aan toe te kennen, om deze vervolgens te printen via de `Serial.print` functie.

In dit voorbeeld hebben we de `millis()` functie direct in de `Serial.print` functie gezet, in plaats van een variabele. Het is een gewone `Serial.print` functie, maar binnen de haakjes aan het einde van de functie staat in plaats van een string tussen aanhalingstekens of een naam van een variabele, nu een andere functie.

Omdat we de uitkomst van de `millis()` functie direct gebruiken, hoeven we geen variabele te gebruiken om deze waarde in op te slaan. Hierdoor hebben we 1 stap minder nodig, en het bespaart ook wat geheugen wat voor de variabele zou worden gereserveerd. Dat maakt voor nu niet heel veel uit, maar voor de complexere programma's zou het besparen van geheugen nog wel eens kunnen helpen.

##Samenvatting##
Nu weet je dus hoe je de Wink interessante zaken tegen je kan laten vertellen. Dit is echt super handig in de vervolglessen. Neem wat tijd om zelf met de `Serial.print()` functies te spelen.

Er zijn dikke boeken geschreven over hoe je moet omgaan met de verschillende methodes in de taal C om de seriele functies te gebruiken. Als je geinteresseerd bent, kan je eens een kijkje nemen op de officiele pagina van de Arduino website voor serieele functies. Wij hebben alleen 2 van de 21 methodes behandeld om Serial te gebruiken. We zullen er later dieper op in gaan.

De officiele Arduino Serial pagina: https://www.arduino.cc/en/Reference/Serial

> Learn to Code ~ Ch07 Rev01.1 ~ Plum Geek
