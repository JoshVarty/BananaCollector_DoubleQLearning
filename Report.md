# Report


## Learning Algorthim

My agent uses [Double DQN](https://arxiv.org/abs/1509.06461) to solve this task. The agent consists of two distinct processes:
 1. Sampling states, actions and rewards from the environment
 2. Periodically using these observations to improve a function-approximating neural network that predicts the value of a given state and action


### Sampling 

Our agent starts off knowing nothing about the environment. It begins learning about its environment by taking primarily random actions. It records the resulting tuple of `(state, action, reward, next_state, done)` in a replay buffer of size `100,000`. 

As training progresses, the agent tries to rely less on choosing random actions and instead chooses what the neural network predicts to be the best action. This behavior is governed by [`Agent.act(self, state, eps=0.0)`](https://github.com/JoshVarty/BananaCollector_DoubleQLearning/blob/6c36c9a6dd27be7a48d391085ba003ccaf6155da/dqn_agent.py#L60-L78). As epsilon (`eps`) decreases, it becomes increasingly likely that the greedy action is taken. Epsilon starts at `1.0` and is decreased by a factor of `0.995` per episode and will decrease down to a minimum of `0.01`. 


### Updating

After the agent has taken `64` (`BATCH_SIZE`) actions and recorded the resulting `(state, action, reward, next_state, done)` tuples in the replay buffer, it is ready to begin learning. Every `4` (`UPDATE_EVERY`) time steps the agent randomly samples an experience from its replay buffer and passes it to [`Agent.learn(self, experience, gamma)`](https://github.com/JoshVarty/BananaCollector_DoubleQLearning/blob/6c36c9a6dd27be7a48d391085ba003ccaf6155da/dqn_agent.py#L80-L107). Randomly sampling experiences in this fashion allows our agent to avoid training on highly correllated experiences (which is a problem for neural networks).

Our network computes weight updates using the Double DQN Learning update algorithm. This method requires us to maintain two networks:
 - One local network we use to choose the best action **and** to compute the currently expected values for a given state-action pair
 - A target network we use the evaluate the actual value of the best action.

 After computing the expected value and the target value, we calculate the mean-squared-error between the two and train **only** the local network. We then perform gradient descent to train the local network. After training the local network, we soft-update to update the parameters of the target network. An alternative approach might be to simply swap the networks after a predetermined number of training steps.

There are a number of hyperparameters to consider:
- Gamma: `0.99` 
   - A high value of gamma allows us to prioritize the long-term rewards of the agent

- BATCH_SIZE: `64`
   - This governs the minimum required samples before we are ready to begin learning. It was somewhat arbitrarily chosen but ensures that there are enough samples that when we randomly choose from them we don't expect the samples to be closely correlated.

- Learning Rate: `5e-4`
   - The learning rate governs how quickly the neural network learns. This was the first value chosen, but if our network had not been learning properly I would have tried lowering the value to make more incremental progress. 

- TAU: `5e-4`
  - This parameter governs how quickly the expected network is updated with values from the local network. If too high of a value is chosen (say `1.0`)then our local network will be chasing a non-stationary target which typically prevents the network from learning or may even cause it to diverge completely. 

- UPDATE_EVERY: `4` 
  - This parameter governs how frequently we train the local network on a newly sampled experience. Using a value greater than `1` helps to ensure we are training on less uncorrelated values. 

### Model Architecture

The local neural-network and expected neural network have have the following identical structure defined in [`model.py`](https://github.com/JoshVarty/BananaCollector_DoubleQLearning/blob/6c36c9a6dd27be7a48d391085ba003ccaf6155da/model.py):

 - A fully connected layer with `37` inputs and `128` outputs using ReLU activations
 - A fully connected layer with `128` inputs and `256` outputs using ReLU activations
 - A fully connected layer with `256` inputs and `256` outputs using ReLU activations
 - A fully connected layer with `256` inputs and `256` outputs using ReLU activations
 - A fully connected layer with `256` inputs and `4` outputs

The input to the network is the current state (a vector with `37` elements). The output represents the networks raw value-score of each of `4` actions.

## Results

After approximately three hours (300 episodes) of training on my local machine, my agent achieved an score greater than 13.0. Its progress is shown below.

![Score over 400 epsiodes](https://user-images.githubusercontent.com/1249087/46922119-794d7000-cfd2-11e8-962f-1bad16917e37.png)


## Future Work

Double DQN Learning seemed to work very well on my first try so I did not have to play around with any hyperparameters. However, it is possible that changing some of these hyperparameters might allow for faster training or training to a higher score. It's also possible that my agent may have continued to improve beyond a score of 13.0 if left to continue learning.

It's possible that my network choice was not optimal. It seemed to take my network much more time to train than I expected (based on experience training larger networks for image recognition). A few questions come to mind:

 - Was my network too large for this task?
 - Was the bottleneck the environment or the neural network?

One other thought I had was whether or not it would make sense to use batches of experiences to train the network instead of just a single experience. When training conv nets we would usually train on batches of 64 or 128 images at a time, does this approach also work with reinforcement learning?

Further improvements would be to use the following:
 - Prioritized Experience Replace
 - Duelling DQN
 - Noisy DQN