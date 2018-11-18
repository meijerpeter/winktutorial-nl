#Gebruik van de IR afstandsbediening#
##Mogelijkheid tot het gebruik van infrarood##
Je Wink kan zijn uitgerust met een infrarood ("IR") ontvanger. Dit is niet een standaard optie, maar wordt alleen uitgevoerd op verzoek. Als je Wink de infrarood ontvanger heeft, zie je een zwart blokje achter de rechtermotor. Dit onderdeel is gesoldeerd in de 3 gaten van de printplaat. Neem contact met plumgeek.com op als je de IR ontvanger wil toevoegen aan een bestaande Wink robot (het onderdeel is eenvoudig zelf te solderen met een klein soldeerstation).

De Wink kan infrarood communicatie ontvangen van een afstandsbediening. Het is ook mogelijk om IR signalen te ontvangen van andere Wink of Ringo robots.

De optionele Plum Geek afstandsbediening is zo gemaakt dat het verschillende berichten stuurt van 4 bytes wanneer een knopje wordt ingedrukt. Om deze reden, nemen we aan dat de Wink berichten verstuurd of ontvangt ter grootte van 4 bytes. Je kan eventueel zelf de lengte van de bytes aanpassen mocht je dit willen.

LET OP: De IR functies van deze les zijn aanwezig in de Wink_Base_Sketch_Rev01_3 of een latere versie.

##Het ontvangen van IR berichten##
De Wink moet worden klaargemaakt om infrarood bericthten te ontvangen van een IR afstandsbediening of een andere robot. De volgende stappen zijn in het algemeen nodig om de Wink klaar te maken:

1. Wink begint met het ontvangen van berichten met `RxIRRestart()`.
1. Je code moet regelmatig checken of er nieuwe IR berichten zijn ontvangen met `IsIRDone()`.
1. Je code moet bepalen wat voor soort bericht is ontvangen is hier op reageren.

```c
/*
 De volgende code zorgt ervoor dat in de achtergrond continu wordt bekeken of een IR bericht van 4 bytes is ontvangen.
*/
RxIRRestart(4);		//zet de IR ontvanger aan, wacht op 4 bytes
```

De IR ontvanger 