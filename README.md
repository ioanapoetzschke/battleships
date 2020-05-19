# battleships

Implementierung (kurze Beschreibung):

- es gibt 2 Grids : OwnGrid und PartyGrid (Gegner Grid)
- eine Position in Grid ist durch eine Location representiert
- Die Location beinhaltet : Koordonaten x und y , die Zuordnung zu einem Schiff (ship_placement), Zuordnung zum Grid (OwnGrid oder Gegner Grid) und einen Feld "shot" (es wird dort gemerkt ob die Location schon mal verwendet wurde)

- für OwnGrid werden nur Location gespeichert die einen Schiff enthalten
- für PartyGrid werden nur Location gespeichert die geschossen wurden . (Bei jedem Versuch wird eine Location gespeichert)

Es gibt 2 Routen : /start und /play

Route /start ist für die Initialisierung

Initialisierung:
- Vor dem Starten des Spieles werden die Grids vorbereiten
- Für OwnGrid werden die Locations mit Schiffe erstellt.Die Schiffe werden jedes Mal zufällig plaziert .
- Für PartyGrid wird lediglich nur den Grid erstellt

Route /play: 

Aufbau:
 Request und Response beinhaltet : 
 
 "shot" : die Position (z.B A-6) , 
 "result" : Position und Ergebniss ( z.B : " B-7: HIT CRUISER"  oder "B-7: MISS" ,  
 "message" : zusätzliche Infos wie z.B. wenn der Schiff versunken ist

Wenn Gegner schießt :
  - es wird geschaut, ob es ein Location in OwnGrid gibt (Für OwnGrid werden nur Locations gespeichert, die auch einen Schiff enthalten).
  - Wenn es einen Location gefunden wurde,  dann heisst es dass ein Shiff getroffen wurde . Es wird dann dementsprechend der Response mit "HIT" und Name des Schiffes ausgegeben.
  - Wenn die Location für OwnGrid nicht vorhanden ist, dann heisst es dass es kein Schiff in OwnGrid getroffen wurde.
  
  Wenn selber geschossen wird:
    1. Den Result aus Response wird ausgewertet: wenn ein Schif getroffen wurde, wird der Loaction aus PartyGrid den Schiff zugeornet. Die Anzahl der Schüsse wird hochgezählt (in SchipPlacement). 
    Es wird eine Nachbarn Location ausgewählt , die noch nicht bisher geschossen wurde
    
    2. Wenn der Result negativ ist, dann wird geschaut ob in PartyGrid eine Location gibt, die einen Schiff enthält, welcher noch nicht gesunken ist
    - Wenn ja, dann wird nach eine Nachbarn Location ausgewählt , die noch nicht bisher geschossen wurde (Location -> shot == false)
    - Wenn nicht , dann wird eine zufällige Location generiert, die noch nicht bisher geschossen wurde 
    
    
   
  
  
