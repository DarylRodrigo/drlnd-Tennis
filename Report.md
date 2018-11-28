**About the Agent:**

To solve this task, I've used Multi-Agent-DDGP.


Usage of CPU:

I trained the agent on my CPU instead of using the GPU because there is more serial computation involved. Running the code on CPU was ~30% faster for me.


**DDPG Hyperparameters:**

    BUFFER_SIZE = int(1e5)  # replay buffer size
    BATCH_SIZE = 128        # minibatch size
    GAMMA = 0.99            # discount factor
    TAU = 1e-3              # for soft update of target parameters
    LR_ACTOR = 1e-5         # learning rate of the actor
    LR_CRITIC = 1e-4        # learning rate of the critic
    WEIGHT_DECAY = 0        # L2 weight decay
    UPDATE_EVERY = 1        # how many steps to take before updating target networks

* **Model architectures:**

  Actor
  
      hidden Layer 1: 128 units +leaky relu activation
      hidden Layer 2: 128 units +leaky relu activation
      hidden Layer 3: 128 units +leaky relu activation
      output Layer  : 1 unit +tanh activation
  
  Critic
  
      hidden Layer 1: 128 units +leaky relu activation
      concat Layer  : 128 + size of actionspace(4)
      hidden Layer 2: 128 units +leaky relu activation
      hidden Layer 3: 128 units +leaky relu activation
      output Layer  : 1 unit
  
* **Results:**

Environment solved after ~1556 Episodes

![](/pictures/Tennis_training_2000episodes.PNG)

* **Ideas for Future Work:**
    * Implement Prioritized Experience Replay from the DQN paper to further reduce training time.
