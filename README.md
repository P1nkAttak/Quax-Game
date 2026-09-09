# Quax Game
A Java implementation of Quax, a Hex-style board game. Features a responsive JavaFX user interface, a speedy custom heuristic bot opponent and a fully replayable gameplay loop.

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
We landed on an set of specific bot strategies to determine priority values. The strategies are as follows:
