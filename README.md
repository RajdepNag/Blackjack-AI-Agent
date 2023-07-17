# Blackjack AI Agent


The game more or less follows the standard Blackjack rules. Read the **Blackjack Rules** section below and game engine code to see minor simplification.

The Hit and Stand buttons are for playing the game manually. The MC, TD, and QL buttons start/pause the corresponding learning processes. 

I've implemented the following algorithms. In all of them, the discount factor is 0.95 as given in Line 8 of `ai.py`. When the player wins, give reward +1, and when loses, the reward is -1. (See **Blackjack Rules** below for details).

### Monte Carlo Policy Evaluation 

Evaluate the policy "Hit (ask for a new card) if sum of cards is below 14, and Stand (switch to dealer) otherwise" using the Monte Carlo method. Namely, learn the values for each state under the policy. 

### Temporal-Difference Policy Evaluation

Evaluate the policy "Hit (ask for a new card) if sum of cards is below 14, and Stand (switch to dealer) otherwise" using the Temporal-Difference method. 

### Q-Learning

Implement the Q-learning algorithm. Use epsilon=0.4 in the epsilon-strategy in your final submission, but you are encouraged to check the behavior difference for various choices of epsilon. After learning, AutoPlay will follow the Q-learning values to make decisions. 

## Rules of Blackjack

**Goal of the player**: Get a bigger sum than the dealer’s sum, without going over 21 (bust). 

### Cards’ values:
- Ace counts as either 1 or 11 based on need. 
- Jack, Queen and King counts as 10. 
- Other cards count as their numerical values.

### Terms:
- Bust: the sum of cards is greater than 21.

### Game’s procedure: 
1. The player and dealer are both given two cards, with one of the dealer’s card revealed to the player. 
2. The player can keep asking for new cards before going bust. 
3. When the player stands, the dealer takes over until termination. 

### Player’s actions: 
1. Hit: player takes a card from card deck
2. Stand: player stops taking cards, and dealer plays with its policy (see below)

### Dealer’s policy:
1. Dealer starts taking cards until the sum get greater than or equal to 17, or greater than or equal to the player’s sum
2. If dealer has A’s in its hand, then the A only counts as 1 when otherwise the dealer bursts. See below for examples
    1. If dealer has {“Ace”, 6}. then the ace counts as 11 and dealer stops taking cards since the sum equals 17.
    2. If dealer has {8, 6, “Ace”}, then the ace counts as 1 (since counting A as 11 would make the dealer burst), and dealer keeps taking cards since the sum equals 15.

### Termination conditions:
1. Player stands
2. Player gets over 21 (bust)
3. Player gets exactly 21

### Game results:
1. If player and dealer has the same sum values, the player LOSES
2. If player busts, player LOSES
3. If dealer busts, player WINS
4. If neither busts, the player WINS if player has a sum bigger than dealer. That means if player and dealer has the same sum value, player LOSES

### Custom rules:
For simplifying the simulation and modeling, the game engine uses rules slightly different than the normal ones. Do not be disturbed by them; your algorithms work regardless of the rules. 

1. Cards are drawn with replacement, so assume that you are playing with infinitely many decks of cards and the drawn cards do not affect the probability of the next cards. 
2. When user has 5 cards without busting, it is NOT considered as WIN in our game engine. 
3. We don’t have DRAW state. If after stand, user and dealer has the same sum values, the player LOSEs.
4. If player gets 21 at the first hand, player WINs if dealer doesn’t have 21; otherwise player LOSEs. 
5. If player gets 21 after a hit, the player automatically stands, meaning dealer starts to play, and check results afterwards.
6. We don’t differentiate between Blackjack (A + 10) and 21, meaning if user and player both has a sum of 21 when the scores are checked, the player is considered as LOSE.
