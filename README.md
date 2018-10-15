# Banana Collector

Unity's Banana Collector Environment is an environment in which an agent must collect as many yellow bananas (+1) as possible while avoiding blue bananas (-1). 

The agent interacts with the environment via the following:
 - It is fed observations of the current state via a vector of 37 elements
 - It can choose to make any of 4 actions: (Left, Forward, Right or Back)

<center>  

![Banana Collector Environment](https://user-images.githubusercontent.com/10624937/42135619-d90f2f28-7d12-11e8-8823-82b970a54d7e.gif)

*Sample image taken from: https://github.com/udacity/deep-reinforcement-learning/tree/master/p1_navigation*



</center>

This repository trains an agent to attain an average score (over 100 episodes) of at least 13. It trains the agent using the Double DQN Reinforcement Learning algorithm.

## Prerequisites

- Anaconda
- Python 3.6
- A `conda` environment created as follows

  - Linux or Mac:
  ```
  conda create --name drlnd python=3.6
  source activate drlnd 
  ```

  - Windows
  ```
  conda create --name drlnd python=3.6 
  activate drlnd
  ```

- Required dependencies

```
git clone https://github.com/udacity/deep-reinforcement-learning.git
cd deep-reinforcement-learning/python
pip install .
```
 
  

## Getting Started
1. `git clone https://github.com/JoshVarty/BananaCollector_DoubleQLearning.git`
2. `cd BananaCollector_DoubleQLearning`
2. Download Unity Banana Collector Enviroment:
   - Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Linux.zip)
   - Linux Headless: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana.app.zip)
   - Mac OSX: [click here]()
   - Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86.zip)
   - Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86_64.zip)

3. Unzip to git directory
4. `jupyter notebook`
5. You can train your own agent via [`DQN.ipynb`](https://github.com/JoshVarty/BananaCollector_DoubleQLearning/blob/master/DQN.ipynb) or watch a single episode of the pre-trained network via [`Visualization.ipynb`](https://github.com/JoshVarty/BananaCollector_DoubleQLearning/blob/master/Visualization.ipynb)


## Results

In my experience the agent achieves an average score of 13 after ~400 episodes of training:

![image](https://user-images.githubusercontent.com/1249087/46922119-794d7000-cfd2-11e8-962f-1bad16917e37.png)


A sample run generated from [`Visualization.ipynb`]()

![](https://i.imgur.com/c95Uglu.gif)


## Notes
 - Only tested on Ubuntu 18.04
 - Details of the learning algorithm and chosen architecture may be found in [`Report.md`](https://github.com/JoshVarty/BananaCollector_DoubleQLearning/blob/master/Report.md)

