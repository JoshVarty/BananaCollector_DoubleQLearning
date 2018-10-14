# Banana Collector

Unity's Banana Collector Environment is an environment in which an agent must collect as many yellow bananas (+1) as possible while avoiding blue bananas (-1).

![Banana Collector Environment](https://user-images.githubusercontent.com/10624937/42135619-d90f2f28-7d12-11e8-8823-82b970a54d7e.gif)

This repository trains an agent to attain an average score (over 100 episodes) of at least 13. It trains the agent using the Double DQN Reinforcement Learning algorithm.

## Prerequisites
 - Python 3
 - Jupyter Notebooks
  

## Usage
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


## Results

In my experience the agent achieves an average score of 13 after ~400 episodes of training:

![image](https://user-images.githubusercontent.com/1249087/46922119-794d7000-cfd2-11e8-962f-1bad16917e37.png)



## Notes
 - Only tested on Ubuntu 18.04

