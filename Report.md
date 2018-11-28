**About the Agent:**

To solve this task, I've used a Multi-Agent-DDGP Agent. The Agent contains an actor and a critic network. The same actor network is used for both agents to select actions. The experience is shared in the same replay buffer. While training the critic network is "judging" based on all states an actions from both agents. While execution the actors have only access to their own, individual state. Actor and Critic are trained with a local and target network-version each. The target networks are updated every step with factor TAU to achieve a soft update rule.

I noted a high variation in the outcomes at every training run. This led to a time-consuming Hyperparameter-tuning phase because to validate the changes I made one has to check the impact based on multiple runs. Although the presented outcome is near optimal, there are still many runs, that lead to poor or no learning.

Usage of CPU:

I trained the agent on my CPU instead of using the GPU because there is more serial computation involved. Running the code on CPU was ~30% faster for me.


**MADDPG Hyperparameters:**

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
    * Test other weight initialization methods, to see if training time can be systematically reduced.
