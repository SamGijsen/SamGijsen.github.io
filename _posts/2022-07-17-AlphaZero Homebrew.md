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


* `neural_nets.py`: Contains the PyTorch models used by the MCTS algorithm. 

    * Mainly for testing purposes, the value ($v = f_\theta(s)$) and policy ($p=f_\theta(s)$) networks are here different models. They take in the current board state $s$ and they provide:

    $$\begin{align}
    p_a &= Pr(a|s) \newline 
    v &= \mathbb{E}[z|s]
    \end{align} $$

    * with $z$ being the game outcome, $v$ an estimator of the expected game outcome $z$, and $p_a$ a vector of move probabilities.

* `mcts.py`: Contains an implementation of the MCTS algorithm. Some questions remain unanswered:

    * How exactly does MCTS select actions? A *UCT* (Upper Confidence bound for Trees) is computed as follows:

    $$\begin{align}
    UCT(s,a) = c p_a \frac{\sqrt{\sum_A N(s,A))}}{1 + N(s,a)}
    \end{align}$$

    * where $p_a$ are the prior move probabilities provided by the network and $N$ the amount of times we've taken a certain action $a$ or summed over all potential actions $A$.



%%![ImageTitle](/blog_AZ/Loss_png.png){:class="img-responsive"}