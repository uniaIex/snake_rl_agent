# game agent
snake agent python pytorch

## reinforcement learning
    ,teaching a software agent how to behave in an environment telling it how good it is doing.

reward system:

    eat food: +10
    game over: -10
    anything else: 0

actions:

    [1,0,0] straight
    [0,1,0] turn right
    [0,0,1] turn left

The agent needs to know about the environment
State (11 values)

    danger
        -straight
        -right
        -left

    direction
        -left
        -right
        -up
        -down

    food
        -up
        -down
        -right
        -left



deep Q Learning:

    Q value is the quality of action

    steps:
           0. init q value
        ->  1. choose action, predict model stat
        |   2. perform action
        |   3. measure reward
        -<  4. update q value, train model
