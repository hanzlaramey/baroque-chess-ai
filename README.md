# Technical Details

1. Minimax Search​

	As we have two players, one is max, and the other is min. We are at a chess board, and the next move is max’s turn so we have max at the root level (level 0). Max looks at all the possible moves at the next layer —level 1, and simulates all the possible moves for min at level 2.​

	Suppose the computation budget only allows us to arrive at level 2, then we evaluate the chess board for all possible situations at level 2 to get an evaluation score. We “transmit” all these values back to level 1 and have the Min player decide which move they will make. Obviously the Min player will choose the move that minimizes the score. Then level 1 again “transmits” the results back to level 0 and now we have the Max player make the choice. This time the max player will move in a way that maximizes the score.

	# you can find the code for Minimax in terminator_BC_Player.py file

2. Alpha-Beta Pruning

	Alpha-Beta pruning is a technique used on minimax search to avoid exploring unnecessary nodes. We create a pair of extra values [ alpha, beta ] that traverses the search tree as we do adversarial search. Alpha is for the maximizing value, Beta is for the minimizing value. Whenever we arrive at a node where Alpha > Beta, the nodes below the current node won’t be explored.​

	The detailed procedure is as follows:​
	​
	1. Initialize the value pair as [-∞ , +∞]​
	2. traverse the search tree in DFS and update node values at the maximizing node, if the current node value is bigger than alpha, update alpha with the current node value​
	3. at the minimizing node, if the current node value is smaller than beta, update beta with the current node value​
	4. if alpha > beta, don’t need to go down to the child nodes of the current node

	# you can find the code for Minimax in terminator_BC_Player.py file

3. Zobrist Hashing​

	The minimax search process will revisit many states where the chess board deployment is the same but we can arrive at such states through different moves.​

	How does the program knows that is has reached at the same position and don't need to calculate the score again?​

	Zobrist hashing is used to create a hash for the chessboard: it maps the chessboard into a numeric value, an integer, so when we are at a state we hash the position into a numeric value and look up in the hash dictionary.​

	If the same value is stored, we don’t need to evaluate the same position or chessboard state again. In this way, Zobrist Hashing reduces the computation cost by approximately 30% on the chessboard static evaluation.
	# you can find the code for Minimax in terminator_BC_module_zobrist_hashing.py file

4. Heuristics

	- which pieces are remaining?​

	- how many and which pieces are frozen?​

	- how structured are the pawns/pincers?​

	- how well-defended the king is?

# Running the code

`BaroqueGameMaster.py` is used to conducted a game between two bots.  To run this, use the template:

```
python3 agentA agentB time_limit
```

An example would be:

```
python3 BaroqueGameMaster.py terminator_BC_Player terminator_BC_Player 5
```

Running this starts printing a game in the terminal between two bots where each move needs to be made within 5 seconds.
