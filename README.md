# Quax Game
A Java implementation of Quax, a Hex-style board game. Features a responsive JavaFX user interface, a speedy custom heuristic bot opponent and a fully replayable gameplay loop. \
\
Created in collaboration with Dominick Odujebe and Alex Zuzuleac.

![A Quax game in progress](/assets/Quax-Game.png)
***A Quax game in progress***

## Game Rules
1. Quax takes place on an 11x11 board between two players, white and black. Your colour is randomly selected at the start of each round.
2. There are two tile types - octagons and rhombuses. Any unoccupied octagon can be taken freely on your turn. An unoccupied rhombus can only be taken if it forms a diagonal connection between two of your own octagons.
3. You win when you form an uninterrupted line from one side of the board to another. Black must form a line from the top to the bottom of the board. White must form a line from the left to the right of the board.
4. Vertically or horizontally connected octagons are considered uninterrupted. Diagonally connected octagons are only considered uninterrupted if the rhombus between them has also been taken.
5. Black moves first. After black's first move, white can activate the pie rule to swap colours and claim black's move.

## Bot Opponent
The player plays against a custom-designed bot opponent. This opponent was designed to run quickly and assess the board's state to make the best possible move.
This was achieved using a flow-grid style design, where each unoccupied tile is given a priority value, and the bot makes its move on the highest priority tile. 
This design came with two benefits - it was easy to display/debug the bot's intentions by making the weight values visible to the player, and it meant we could focus our efforts
on programming a solid priority system without the overhead of the bot.
\
\
We landed on a set of specific bot strategies to determine priority values. The strategies are as follows:
- **Opening Strategy:** the bot picks a random central tile as an opening move
- **Winning Strategy:** the bot picks a tile that will directly lead to victory
- **Blocking Strategy:** the bot blocks a tile that will directly lead the opponent to victory
- **Defensive Strategy:** the bot picks a tile that blocks the opponent's strongest line
- **Pathfinding Strategy:** the bot picks a tile to strengthen its own line
- **Pressure Strategy:** the bot picks a tile near the opponent's line to reduce their options
- **Rhombus Strategy:** the bot picks a rhombus that blocks the formation of an enemy line

...and many more minor strategies.

![The bot in action showing its strategy](/assets/Bot-Strategy.png)
***The bot in action showing its strategies***


## Architecture
The project is set up to loosely follow the Model-View-Controller architecture. Our classes show a clear separation of concern.
- **QuaxGame:** acts as the model, with the current state being stored in a `QuaxBoard` object. All game requests go through `QuaxGame`, which validates the request based on the current state of the board.
- **BoardFX:** acts as the view. The user interface is created and updated through this object.
- **BotController:** acts as the controller. The bot logic is stored here, using the `QuaxBoard` state to make heuristic decisions.

## How to Run
### Via IntelliJ
1. Set up a new project
2. Copy everything from the 'src' folder into the 'src' folder of the project
3. Under 'Project Structure', set the SDK to ms-21
4. In the 'Modules' tab, go to 'Dependencies' and add every .jar file from the javafx lib
   folder
5. In the 'Libraries' tab, add the javafx lib folder as a new entry
6. Create a new run configuration, and add the following to the VM options:
   --module-path path/to/javafx/lib --add-modules=javafx.controls
7. Run the main method in the Main.java file
### Via JAR File
1. Install the Quax.jar file and a Java Runtime Environment
2. Ensure you have the JavaFx SDK 21 package in the same directory as the .JAR file
3. Run the following command: java --module-path javafx-sdk-21.0.10/lib --add-modules javafx.controls,javafx.fxml -jar Quax.jar
