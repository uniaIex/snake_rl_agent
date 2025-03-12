# Snake AI with Deep Q-Learning

This project demonstrates how **Q-Learning** combined with a neural network can train an AI to play the classic Snake game. The AI agent learns to maximize its score by avoiding collisions and eating food efficiently. Built using PyTorch for the neural network and Pygame for game rendering, this implementation highlights key concepts in reinforcement learning (RL).

## Overview
The Snake AI uses a **Deep Q-Network (DQN)** to approximate the Q-value function, which helps the agent decide the best actions. Key components include:
- **Q-Learning**: A model-free RL algorithm that learns the value of actions in a given state.
- **Experience Replay**: Stores past experiences (state, action, reward, next state) to break correlations in training data.
- **Epsilon-Greedy Strategy**: Balances exploration (random actions) and exploitation (learned policy).

## Project Structure
- `agent.py`: Defines the RL agent, state representation, and training logic.
- `game.py`: Implements the Snake game environment and mechanics.
- `model.py`: Contains the neural network architecture (`Linear_QNet`) and the Q-learning trainer (`QTrainer`).
- `helper.py`: Plots training progress (scores and mean scores over games).

## Dependencies
- Python 3.7+
- PyTorch
- Pygame
- NumPy
- Matplotlib

# How It Works

## State Representation
The agent observes an **11-dimensional state vector** containing:
- **Danger Signals** (3 boolean values):
  - Collision risk straight ahead
  - Collision risk to the right
  - Collision risk to the left
- **Direction** (4 boolean values):
  - Current movement: Left/Right/Up/Down
- **Food Location** (4 boolean values):
  - Food positioned left/right/above/below the snake's head

## Neural Network Architecture
- **Input Layer**: 11 nodes (matches state vector size)
- **Hidden Layer**: 256 nodes with ReLU activation
- **Output Layer**: 3 nodes (possible actions: straight, right turn, left turn)

## Training Process

### Action Selection (ε-Greedy Policy)
- **Exploration**:
  - Random action with probability `ε` (epsilon)
- **Exploitation**:
  - Use neural network's predicted optimal action  
  *Epsilon decays as the agent gains experience*

### Reward System
| Event                | Reward |
|----------------------|--------|
| Eating food          | +10    |
| Collision/starvation | -10    |
| Normal movement      | 0      |

### Experience Replay
- Stores past experiences in a replay buffer (`deque`)
- Samples mini-batches (1,000 experiences) for training
- Reduces correlation between consecutive samples

### Q-Learning Update
- Uses **Mean Squared Error (MSE)** loss
- Implements Bellman equation:
- Updates network weights via backpropagation

## Hyperparameters
| Parameter      | Value     | Description                          |
|----------------|-----------|--------------------------------------|
| `LR`           | 0.001     | Learning rate                        |
| `GAMMA`        | 0.9       | Future reward discount factor        |
| `MAX_MEMORY`   | 100,000   | Experience replay buffer capacity    |
| `BATCH_SIZE`   | 1,000     | Training batch size                  |