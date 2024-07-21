# Week 3: Reinforcement Learning

## Introduction to Reinforcement Learning

### Overview

Reinforcement learning is an unsupervised learning model based on a reward function that rewards desired behaviors and punishes negative ones. The model iterates over “state”, in which a decision must be made, and rewards are typically applied at the “terminal state”, which is a desired final condition marking the end of a learning outcome.

### Key Concepts

#### Return

The return is a way of comparing rewards and determining which ones are better or worse. It sums the rewards from each step and weighs them with a discount factor, γ, until the terminal state is reached:

$$\text{Return} = R_1 + \gamma R_2 + \gamma^2 R_3 + \ldots + \gamma^n R_n$$

By decreasing the gamma value in each subsequent step, the algorithm becomes incentivized to finish as fast as possible. The discount factor also incentivizes the system to push out negative rewards as far into the future as possible.

#### Policies

A policy is a function that takes an input state and maps it to an action. The goal is to find a policy that gives an action for every possible state to maximize the return. Different policies can be used, such as always going for the nearest reward or always going for the larger reward.

### Model Algorithms

#### State-action Value Function (Q-function)

The Q-function, Q(s, a), gives the return if starting in state s and taking action a once, then behaving optimally after. The Q-function is recursively calculated to cover all possible scenarios and the best possible return is selected from each state, defining the overall policy of the model.

#### Bellman Equation

The Bellman equation is used to compute the Q-function:

$$Q(s,a) = R(s) + \gamma \max_{a'} Q(s', a')$$

This equation defines a recursive function that iterates through all states and uses the maximum reward from the following state.

### Stochastic Environments

In stochastic environments, the outcome of an action is not always completely reliable. Actions are represented as probabilities, and the goal is to maximize the average value of rewards across many attempts. The Bellman equation is modified to account for this randomness:

$$Q(s,a) = R(s) + \gamma E[\max_{a'} Q(s', a')]$$

### Continuous State Spaces

In continuous state spaces, the state can be a range of values or a spectrum, often including a combination of variables. For example, an autonomous car's state could include position, velocity, and acceleration.

### State-value Function and Neural Networks

The state-value function uses a neural network to compute the return (Q-function) for every possible action in a given state and picks the action maximizing the return. The Bellman equation is used to create a training set with lots of examples, and supervised learning is used to create the mappings from state-action pairs to returns.

### Learning Algorithm

1. Initialize the neural network parameters randomly.
2. Take various actions (good, bad, random, deliberate) and store them as training data tuples.
3. Train the neural network using the state-value function to predict desired outputs.
4. Set the return produced by the model as the initial return for the next model.

### Refining the Learning Algorithm

#### Improving Neural Network Architecture

Instead of outputting a single unit in the output layer, compute the return for all possible actions, each one being a unit in the output layer. This improves efficiency and makes parts of the Bellman equation more efficient.

#### Epsilon-greedy Policy

The Epsilon-greedy policy helps in choosing actions while learning. With probability ε, pick a random action (exploration), and with probability 1-ε, pick the action that maximizes the return (exploitation). This value usually starts high and gradually decreases.

#### Mini-batch Gradient Descent

Mini-batches involve picking a subset of training examples to speed up computing time. This technique is used after storing tuples in the replay buffer, and helps in reducing memory load and improving efficiency.

#### Soft Updates

Soft updates involve fractionally modifying the Q-function parameters to avoid abrupt changes and noisy updates. This method helps the model converge on an optimal return more reliably.

### Application: Lunar Lander

The lunar lander application involves training a neural network to approximate the Q-function for controlling a simulated vehicle to land on the moon's surface. The state space includes the lander's position, velocity, angle, and whether the legs are grounded. The learning algorithm for this task uses deep learning and the DQN algorithm, which involves training with Bellman's equations and using the Epsilon-greedy policy for action selection.

---

### Quizzes

#### Practice Quiz: Reinforcement Learning Introduction

#### Question 1

<img src="../quizzes/Quiz 4 - Reinforcement learning introduction q1.png" alt="practice quiz 3 question 1" width="70%" style="min-width: 850px">

<details>
<summary>    
    <font size='3' color='#00FF00'>Answer to <b>question 1</b></font>
</summary>
<p>If you selected <em>state</em>, then you are right!<br/><b>Explanation:</b><br/>The position of the robot is considered its state.</p>
</details>

#### Question 2

<img src="../quizzes/Quiz 4 - Reinforcement learning introduction q2.png" alt="practice quiz 3 question 1" width="70%" style="min-width: 850px">

<details>
<summary>    
    <font size='3' color='#00FF00'>Answer to <b>question 2</b></font>
</summary>
<p>If you selected <em>R(1) > R(2) > R(3), where R(1) and R(2) are positive and R(3) is negative</em>, then you are right!<br/><b>Explanation:</b><br/>To reflect the varying levels of happiness based on the state, R(1) > R(2) > R(3) with R(1) and R(2) positive and R(3) negative is appropriate.</p>
</details>

#### Question 3

<img src="../quizzes/Quiz 4 - Reinforcement learning introduction q3.png" alt="practice quiz 3 question 1" width="70%" style="min-width: 850px">

<details>
<summary>    
    <font size='3' color='#00FF00'>Answer to <b>question 3</b></font>
</summary>
<p>If you selected <em>-0.75*100 - 0.75^2*100 + 0.75^3*1000</em>, then you are right!<br/><b>Explanation:</b><br/>With a discount factor of 0.75, the return is calculated as -100 - 0.75*100 + 0.75^2*1000.</p>
</details>

#### Question 4

<img src="../quizzes/Quiz 4 - Reinforcement learning introduction q4.png" alt="practice quiz 3 question 1" width="70%" style="min-width: 850px">

<details>
<summary>    
    <font size='3' color='#00FF00'>Answer to <b>question 4</b></font>
</summary>
<p>If you selected <em>6.25</em>, then you are right!<br/><b>Explanation:</b><br/>Starting from state 3, the rewards are in states 3, 2, and 1. The return is 0 + 0.25*0 + 0.25^2*100 = 6.25.</p>
</details>

---

#### Practice Quiz: State-action Value Function

#### Question 1

<img src="../quizzes/Quiz 5 - State-action value function q1.png" alt="practice quiz 3 question 1" width="70%" style="min-width: 850px">

<details>
<summary>    
    <font size='3' color='#00FF00'>Answer to <b>question 1</b></font>
</summary>
<p>If you selected <em>It is the return if you start from state s, take action a (once), then behave optimally after that</em>, then you are right!<br/><b>Explanation:</b><br/>This describes the state-action value function Q(s,a).</p>
</details>

#### Question 2

<img src="../quizzes/Quiz 5 - State-action value function q2.png" alt="practice quiz 3 question 1" width="70%" style="min-width: 850px">

<details>
<summary>    
    <font size='3' color='#00FF00'>Answer to <b>question 2</b></font>
</summary>
<p>If you selected <em>STOP</em>, then you are right!<br/><b>Explanation:</b><br/>The optimal action to take in state s is STOP because it has the greatest value.</p>
</details>

#### Question 3

<img src="../quizzes/Quiz 5 - State-action value function q3.png" alt="practice quiz 3 question 1" width="70%" style="min-width: 850px">

<details>
<summary>    
    <font size='3' color='#00FF00'>Answer to <b>question 3</b></font>
</summary>
<p>If you selected <em>0.625</em>, then you are right!<br/><b>Explanation:</b><br/>We get 0 reward in state 5, then 0 ∗ 0.25 discounted reward in state 4, since we moved left for our action. Now we behave optimally starting from state 4 onwards. So, we move right to state 5 from state 4 and receive 0.25^2 ∗ 2 discounted reward. Finally, we move right in state 5 to state 6 to receive a discounted reward of 40 ∗ 0.25^3. Adding these together we get 0.625.</p>
</details>

---

#### Practice Quiz: Continuous State Spaces

#### Question 1

<img src="../quizzes/Quiz 6 - Continuous state spaces q1.png" alt="practice quiz 3 question 1" width="70%" style="min-width: 850px">

<details>
<summary>    
    <font size='3' color='#00FF00'>Answer to <b>question 1</b></font>
</summary>
<p>If you selected <em>The state contains numbers such as position and velocity that are continuous valued.</em>, then you are right!<br/><b>Explanation:</b><br/>The Lunar Lander is a continuous state MDP because the state contains numbers such as position and velocity that are continuous valued.</p>
</details>

#### Question 2

<img src="../quizzes/Quiz 6 - Continuous state spaces q2.png" alt="practice quiz 3 question 1" width="70%" style="min-width: 850px">

<details>
<summary>    
    <font size='3' color='#00FF00'>Answer to <b>question 2</b></font>
</summary>
<p>If you selected <em>y = R(s) + γ max a′ Q(s′, a′) where s′ is the state you get to after taking action a in state s</em>, then you are right!<br/><b>Explanation:</b><br/>The learning algorithm described in the videos involves applying supervised learning where the input \(x = (s, a)\) and the target is constructed using Bellman’s equations as y = R(s) + γ max a′ Q(s′, a′) where s′ is the state you get to after taking action a in state s.</p>
</details>

#### Question 3

<img src="../quizzes/Quiz 6 - Continuous state spaces q3.png" alt="practice quiz 3 question 1" width="70%" style="min-width: 850px">

<details>
<summary>    
    <font size='3' color='#00FF00'>Answer to <b>question 3</b></font>
</summary>
<p>If you selected all options, then you are right!<br/><b>Explanation:</b><br/>All statements describe what you’ve accomplished by reaching the final practice quiz of the class. Congratulations!</p>
</details>

---

This week's content provided an in-depth understanding of reinforcement learning, covering key concepts such as return, policies, Q-function, Bellman equation, stochastic environments, and continuous state spaces. It also explored the practical application of reinforcement learning algorithms through neural networks and advanced techniques like mini-batch gradient descent and soft updates. The lunar lander application demonstrated how these concepts are applied in real-world scenarios.
