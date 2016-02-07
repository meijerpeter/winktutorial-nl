#Les 1 - Arduino Super Basics#

##Hoe ziet het code venster eruit?##
In de wereld van Arduino, het venster waarin je de code schrijft noemen we een *sketch*. We noemen dit ook wel *broncode*. Laten we eens kijken hoe het venster is opgezet:

![Arduino venster] (https://github.com/meijerpeter/meijerpeter/winktutorial-nl/blob/master/img/arduino-venster.png?)

1. Klik op de knop om je code te *verifieren*. Dit zorgt ervoor dat je code wordt gecompileerd en vertelt je of de computer deze code ook begrijpt.

2. Klik op het pijltje om de code te compileren en vervolgens naar het brein van de robot te sturen.

3. Dit zijn tabs. De eerste heeft de naam van je sketch. De andere ondersteunende tabs zijn bedoeld om achtergrond functies te laten zien. Later meer hierover in de geavanceerde lessen.

4. Dit is je code! Het zijn de regels die je robot coole dingen laat doen. Een voorbeeld van code staat hieronder.

5. Dit is het berichten gedeelte. Hierin wordt verteld als je fouten hebt gemaakt in je code en komen ook andere nuttige berichten te voorschijn.

6. Dit opent de "Serial Monitor", dit is een venster waarin je de berichten kan zien van je robot. Dit is handig wanneer je de code wil "debuggen".

'''
/*
Alles in dit gedeelte is commentaar. Commentaar verteld je onder andere wat het programma doet. De computer negeert commentaar, ze zijn er alleen om mensen te helpen om de code te begrijpen.

Gebruik commentaar om jezelf en andere mensen te vertellen wat de code doet. Commentaar achter een regel code kan door een paar "forward slashes" te gebruiken: //
*/

/*
De setup() functie wordt uitgevoerd wanneer de computer start. Het wordt gebruikt om de processor eenmalig te configureren.
*/

void setup() {
	hardwareBegin(); //initialiseren van de computer om met de robot te werken
}

/*
Hier gebeurt het! Alles binnen de loop() functie wordt continu uitgevoerd. De meeste code schrijf je binnen deze functie.
*/
void loop() {
	eyesPurple(100); //kleurt beide ogen paars
	delay(3000); //3 seconden wachten 
	rightOff(); //uitzetten van het rechter oog (geeft een knipoog ("wink" in het Engels))
	delay(250);  //1/4 seconde wachten
}
'''

Leren programmeren - Ch01 Rev01.2 ~ Plum Geek