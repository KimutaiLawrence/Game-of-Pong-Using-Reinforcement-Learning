# Game-of-Pong-Using-Reinforcement-Learning
Training an agent to beat the computer  using Reinforcement Learning. Simply the power of A.I !
Game of Pong Using Reinforcement Learning 
Reinforcement Learning:
Reinforcement learning is a machine learning training strategy that rewards positive actions while penalizing undesirable ones. A reinforcement learning agent, in general, is capable of seeing and interpreting its surroundings, taking actions, and learning via trial and error. The primary assumption of RL is to create a history of encounters for the AI, also known as the Agent in the field.

Pong from Pixels: The Game of Pong was trained purely from image-pixels. This means it doesn't have to follow any rules/program but basically follow the A.I Model. Atari was developed around 1970’s to host video game consoles. To effectively learn to play Atari Pong, an AI Agent must play multiple rounds of the game, observe which actions for a given input* image works best, and then modify its behavior to increase the frequency of the actions that worked well for the input and decrease the frequency of the actions that didn't.

Keywords: Reinforcement Learning, Agent, A.I, Atari Pong

How it works:
The OpenAI gym environment is used to launch the Atari Pong emulation and accept inputs, allowing our Agent to make moves.

Rewards:
In order to select which actions to execute, RL employs the concept of rewards/incentives, and for the game of Pong, the reward is simply a +1 for every round the Agent wins, and a -1 for every round the opponent CPU wins. Other games, such as Space Invaders, might relate incentives to point increments gained for shooting down different sorts of aliens, but computing rewards in real-life applications can be more difficult, especially when there is no evident single score or target to optimize.

Policy:
A policy describes the learning agent's behavior at a specific point in time. A policy, in broad terms, is a mapping from perceived environmental states to actions to be conducted while in those situations.In the instance of Pong, the policy assists the Agent in selecting one of the potential actions, which include moving the paddle up, down, or doing nothing.

Parameters:
To ensure that the the algorithm can explore and learn on its own while interacting with a complicated environment in a continuous control issue, a set of parameters must be established. These include:
1.  num_hidden_layers: How many neurons are in our hidden layer
2.  games_to_play:number of games to play before neural network update
3.  learning_rate: The rate at which we learn from our results to compute the new weights. A higher rate means we react more to results and a lower rate means we don’t react as strongly to each result.
4.  backprop_rate: decay factor for RMSProp leaky sum of weight_gradients^2
5.  discount_rate = 0.99 # The discount factor we use to discount the effect of old actions on the final result.
The hidden layer output is transferred to a sigmoid function, which essentially compresses the output into a probability range between 0 and 1. The image to be used in the game of pong is transformed into something we can work with through pre-processing  by Cropping the image, Converting the image to black and white by removing color, removing the background and flattening.

Reward Discounting:
One way we may improve is to be intelligent about how we assign rewards for actions.The most recent action or frame previous to the Agent receiving a reward is the most relevant and should thus be encouraged in the case of a positive reward and discouraged in the case of a negative reward.
Because there is just one reward for winning a game in Pong, the rewards setup is extremely basic, but in more complicated situations, discount functions may be utilized as part of Value functions in Reinforcement Learning problems to assess the state based on predicted future rewards. This can be shown by the equation below:


<!-- Where ,r = the magnitude of the reward for a given timestamp t + n,  γ = the discounting factor, n =the number of timesteps and H is the horizon for which we count the rewards.  -->
<!-- Neural Networks and the Policy network: -->
<!-- So our structure looks like this: -->
<!-- Neural Network Structure ( Andrej Karpathy, Pong from Pixels blog post) -->

The policy network, which is used to decide what to do next depending on the input in the case of Pong and many Atari games, is a fully-connected Neural Network with n hidden layers, which is why this approach is referred to as Deep RL, even though we only have one hidden layer in this post. The Neural Network  takes a frame image of the game as input, with each pixel representing an individual input neuron, and outputs a decimal probability between 0 and 1, corresponding to the likelihood that the action our agent has made in the past for a comparable image was a UP move. It is worth noting that if the probability is less than 0.5, the closer it is to 0, the more likely it is that the agent chose a DOWN move.
Because there are no labels or ground truth in RL, we create false labels that match to the rewards earned at the conclusion of a round to compute the loss and gradients. The loss and gradient vectors are used to update the NN weights using back-propagation and an optimization technique, which is used to promote the action that resulted in a positive reward (by increasing its output probability), and vice versa for a negative reward. The bogus label is decided by the previously computed discounted Advantage factor Ai, the amount of which is determined by how much we discounted the reward for that activity.

The RMS Prop optimization approach is used to update the weights in the NN – after 10 episodes, we do a parameter update to guarantee that the NN gradients are modified and that the NN converges as quickly as possible. 

The final result is A.I-powered-game trained for up to more than 10,000 episodes.

References 
Schultz, W., Dayan, P. & Montague, P. R. A neural substrate of prediction and reward. Science 275, 1593–1599 (1997)
Andrej Karpathy, Learning to play Pong from Pixels by Andrej Karpathy
OpenAI Spinning up in RL
David Silver Deep RL Lecture series
https://books.google.co.uk/books?id=Hd9YDwAAQBAJ&pg=PA120&dq=for+t+in+reversed(xrange(0,+rewards.size)):&hl=en&sa=X&ved=0ahUKEwj0iN3EgProAhXvQEEAHfVJAswQ6AEIKDAA#v=onepage&q=xrange&f=false
 
