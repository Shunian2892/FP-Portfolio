# Portfolio
## Kim Veldhoen 
## Studentnummer: 2154630
## Jaar 1, klas B

# Inhoud:
1. [`Wekelijkse reflectie`](#wekelijkse-reflectie)
2. [`Vakinhoudelijke reflectie`](#vakinhoudelijke-reflectie)
3. [`JSON applicaties`](#json-applicaties)


# Wekelijkse reflectie 
## Week 2:
In deze week zijn we gestart met de opzet van de agenda GUI. Voor het maken van het klassendiagram hebben we, in de eerste week, een opzet gemaakt van hou de GUI eruit zou moeten zien en welke functies deze nodig had.
![Ontwerp agenda GUI](handleiding.png)

Hierbij hebben we verschillende klassen opgezet waarin de agenda GUI zelf, de datastore, de shows, artiesten en podiums aangemaakt kunnen worden.
![Klassendiagram FestivalPlanner](FestivalAgenda.jpg)

Ieder persoon van de projectgroep kreeg een klasse aangewezen om deze week te maken. Remco en ik zijn beide begonnen aan de agenda GUI klasse zelf.
In deze week heb ik een aantal veranderingen gemaakt aan de GUI klas. Dit in overleg met de rest van de project groep, omdat bepaalde aspecten die in week 1 in de GUI klas zijn geïmplementeerd niet aan onze eisen voldoen. 

## Week 3:
In deze week zijn we verder gaan werken aan de functionaliteiten van de agenda GUI.
Ik heb in de GUI klas een aantal aanpassingen gedaan aan hoe de knoppen van de verschillende stages (new, edit, delete) shows aanmaken, bewerken, en opslaan.
Dit in combinatie met gebruik van ObjectIO wat Florian heeft geïmplementeerd. Hiermee kunnen we nieuwe shows aanmaken en opslaan, shows ophalen en deze bewerken, shows individueel verwijderen, of alle shows tegelijk verwijderen.
![GUI](agendaGUI.png)

## Week 4:
In deze week zijn we begonnen met het inladen van JSON-files in InteliJ. Hiermee kunnen we een aparte file maken wat als "map" achtergrond gebruikt kan worden.
Hierop plaatsen we de vier verschillende podiums, toiletten, eettentjes en rustplaatsen waar de karakters op kunnen rondlopen.
Verder hebben we tijdens het senior gesprek met Johan besproken dat we de individuele portfolio's in de git-repository van het project toevoegen. Hierdoor is de toegang tot onze portfolio's voor onze eigen senior, Joep, makkelijker.

## Week 5:
In deze week zijn we begonnen met de opzet van de festival simulatormodule. Hiervoor hebben we een globaal overzicht gemaakt van welke klassen er nodig zullen zijn.
Op basis van de globale opzet kunnen we een klassendiagram maken van welke klassen er nodig zijn voor de simulator zelf.
![Globale opzet](simulatiemodule.png)
Wanneer de klasse voor NPC en gasten af is, kunnen de karakters op de map worden ingeladen. In eerste instantie testen we of deze karakters over de map heen kunnen lopen en of de collisiondetection goed werkt.
In week 6 kunnen we met A* pathfinding ervoor zorgen dat deze karakters tussen de verschillende podiums, toiletten en eettentjes kunnen lopen.
Zo kan het gedrag van gasten op een festival gesimuleerd worden en kunnen de knelpunten van het festival terrein in kaart worden gebracht.

## Week 6:
//TODO uitbreiden
In deze week zijn we begonnen met het implementeren van het pathfinding algortitme. Na het opstart college hebben we besloten om Breath First Search (BFS) toe te passen in plaats van A^. Dit omdat uit het opstart college naar voren kwam dat A* lastiger wordt voor een simulatie met veel NPC's.

## Week 7:
//TODO uitbreiden
In deze week zijn Dogukan en ik verder gegaan met het implementeren van BFS. Dit kwam omdat wij vorige week compleet vast liepen op bepaalde punten.

# Vakinhoudelijke reflectie 
## VR Week 2:
In week 1 hebben we een opzet gemaakt voor de GUI van de agenda. Hier hadden we een tabel in verwerkt, maar dit bleek uiteindelijk niet te voldoen aan onze eisen omdat we hiermee geen gebruik konden maken van java2D.
Hierdoor heb ik in week 2 de hele GUI klas omgebouwd waardoor deze wel gebruik kon maken van java2D.
In de GUI klas hebben we ook gebruik gemaakt van de popup klas van Java zelf. Deze popups heb ik, na het ombouwen van de GUI klas, achterwegen gelaten omdat deze niet het effect gaven wat we eigenlijk hadden verwacht.
Ik heb in plaats van de popups nieuwe klassen aangemaakt voor elke actie die we willen gebruiken: het toevoegen van een nieuwe show, het bewerken van een bestaande show, en het verwijderen van een bestaande show.
Wanneer er nu op een bepaalde knop wordt gedrukt (new, edit, delete), zal er een nieuwe instantie van de desbetreffende klas worden aangemaakt.
Hierin kan doormiddel van tekstvelden informatie worden ingevoerd die een (nieuwe) show zullen aanmeken.
Deze show wordt voor nu opgeslagen in een ArrayList met shows die vanuit de datastore klas kan worden opgeslagen en opgevraagd.

## VR Week 3:
Deze week heb ik samen met Florian er voor gezorgd dat de informatie van de tekstvelden worden opgeslagen door gebruik te maken van ObjectIO.
Wanneer nu, tijdens het aanmaken van een nieuwe show, op de 'done' knop gedrukt is zal er eerst worden gekeken of er een artiestennaam is ingevuld in het artiesten tekstvak.
Als dit niet het geval is, dan kan er niet op 'done' gedrukt worden. Dit om er voor te zorgen dat er geen shows worden opgeslagen zonder artiest.
Wanneer er wel een artiesten naam is ingevuld, maar de rest van de tekstvakken zijn leeg dan zullen deze een standaard waarde van '0' meekrijgen. Deze zijn bij het bewerken van de show, editStage, aan te passen.

    doneButton.setOnAction(e -> {
        if(!artistField.getText().isEmpty()){
            newShow.setShow(artistField.getText());
            } else {
                artistField.setText("please type in a name");
            }
            if(!beginTimeField.getText().isEmpty()
              && Integer.parseInt(beginTimeField.getText()) != Integer.parseInt(endTimeField.getText())
              && Integer.parseInt(beginTimeField.getText()) < Integer.parseInt(endTimeField.getText())){
                newShow.setStartTime(Integer.parseInt(beginTimeField.getText()));
            } else {
                newShow.setStartTime(0);
            }
            if(!endTimeField.getText().isEmpty()){
                newShow.setEndTime(Integer.parseInt(endTimeField.getText()));
            } else {
                newShow.setEndTime(0);
            }
            if(!popularityField.getText().isEmpty()){
                newShow.setPopularity(Integer.parseInt(popularityField.getText()));
            } else {
                newShow.setPopularity(0);
            }
            if(!stageField.getText().isEmpty()){
                newShow.setStage(Integer.parseInt(stageField.getText()));
            } else {
                newShow.setStage(0);
            }
            
            this.showList.add(newShow);
            newStage.close();
                 
            if (!this.showList.isEmpty()){
                serializer.Write(this.showList);
            }
    });

Bij het verwijderen van een show zal eerst worden gevraagd of de gebruiker zeker weet of hij/zij deze show wilt verwijderen. Nadat op 'yes' is gedrukt, zal de desbetreffende show uit de lijst worden gehaald.
     
    yesButton.setOnAction(e -> {
        if (!deserializer.Read().isEmpty()){
            showList = deserializer.Read();
        }
        showList.remove(index);
        serializer.Write(showList);
        delStage.close();
    }); 
    
## VR Week 4:
//TODO uitbreiden
Deze week heb ik mij verdiept in het inladen en uitlezen van JSON-files in Java en IntelliJ. 

## VR Week 5:
//TODO uitbreiden
Deze week heb ik mij verdiept in A* pathfinding. Wij waren van plan A* te gebruiken omdat merendeel van de project groep hier al van had gehoord. Bij het onderzoek doen naar A* heb ik in pseudocode een paar klassen gemaakt met attributen waarvan ik dacht deze nodig te hebben.


## VR Week 6:
Deze week hebben mijn projectgroep en ik er voor gekozen om, in plaats van het A* pathfinding te gebruiken, het Dijkstra-pathfinding te implementeren. Dit omdat dit algoritme tijdens het opstart college kort is uitgelegd en omdat Johan zei dat het Breath Frist Search (BFS) makkelijker toe te passen is op een simulatie met veel NPC's (zoals in ons geval).
Samen met de projectgroep hebben we op de map een collisionLayer aangemaakt waarin de grenzen van de map zijn aangegeven.
![CollisionMap](tileMap.png)
In de afbeelding staan alle rood getekende vierkanten voor een collisionTile. Dit betekend dat de NPC's niet op deze tile kunnen lopen. Als eerste hebben Dogukan en ik ons verdiept in het BFS algortime.
Vervolgens hebben we met hulp van Timo en Nathalie de collisionLayer uit de JSON file kunnen halen en hebben wij de data hiervan kunnen opslaan in een 2D Array met de hoogte en breedte van de map zelf.
 
    for (int y = 0; y < height; y++){
        for (int x = 0; x < width; x++) {
            int gid = map[y][x];
            this.tileMap[y][x] = new Tile(new Point2D.Double(x,y), false, false, false);
                                     
            if (gid == 0) {
                graphics.setColor(Color.GREEN);
                graphics.draw(new Rectangle2D.Double(x * tileWidth, y * tileHeight, 32, 32));
                Font font = new Font("Arial", Font.PLAIN, 5);
                graphics.setFont(font);
                graphics.drawString("(" + (int) gridPos.getX()/32 + " , " + (int) gridPos.getY()/32 + ")", (x * tileWidth), (y * tileHeight));                        
            } else if (gid == 975) {
                graphics.setColor(Color.RED);
                graphics.fill(new Rectangle2D.Double(x * tileWidth, y * tileHeight, 32, 32));
                this.tileMap[y][x].setWall(true);
                                    
            }
        }
    }
In bovenstaande code hebben we een geneste for-loop. Hiermee wordt er door elke rij en kolom heen gegaan en wordt gecheckt of de gid op die plaats 0 of 975 is (met 975 als collisonTile).
Als de gid overeen komt met 975, dan zetten we de voor die tile de boolean setWall op true. Voor visuele validatie, wat betreft het corrcet uitlezen van de map, hebben wij voor de zekerheid deze tiles met een rood blokje aangegeven.
Nadat we deze grid hadden gemaakt, kwamen we compleet vast te zitten. Hierom hebben wij hulp gevraagd bij medestudenten, wij hebben deze week dezelfde vragen aan Joep (onze senior) gevraagd, maar hierop kregen wij geen antwoord.


## VR Week 7:
In deze week zijn Dogukan en ik verder gegaan met het uitzoeken van de BFS. We hebben ieder voor zich geprobeerd het BFS algortime te implementeren om deze vervolgens samen na te gaan om zo tot één geheel te komen.
Ik heb mij voornamelijk bezig gehouden met het uitprinten van een adjacency map van de tileMap. Voor het implementeren van het BFS algoritme heb ik de klasse Tile aangemaakt,
In de Tile klas wordt een int x en int y meegegeven als start punt. Verder heeft deze klassen getters en setters voor de x, y en de boolean isWall.
Met het aanmaken van een nieuwe Tile heb ik geprobeerd om de vier omliggende cellen (links, rechts, boven, onder) te kunnen detecteren. Door de twee geneste for-loops kon ik een x en y waarde opvragen, om vervolgens hiermee met vier if-statements om de desbetreffende cel heen te kijken.
    
    Tile start  = new Tile(int x, int y);
    Queue<Tile> open = new LinkedList<Tile>();
    ArrayList<Tile> closed = new ArrayList<Tile>();
    Tile current = start;
    open.add(start);
    
    while(!open.isEmpty()){
        closed.add(open.poll());
        //Check de omliggende tiles
        if (i > 0 && array[i-1][j] == 0 && !closed.contains(new Tile(i-1, j))) //Voor cel boven
            open.add(new Tile(j, i-1);
        if (j > 0 && array[i][j-1] == 0 && !closed.contains(new Tile(j-1, i))) //Voor cel links
            open.add(new Tile(j-1, i);
        if (j + 1 < array[1].length && array[i][j+1] == 0 && !closed.contains(new Tile() //Voor cel rechts
            open.add(new Tile(j+1, i);
        if (i + 1 < array.length && array[i+1][j] == 0) //Voor cel onder
            open.add(new Tile(j, i+1)
    }
    
Hierbij heb ik geprobeerd om als eerste te kijken of de cel links/rechts/boven/onder uberhaüpt in de grid zit of niet. Wanneer dit niet het geval was wordt er een nieuwe tile van die positie aangemaakt ne in de Queue open gezet.
Dit bleek niet geweldig te werken. Vervolgens hebben Dogukan en ik onze codes samen doorgekeken en hebben we een paar aanpassingen gedaan aan de Tile klasse en het doorlopen van de 2D Array. Helaas zijn we er niet zelf uitgekomen, ook niet met het senior gesprek met Joep.
Daarom hebben we weer de hulp van onze medestudent gevraagd. Op basis van zijn uitleg zijn hebben Dogukan en ik aanpassingen gedaan in de klassen: Tile, Map, BreathFirstSearch en de main.
De Tile klasse vraagt nu om een Point2D, boolean isWall, boolean isDestination, boolean isVisited.
De BreathFirstSearch klasse bevat het BFS algoritme en het checken van de omliggende cellen, in plaats van in de main. Het zetten van een tileMap op basis van de 2D Array die we aanmaken in de map klasse.
    
    if(inGrid(pos.getX(), pos.getY())){
        this.queue = new LinkedList<Tile>();
        grid[(int)pos.getY()][(int)pos.getX()].setDestination(true);
        grid[(int)pos.getY()][(int)pos.getX()].addRoute("route 1", new Point2D.Double(0,0));
        grid[(int)pos.getY()][(int)pos.getX()].setVisited(true);
    }
      
De code om de buren te controleren is nu veranderd in:
        
    //Dit dan voor elke richting dan voor alleen de cel onder
    if(inGrid(pos.getX(), pos.getY() + 1)){
        final Tile checkTile = this.grid[(int)pos.getY() + 1][(int)pos.getX()];
        if(!checkTile.isWall() && !checkTile.isVisited() && !checkTile.isDestination()){
            checkTile.addRoute(route, new Point2D.Double(0,-1));
            checkTile.setVisited(true);
            queue.add(checkTile);
        }
    }

Met een HashMap kunnen we karakters meegeven aan verschillende routes (voor verschillende targets):

    //Dit dan voor elke richting
    if (bfs.getTileMap()[y][x].isWall()) {
        System.out.print("W ");
    } else if (bfs.getTileMap()[y][x].getRoute().get("route 1") == null) {
        System.out.print("o ");
    } else if (bfs.getTileMap()[y][x].getRoute().get("route 1").getX() == 1) {
        System.out.print("> ");
    } else if (bfs.getTileMap()[y][x].getRoute().get("route 1").getX() == -1) {
        System.out.print("< ");
    
Zodat we uiteindelijk als resultaat krijgen:
![PathFinding](pathfindingMap.png)
Met "o" wanneer de Tile onbereikbaar is, "W" wanneer de Tile de boolean isWall = true bevat, en pijltjes voor de richting wanneer de Tile naar een andere Tile moet lopen


# JSON applicaties
JSON staat voor JavaScript Object Notation en is een gemakkelijke en lichtgewicht data-uitwisselings format.
JSON maakt alleen gebruik van tekst, waardoor dit gemakkelijk van en naar een server verzonden kan worden.
## Websites
### HTML
Json kan heel gemakkelijk worden omgezet in JavaScript wat omgezet kan worden in HTML voor websites

### PHP
PHP objecten kunnen geconverteerd worden in JSON waarmee bijvoorbeeld een website gemaakt kan worden

## Web servers

## Smartwatch apps

Al deze applicaties maken gebruik van JavaScript