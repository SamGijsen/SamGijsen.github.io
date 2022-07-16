---
title: Testing!
categories:
- General
feature_text: |
  Feature text
---

## Homebrew your own AlphaZero


Let's have a look at the AlphaZero algorithm, implement it for the game of TicTacToe, and inspect its performance.

&nbsp;

**Issue**: Some problems (such as the game of Go) have very wide decision trees. For a 19x19 board, there are 361 possibilities for the first move. To map all of the first two moves, there are 361\*350=129960 possibilities. First three? Over 46 million. Due to the severity of this increase, previous approaches (such as alpha-beta pruning) become infeasible. 


**Solution**: The AlphaZero (AZ) algorithm doesn’t perform a full tree search, but rather uses a probabilistic search algorithm (Monte-Carlo tree search: MCTS) to explore only those sections of the tree that are deemed most promising. MCTS is combined with a neural network in the following way:

 The current board-state is fed through a network that is trained to indicate promising moves to make. This provides a prior distribution over moves to kickstart the MCTS.

- A hypothetical move is selected and the algorithm interacts with a simulator to update the board state. At this point, one of following possibilities exist:

    * This board state **has** been visited before in this MCTS-session. 
        * In this case we select another action and progress the board state until we reach a state that has not been visited yet.

    * This board state **has not** been visited before in this MCTS-session yet. 
        * If the game **has ended**, we check whether its a win, draw, or loss. This is translated into a value (1, 0, -1 respectively).
        * If the game **hasn’t ended**, we ask a neural net to provide an estimate of how ‘good’ this board state is; it’ll return a value between 1 and -1. Alternatively, the game may be played until the end in simulation to provide a value estimate ("*rollout*").

Whichever it is, we now have a value estimate of how ‘good’ the path we explored is. This is pushed back up the tree and associated with the moves that led us here.

![Monte-Carlo Tree Search [source](https://en.wikipedia.org/wiki/Monte_Carlo_tree_search)](https://upload.wikimedia.org/wikipedia/commons/a/a6/MCTS_Algorithm.png){:class="img-responsive"}


* `mcts.py`: Contains an implementation of the MCTS algorithm. Some questions remain unanswered:

    * How do we select our actions? 

* `neural_nets.py`: Contains the PyTorch models used by the MCTS algorithm. 

    * Mainly for testing purposes, the value- and policy networks are here different models. They provide:

$$\begin{align}
p_a &= Pr(a|s) \\ 
v &= \mathbb{E}[z|s]
\end{align} $$

$ x=3$




%%![ImageTitle](/blog_AZ/Loss_png.png){:class="img-responsive"}