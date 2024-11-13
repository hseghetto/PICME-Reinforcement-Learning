## PICME-Reinforcement Learning
This is a simplified implementation of a Monte Carlo Tree Search (MCTS) combined with a Convolutional Neural Network (CNN) model, inspired by AlphaZero. 

The model is trained by having the network play against itself using a MCTS with 20 simulations and decaying temperature.
The model only has access to the available legal moves at each step and receives feedback on the game outcome (win or loss) once the game ends.
Q-values and Z-values are initialized such that the model initially prioritizes the game-state outcomes (win, loss, or tie) for each action over the MCTS-estimated rewards. As training progresses, the model gradually shifts to valuing the MCTS-estimated rewards more heavily than the final game-state outcomes.

Initially developed in a Tic-Tac-Toe environment, it was later generalized to support m,n,k-games. Current implementation incorporates episode batching and a combined policy-value head. 


##  Performance Results:

+  Each episode simulation took approximately 200-250ms, with the entire training process completed in 200 episodes (around 10 minutes, including in-training evaluation) and the CNN architecture had just under 14,000 parameters.
+  The MCTS model achieved a near 90% win rate as Player 1 against a random agent and approximately 50% as Player 2. However, for single-shot predictions, the win rates were lower, reaching around 65% for Player 1 and 40% for Player 2.
+  Against a semi-optimal agent with game-specific knowledge, the MCTS model managed to achieve a 100% draw rate as Player 1 and a 40% draw rate as Player 2.
+  These results indicate that the model successfully learns the fundamental strategies required to play the game. However, it appears to struggle with unconventional moves and the inherent disadvantage of playing as Player 2.

## Potenial Improvements:

+  Increased Exploration: Adjusting the balance between exploration and exploitation in MCTS (e.g., by further tuning the temperature decay or adding more simulations) could help the model better handle unconventional moves.
+  Data Augmentation: During training, symmetric transformations of the board states (e.g., rotations and reflections) can be applied to generate additional training examples from existing ones. This technique effectively expands the training dataset, enabling the model to better generalize and recognize patterns across different configurations.
+  Larger Models and Extended Training: Increasing the model size and extending the training duration with more episodes could enhance generalization and further refine the model's decision-making, both in handling uncomon moves and more capable opponents.
+  More Parameter Tunning: Other parameter such as Q&Z-values, learning rate, batch sizes, games per run and simulations per move can potentially be tweak to increase performance.
