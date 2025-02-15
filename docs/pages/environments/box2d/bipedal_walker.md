---
AUTOGENERATED: DO NOT EDIT FILE DIRECTLY
layout: env
title: Bipedal Walker
grid:
   - Action Space: Box(-1.0, 1.0, (4,), float32)
   - Observation Shape: (24,)
   - Observation High: [inf inf inf inf inf inf inf inf inf inf inf inf inf inf inf inf inf inf
 inf inf inf inf inf inf]
   - Observation Low: [-inf -inf -inf -inf -inf -inf -inf -inf -inf -inf -inf -inf -inf -inf
 -inf -inf -inf -inf -inf -inf -inf -inf -inf -inf]
   - Import: <code>gym.make("BipedalWalker-v3")</code>
---
### Description
This is simple 4-joints walker robot environment.
There are two versions:
- Normal, with slightly uneven terrain.
- Hardcore with ladders, stumps, pitfalls.

To solve the game you need to get 300 points in 1600 time steps.
To solve the hardcore version you need 300 points in 2000 time steps.

Heuristic is provided for testing, it's also useful to get demonstrations
to learn from. To run the heuristic:
```
python gym/envs/box2d/bipedal_walker.py
```

### Action Space
Actions are motor speed values in the [-1, 1] range for each of the
4 joints at both hips and knees.

### Observation Space
State consists of hull angle speed, angular velocity, horizontal speed,
vertical speed, position of joints and joints angular speed, legs contact
with ground, and 10 lidar rangefinder measurements. There's no coordinates
in the state vector.

### Rewards
Reward is given for moving forward, total 300+ points up to the far end.
If the robot falls, it gets -100. Applying motor torque costs a small
amount of points, more optimal agent will get better score.

### Starting State
The walker starts standing at the left end of the terrain with the hull
horizontal, and both legs in the same position with a slight knee angle.

### Episode Termination
The episode will terminate if the hull gets in contact with the ground or
if the walker exceeds the right end of the terrain length.

### Arguments
To use to the _hardcore_ environment, you need to specify the
`hardcore=True` argument like below:
```python
import gym
env = gym.make("BipedalWalker-v3", hardcore=True)
```

### Version History
- v3: returns closest lidar trace instead of furthest;
    faster video recording
- v2: Count energy spent
- v1: Legs now report contact with ground; motors have higher torque and
    speed; ground has higher friction; lidar rendered less nervously.
- v0: Initial version


<!-- ### References -->

### Credits
Created by Oleg Klimov