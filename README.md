# Reinforcement Learning

Exercise to implement SARSA and Q-Learning on a Grid-World problem.

You will solve several variants of the Grid World problem (a sample world is shown below in Figure 1).

![Figure 1](https://github.com/muskanjindal78/rl-sarsa-qlearning/blob/main/env.png?raw=true)

This is a grid world with 4 deterministic actions ('up', 'down', 'left', 'right'). The agent transitions to the next state determined by the direction of the action chosen with a probability of $p \in [0, 1]$. We also define a parameter called $b \in [0, 1]$ (Set $b=0.5$ for this assignment). Consider the direction of the action chosen as the agent's “North”. For example, if the action is 'left', it is the agent's North, and the agent's East would be the direction of the action 'up'. Figure 2 provides an illustration of the same. The agent transitions to the state West of the chosen action with probability $(1-p)\times b$, and to the East of the chosen action with probability $(1-p) \times (1-b)$.

 The environment may also have a wind blowing that can push the agent one **additional** cell to the right **after transitioning to the new state** with a probability of 0.4. An episode is terminated either when a goal is reached or when the timesteps exceed 100. Transitions that take you off the grid will not result in any change in state.

 ![Figure 2](https://github.com/muskanjindal78/rl-sarsa-qlearning/blob/main/env1.png?raw=true)

The dimensions of the grid are $10 \times 10$. The following types of states exist:

- ***Start state***: The agent starts from this state.
- ***Goal state***: The goal is to reach one of these states. There are 3 goal states in total.

- ***Obstructed state***: These are walls that prevent entry to the respective cells. Transition to these states will not result in any change.

- ***Bad state***: Entry into these states will incur a higher penalty than a normal state.
- ***Restart state***: Entry into these states will incur a very high penalty and will cause agent to teleport to the start state without the episode ending. Once the restart state is reached, no matter what action is chosen, it goes to the start state at the next step.
- ***Normal state***: None of the above. Entry into these states will incur a small penalty.


***Rewards***: -1 for normal states, -100 for restart states, -6 for bad states, +10 for goal states.

## Tasks
- Implement SARSA and Q-Learning.
- For each algorithm, There are total ***16 different configurations*** in total.
- For SARSA, there are a total of $8$ configurations:
  - set $p = 1$
  - wind could take one of two values, `True` or `False`
  - start state could take one of two values: `(0, 4)` or `(3, 6)`
  - exploration strategy could take one of two values: $\epsilon$-greedy or softmax
- For Q-learning, there are a total of $8$ configurations:
  - $p = 1$ or $p = 0.7$
  - set `wind = False`
  - start state could take one of two values: `(0, 4)` or `(3, 6)`
  - exploration strategy could take one of two values: $\epsilon$-greedy or softmax

- There are a total of $16$ configurations.
- For each of the $16$ configurations, determine the best set of hyperparameters (i.e. $ϵ$ in $ϵ$-greedy exploration, temperature $\beta$ in softmax exploration, learning rate $\alpha$, and discount factor $\gamma$) which maximize reward per episode over atleast 100 runs. Plot the following:
  1. Reward curves and the number of steps to reach the goal in each episode (during the training phase with the best hyperparameters).
  2. Heatmap of the grid with state visit counts, i.e., the number of times each state was visited throughout the training phase.
  3. Heatmap of the grid with Q values after training is complete, and optimal actions for the best policy.
- Try following set of values for each of the hyperparameters, for each of the configurations:

  a. learning rate ($α$) = [0.001, 0.01, 0.1, 1.0]

  b. discount factor ($γ$) = [0.7, 0.8, 0.9, 1.0]

  c. epsilon in $ϵ$-greedy = [0.001, 0.01, 0.05, 0.1] or
  
  Temperature in soft max ($τ$) = [0.01, 0.1, 1, 2]

## Configurations

There are total 16 configurations 8 each for SARSA and Q-Learning).

#### Configuration Parameters
Learning algorithm =  [0.001, 0.01, 0.1, 1.0]

Wind for SARSA= [True, False]

Wind for Q-learning = [False]

Start State = [(0,4),(3,6)]

Value of $p$ for SARSA = 1

Value of $p$ for Q-learning = [1,0.7]

Exploration strategy = ['epsilon-greedy', 'softmax']


## Results

### SARSA
1. Provide a written description of the policy learnt, explaining the behavior of the agent, and your choice of hyperparameters.
   **SARSA with Wind:**
    - **Best Hyperparameters:**
      - `start_state`: (3, 6)
      - `alpha`: 1
      - `gamma`: 1.0
      - `epsilon`: 0.001
      - `tau`: 0
      - `p`: 1
      - `wind`: True
      - `exploration_strategy`: epsilon-greedy
      - `algorithm`: SARSA
    - **Best Rewards:** -1.0
    - **Best Average Rewards:** -46.28
    - **Visit Count:**
      - High variability in visits across different states and actions, indicating some actions/states are visited more frequently than others.
    - **Q-Value Matrix:**
      - Contains some extreme values (e.g., -5021), which might indicate unstable learning or high penalties.
    
    **SARSA without Wind:**
    - **Best Hyperparameters:**
      - `start_state`: (3, 6)
      - `alpha`: 1
      - `gamma`: 1.0
      - `epsilon`: 0.001
      - `tau`: 0
      - `p`: 1
      - `wind`: False
      - `exploration_strategy`: epsilon-greedy
      - `algorithm`: SARSA
    - **Best Rewards:** -1.0
    - **Best Average Rewards:** -36.847
    - **Visit Count:**
      - More consistent visit counts compared to the wind scenario, suggesting more stable exploration.
    - **Q-Value Matrix:**
      - Q-values are generally less extreme, indicating more stable learning.
    
    **Optimal Actions Comparison:**
    - **SARSA:**
      - Actions vary between states with some actions consistently chosen in specific states.
2. This description should also provide information about how the behavior changes with and without the wind, for different levels of stochasticity and for different start states.
    1. **Wind Effect:** The presence of wind seems to impact the learning stability and effectiveness, with Q-Learning performing better than SARSA in both cases.
    2. **Algorithm Comparison:** Q-Learning tends to have more stable Q-values and better rewards compared to SARSA in the scenarios tested.
    3. **State Visit Patterns:** Both algorithms show different patterns in state visits, which affect their learning and performance.

These results suggest that Q-Learning is more robust under varying conditions (wind vs. no wind) compared to SARSA, and that consistent exploration strategies (like those without wind) generally lead to better performance.

### Q Learning

1. Provide a written description of the policy learnt, explaining the behavior of the agent, and your choice of hyperparameters.
   **Q-Learning with Wind:**
    - **Best Hyperparameters:**
      - `start_state`: (3, 6)
      - `alpha`: 1
      - `gamma`: 1.0
      - `epsilon`: 0.001
      - `tau`: 0
      - `p`: 1.0
      - `wind`: True
      - `exploration_strategy`: epsilon-greedy
      - `algorithm`: Q-Learning
    - **Best Rewards:** 0.0
    - **Best Average Rewards:** -38.128
    - **Visit Count:**
      - Visits show some patterns similar to SARSA with wind, but with different frequencies.
    - **Q-Value Matrix:**
      - Values are less extreme than SARSA with wind, which might indicate more effective learning.
    
    **Q-Learning without Wind:**
    - **Best Hyperparameters:**
      - `start_state`: (3, 6)
      - `alpha`: 1
      - `gamma`: 1.0
      - `epsilon`: 0.001
      - `tau`: 0
      - `p`: 1.0
      - `wind`: False
      - `exploration_strategy`: epsilon-greedy
      - `algorithm`: Q-Learning
    - **Best Rewards:** 0.0
    - **Best Average Rewards:** -38.128
    - **Visit Count:**
      - Shows more consistent exploration across states compared to Q-Learning with wind.
    - **Q-Value Matrix:**
      - More stable Q-values compared to Q-Learning with wind.
    
    **Optimal Actions Comparison:**
    - **Q-Learning:**
      - Actions are generally more consistent across states compared to SARSA.

2. This description should also provide information about how the behavior changes with and without the wind, for different levels of stochasticity and for different start states.
    1. **Wind Effect:** The presence of wind seems to impact the learning stability and effectiveness, with Q-Learning performing better than SARSA in both cases.
    2. **Algorithm Comparison:** Q-Learning tends to have more stable Q-values and better rewards compared to SARSA in the scenarios tested.
    3. **State Visit Patterns:** Both algorithms show different patterns in state visits, which affect their learning and performance.
    
    These results suggest that Q-Learning is more robust under varying conditions (wind vs. no wind) compared to SARSA, and that consistent exploration strategies (like those without wind) generally lead to better performance.


## Analyzing with and without wind for state (0,4)

### With Wind:

**Results for SARSA:**

Reward: -6.0,
Average Reward: -70.55

**Results for Q-Learning:**

Reward: -6.0,
Average Reward: -68.891


### Without Wind:

**Results for SARSA:**

Reward: -7.0,
Average Reward: -43.618

**Results for Q-Learning:**

Best Reward: -6.0
Average Rewards: -40.393

1. **Q-values:**

Both algorithms show non-zero Q-values in various states, with notable differences in the magnitude and distribution of these values.

2. **Visit Counts:**

The visit counts indicate how often each state was visited during the training. Higher visit counts in certain states suggest those states were more critical or challenging for the agent.

3. **Optimal Actions:**

The optimal actions derived from both algorithms indicate the preferred direction to move in each state to maximize rewards. These actions differ slightly between SARSA and Q-Learning, reflecting the different policies learned by each algorithm.

4. **Performance:**

Both algorithms perform similarly in terms of best rewards, with Q-Learning having slightly better average rewards in both wind and no-wind conditions.

5. **Impact of Wind:**

The presence of wind increases the average reward (in absolute terms), suggesting that the environment becomes more challenging with wind.
#### Conclusion:
Both SARSA and Q-Learning performed well under the given conditions, with Q-Learning showing a slight edge in average performance. The choice of hyperparameters significantly affects the performance, with high values of alpha and gamma, and a very small epsilon yielding the best results in this case. The wind introduces additional complexity, reflected in the higher (in absolute terms) average rewards.
