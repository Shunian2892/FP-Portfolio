# Portfolio
## Kim Veldhoen 2154630

#Weeklijkse reflectie 
##Week 2:
In deze week heb ik een aantal veranderingen gemaakt aan de GUI klas. Dit in overleg met de rest van de project groep, omdat bepaalde aspecten die in week 1 in de GUI klas zijn geïmplementeerd niet aan onze eisen voldoen. 
##Week3:
In deze week heb ik een aantal aanpassingen gedaan aan hoe de knoppen van de verschillende stages (new, edit, delete) shows baanmaken, bewerken, en opslaan.
Dit in combinatie met gebruik van ObjectIO wat Florian heeft geïmplementeerd.


#Vakinhoudelijke reflectie 
##Week 2:
In week 1 hebben we een opzet gemaakt voor de GUI van de agenda. Hier hadden we een tabel in verwerkt, maar dit bleek uiteindelijk niet te voldoen aan onze eisen omdat we hiermee geen gebruik konden maken van java2D.
Hierdoor heb ik in week 2 de hele GUI klas omgebouwd waardoor deze wel gebruik kon maken van java2D.
In de GUI klas hebben we ook gebruik gemaakt van de popup klas van Java zelf. Deze popups heb ik, na het ombouwen van de GUI klas, achterwegen gelaten omdat deze niet het effect gaven wat we eigenlijk hadden verwacht.
Ik heb in plaats van de popups nieuwe klassen aangemaakt voor elke actie die we willen gebruiken: het toevoegen van een nieuwe show, het bewerken van een bestaande show, en het verwijderen van een bestaande show.
Wanneer er nu op een bepaalde knop wordt gedrukt (new, edit, delete), zal er een nieuwe instantie van de desbetreffende klas worden aangemaakt.
Hierin kan doormiddel van tekstvelden informatie worden ingevoerd die een (nieuwe) show zullen aanmeken.
Deze show wordt voor nu opgeslagen in een ArrayList met shows die vanuit de datastore klas kan worden opgeslagen en opgevraagd.

##Week 3:
Deze week heb ik samen met Florian ervoor gezorgd dat de informatie van de tekstvelden worden opgeslagen door gebruik te maken van ObjectIO.
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

Bij het verwijderen van een show zal er eerst worden gevraagd of de gebruiker zeker weet of hij/zij deze show wilt verwijderen. Nadat er op 'yes' is gedrukt, zal de desbetreffende show uit de lijst worden gehaald.
     
    yesButton.setOnAction(e -> {
        if (!deserializer.Read().isEmpty()){
            showList = deserializer.Read();
        }
        showList.remove(index);
        serializer.Write(showList);
        delStage.close();
    }); 
   