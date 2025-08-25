# MDP REPRESENTATION

## AIM:
To develop a stochastic Markov Decision Process (MDP) model for an autonomous warehouse robot navigating a 3x3 grid environment, delivering packages efficiently while avoiding obstacles.

## PROBLEM STATEMENT:
### Problem Description
An autonomous warehouse robot operates in a 3x3 grid layout containing shelves, aisles, and obstacles. The robot's goal is to deliver packages to the goal location (state 8) as quickly and safely as possible. The environment is stochastic: when the robot chooses an action (up, down, left, right), it may not always succeed and can end up in an unintended neighboring cell with a small probability. The environment includes blocked states (3 and 5) and slippery surfaces that can affect movement.

### State Space

S={0,1,2,3,4,5,6,7,8}
States 3 and 5 are blocked.
State 8 is the goal state.

### Sample State

0 - Initial state

### Action Space

0:up
1:down
2:right
3:left

### Sample Action

action 2 (right) from state 0:
    0.8 probability to move right to state 1
    0.1 probability to move up (state 0, stays in place)
    0.1 probability to move down (state 3, blocked)

### Reward Function

R = { +10  Goal State,
      -1   Blocked state,
       0   Otherwise  )

### Graphical Representation

![output](https://github.com/user-attachments/assets/e8ca40e0-b61a-4579-affb-695dc0222f8d)

## PYTHON REPRESENTATION:
```
import gym
P = {
    0: {
        0: [(0.8, 0, 0, False), (0.1, 0, 0, False), (0.1, 3, -1, True)],  
        1: [(0.8, 3, -1, True), (0.1, 0, 0, False), (0.1, 1, 0, False)], 
        2: [(0.8, 1, 0, False), (0.1, 0, 0, False), (0.1, 3, -1, True)],  
        3: [(0.8, 0, 0, False), (0.1, 0, 0, False), (0.1, 3, -1, True)]   
    },
    1: {
        0: [(0.8, 1, 0, False), (0.1, 0, 0, False), (0.1, 2, 0, False)],
        1: [(0.8, 4, 0, False), (0.1, 1, 0, False), (0.1, 2, 0, False)],
        2: [(0.8, 2, 0, False), (0.1, 1, 0, False), (0.1, 4, 0, False)],
        3: [(0.8, 0, 0, False), (0.1, 1, 0, False), (0.1, 4, 0, False)]
    },
    2: {
        0: [(0.8, 2, 0, False), (0.1, 1, 0, False), (0.1, 2, 0, False)],
        1: [(0.8, 5, -1, True), (0.1, 2, 0, False), (0.1, 2, 0, False)],
        2: [(0.8, 2, 0, False), (0.1, 1, 0, False), (0.1, 5, -1, True)],
        3: [(0.8, 1, 0, False), (0.1, 2, 0, False), (0.1, 5, -1, True)]
    },
    3: {
        0: [(1.0, 3, -1, True)],
        1: [(1.0, 3, -1, True)],
        2: [(1.0, 3, -1, True)],
        3: [(1.0, 3, -1, True)]
    },
    4: {
        0: [(0.8, 1, 0, False), (0.1, 3, -1, True), (0.1, 5, -1, True)],
        1: [(0.8, 7, 0, False), (0.1, 4, 0, False), (0.1, 5, -1, True)],
        2: [(0.8, 5, -1, True), (0.1, 4, 0, False), (0.1, 7, 0, False)],
        3: [(0.8, 3, -1, True), (0.1, 4, 0, False), (0.1, 7, 0, False)]
    },
    5: {
        0: [(1.0, 5, -1, True)],
        1: [(1.0, 5, -1, True)],
        2: [(1.0, 5, -1, True)],
        3: [(1.0, 5, -1, True)]
    },
    6: {
        0: [(0.8, 3, -1, True), (0.1, 6, 0, False), (0.1, 7, 0, False)],
        1: [(0.8, 6, 0, False), (0.1, 6, 0, False), (0.1, 7, 0, False)],
        2: [(0.8, 7, 0, False), (0.1, 6, 0, False), (0.1, 3, -1, True)],
        3: [(0.8, 6, 0, False), (0.1, 6, 0, False), (0.1, 3, -1, True)]
    },
    7: {
        0: [(0.8, 4, 0, False), (0.1, 6, 0, False), (0.1, 8, 10, True)],
        1: [(0.8, 7, 0, False), (0.1, 7, 0, False), (0.1, 8, 10, True)],
        2: [(0.8, 8, 10, True), (0.1, 7, 0, False), (0.1, 4, 0, False)],
        3: [(0.8, 6, 0, False), (0.1, 7, 0, False), (0.1, 4, 0, False)]
    },
    8: {
        0: [(1.0, 8, 10, True)],
        1: [(1.0, 8, 10, True)],
        2: [(1.0, 8, 10, True)],
        3: [(1.0, 8, 10, True)]
    }
}

print(P)
```

## OUTPUT:

<img width="694" height="654" alt="Screenshot 2025-08-25 121033" src="https://github.com/user-attachments/assets/1c0a38a7-be3c-4645-a770-5afe8987aee0" />
<img width="723" height="658" alt="Screenshot 2025-08-25 121100" src="https://github.com/user-attachments/assets/fced301b-5712-488f-9ee7-69da19e68b07" />
<img width="285" height="161" alt="Screenshot 2025-08-25 121105" src="https://github.com/user-attachments/assets/3140e5a0-df8e-4021-a557-2ac17fc76d0a" />



## RESULT:
The stochastic MDP model successfully represents warehouse navigation with probabilistic movements. The robot has an 80% chance of moving correctly and 10% chance of slipping, with +10 reward for reaching the goal, –1 for blocked states, and 0 otherwise. This model enables solving the task using reinforcement learning methods to find the optimal path.

