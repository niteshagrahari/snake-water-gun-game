# snake-water-gun-game
 
 the SNAKE-WATER-GUN game rule before we move on to discussing the game client/server application. This classic fun game is commonly played by two people (although can be played by more). Later, you'll extend the game by adding feature support for more than two users
 
 snake will drink water and win by water
 snake will dead by gun 
 gun will not work in water 
 gun will beat snake
 water will beat gun
 water will be drink by snake so it loose.
 
 
 def game_logic(you, opponent):
    winner = ""
    snake = "snake"
    water = "water"
    gun = "gun"
    player0 = "you"
    player1 = "opponent"

    if you == opponent:
        winner = "draw"
    elif you == snake:
        if opponent == water:
            winner = player0
        else:
            winner = player1
    elif you == gun:
        if opponent == snake:
            winner = player0
        else:
            winner = player1
    elif you == water:
        if opponent == gun:
            winner = player0
        else:
            winner = player1
    return winner


 The function takes in two arguments and using if/else statements decides if there’s a win, loss or even a draw. We will covert this classic game to a network game so you can play with your friends and family online. The game will have 5 rounds. We'll show the winner for each round and the final results at the last round. Then, the game session starts all over.
 
 
 ************************************************************************************************************************************
 client
 
 The game client application allows a player to connect to the game server and play against another connected player (i.e. the opponent).
 the Game client window for two connected clients (assuming the server is already running). When a player connects to the server, the server responds with a welcome message. Here, the welcome message depends on the number of connected players. After both players are connected. The game client receives the opponent's name and displays this information on the game window. Also, the "Game log" section is display on the game client window
 
 ![Screenshot (4)](https://user-images.githubusercontent.com/76960456/198746039-eb8c9ecc-60ce-4066-96d5-d94af6a9f076.png)
Now that both clients are connected and we know who the opponent is. The game session can start. But how do we know when to start the game session? One possibility is for the server to send a "start" signal to the clients. The game session can start when the clients receive the start signal.

We use a count-down timer and enabling/disabling of the "choice buttons"( i.e. snake water gun buttons at the bottom of the game window) to control when user can play. Initially the choice buttons are disabled and enabled when the counter decrements to 0. When this happens, the players make their choices. The choice buttons get disabled when a player clicks on them. In this way, we ensure our players do not make more than one choice for each game round. The selected choice is forwarded to the server and the server in turn forwards the opponent’s choice to the client (e.g. player 1 choice is forwarded to player 2 and vice versa). This info gets displayed on the game client window . It’s important to note that we do not forward the player choices until we are sure both players have made their choices. So, the server waits until it receives both choices before forwarding the info.

![Screenshot (3)](https://user-images.githubusercontent.com/76960456/198746686-a11b4706-17d7-4a7e-87de-19aa56eae493.png)


The next step is to determine who wins in the current game round. 
Game server will send opponents choice e.g. player 1 choice to player 2 and vice versa (i.e. 2 send function call multiply by 5 rounds)
Game client determines the winner (runs the game logic that compares the two choices and determines if it's a win, loss or draw)
Game client keep track of the game scores for both players .
Game client compute the final score and determines the overall winner at the final round. Hence.
