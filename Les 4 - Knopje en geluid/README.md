#Les 4 - Knopje en geluid#

##Voer een actie uit nadat het knopje op de Wink is ingedrukt##
Tot nu toe zijn de voorbeelden altijd in een eeuwige loop gezet, het programma wordt continu opnieuw uitgevoerd. Soms wil je dat je programma wacht tot iets gebeurt, bijvoorbeeld een druk op het knopje van de Wink. Je kan je programma laten stoppen en wachten op een druk op het knopje met de `waitForButton()` functie.

``` c
/*
 Wacht totdat het knopje van de Wink wordt ingedrukt. Daarna zal het programma
 direct verder gaan met het aanzetten van de ogen in de kleur rood. Na 1 seconde 
 worden de ogen uitgezet, en zal het programma opnieuw wachten totdat het knopje wordt
 ingedrukt.
*/
void loop() {
  waitForButton();	// Wacht totdat het knopje wordt ingedrukt
  eyesRed(100);		// Kleur de ogen rood
  delay(1000);		// Wacht 1 seconde
  eyesOff();		// Zet de ogen uit
}
```

Door te wachten op het indrukken van het knopje kan je een gebeurtenis (event) laten plaatsvinden wanneer je maar wil. Je zou bijvoorbeeld de ogen kunnen laten knipperen. Als je in dit voorbeeld de knop ingedrukt houdt dan lijkt het alsof de ogen aan blijven. In werkelijkheid worden de ogen in een zeer korte periode uitgezet aan het einde van het programma. Maar aan het einde van het programma wordt weer begonnen met het begin van de `loop()`, hier staat de `waitForButton()` functie. Als je nog steeds de knop ingerukt houdt dan worden de lichten weer voor 1 seconde aangezet.

Laten we de lichten uitzetten zodra je de knop loslaat. Dit kunnen we doen door de pauzetijd veel korter te maken. Laten we eens `delay(25)` proberen.

``` c
/*
 Wacht totdat het knopje wordt ingedrukt. Het programma zal doorgaan totdat
 de knop wordt ingedrukt, waarna de ogen oplichten, vervolgens weer uitgaan totdat
 de knop weer wordt ingedrukt.
*/
 void loop() { 
   waitForButton();	// Wacht totdat het knopje wordt ingedrukt
   eyesRed(100); 	// Kleur de ogen rood
   delay(25); 		// Wacht voor 25 milliseconden
   eyesOff();		// Zet de ogen uit
```

Je hebt gezien dat dit programma snel reageert op wanneer je het knopje loslaat. Het eerste programma kan je gebruiken als je de ogen lang aan wilt houden na een druk op de knop, het tweede programma zal de ogen alleen aanzetten als je de knop ingedrukt houdt. Zodra je de lessen van niveau 2 bereikt leer je ook `if` (als) en `else` (dan) te gebruiken om hier beter mee om te gaan.


##Geluid toevoegen##
Laten we eens uitzoeken hoe we de Wink een geluid kunnen laten maken. De functies werken als volgt.

``` c
beep(200);	// Maak een geluid voor 200 milliseconden
beepOn();	// Zet het geluid aan en laat het aan
beepOff();	// Zet het geluid weer uit
```

Je zal meteen opmerken dat het geluid van de Wink best hard is. Het is een goed idee om de `beep()` functie te gebruiken omdat dit zowel het geluid aanzet als ook uitzet na een bepaalde periode. Je kan ook de `beepOn()` functie gebruiken om het geluid continu aan te zetten. Vergeet hierbij niet om het geluid ook weer uit te zetten met `beepOff()`.

Merk op dat de `beep()` functie de tijd van het geluid beperkt tussen 10 en 1000 milliseconden. Als je een getal gebruikt onder de 10, zal het geluid voor 10 milliseconden te horen zijn. Bij een getal hoger dan 1000 wordt het geluid maar maximaal 1000 milliseconden (1 seconde) aangezet. Dit is om te voorkomen dat je per ongeluk een heel hoog getal invoert en heel lang moet wachten voordat het geluid uit gaat.

BELANGRIJKE WAARSCHUWING!!! Het onderdeel dat het geluid maakt staat of aan of uit. Als je heel snel het geluid aan en uitzet zal je verschillende toonhoogtes horen. Dit zal hoogstwaarschijnlijk het onderdeel beschadigen. De `beep()` functie heeft ingebouwde maatregelen die beschadigingen voorkomen, dus gebruik `beep()` zo veel als mogelijk. GA NIET zelf het geluid aansturen met de Arduino `tone()` functie of andere mogelijkheden omdat dit waarschijnlijk het onderdeel kan beschadigen. Vermijd ook het aanroepen van `beepOn()` en `beepOff()` in korte periodes achter elkaar omdat dit hetzelfde probleem kan opleveren. Het is aan te raden om het geluid niet korter dan 10 milliseconden te laten duren, en minstens 50 milliseconden te wachten voordat je het geluid weer aanzet. De `beep()` functie zorgt automatisch dat aan deze voorwaarden wordt voldaan.

Laten we eens geluid toevoegen aan ons eerdere voorbeeld van het gebruik van het knopje.

``` c
/*
 beep() werkt hetzelfde als de delay() functie, maar zal tijdens deze periode
 een geluidje laten horen.
*/
 void loop() {
   waitForButton(); 
   eyesRed(100); 
   beep(25); 
   eyesOff();
}
```

##Experimenteer zelf ook eens##
Nu weet je hoe je de Wink zijn ogen, motoren en geluid moet aansturen en hoe je moet wachten op het drukken op de knop. Makkelijk toch? Nu is het een goed moment om een zelf leuke experimenten uit te voeren. In de volgende les zullen we al deze ideeën samenvoegen om iets leuks te doen!

