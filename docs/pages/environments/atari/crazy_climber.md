---
layout: env
title: Crazy Climber
grid:
   - Action Space: Discrete(18)
   - Observation Shape: (250, 160, 3)
   - Observation High: 255
   - Observation Low: 0
   - Import: <code>gym.make("ALE/CrazyClimber-v5")</code>
---

### Description
You are a climber trying to reach the top of four builidings, while avoiding obstacles like closing
windows and falling objects. When you receive damage (windows closing or objects) you will fall and
lose one life; you have a total of 5 lives before the end games. At the top of each building, there's
a helicopter which you need to catch to get to the next building. The goal is to climb as fast as
possible while receiving the least amout of damage. 


Detailed documentation can be found on [the AtariAge page](https://atariage.com/manual_html_page.php?SoftwareLabelID=113).

### Actions
By default, all actions that can be performed on an Atari 2600 are available in this environment.
However, if you use v0 or v4 or specify `full_action_space=False` during initialization, only a reduced
number of actions (those that are meaningful in this game) are available. The reduced action space may depend
on the flavor of the environment (the combination of `mode` and `difficulty`). The reduced action space for the default 
flavor looks like this:

| Num | Action                 |
|-----|------------------------|
| 0   | NOOP |
| 1   | UP |
| 2   | RIGHT |
| 3   | LEFT |
| 4   | DOWN |  
| 5   | UPRIGHT |
| 6   | UPLEFT |
| 7   | DOWNRIGHT |
| 8   | DOWNLEFT |

### Observations
By default, the environment returns the RGB image that is displayed to human players as an observation. However, it is
possible to observe
- The 128 Bytes of RAM of the console
- A grayscale image

instead. The respective observation spaces are
- `Box([0 ... 0], [255 ... 255], (128,), uint8)`
- `Box([[0 ... 0]
 ...
 [0  ... 0]], [[255 ... 255]
 ...
 [255  ... 255]], (250, 160), uint8)
`

respectively. The general article on Atari environments outlines different ways to instantiate corresponding environments
via `gym.make`.

### Rewards
A table of scores awarded for completing each row of a building is provided on [the AtariAge page](https://atariage.com/manual_html_page.php?SoftwareLabelID=113).

### Arguments

```
env = gym.make("ALE/CrazyClimber-v5")
```

The various ways to configure the environment are described in detail in the article on Atari environments.
It is possible to specify various flavors of the environment via the keyword arguments `difficulty` and `mode`. 
A flavor is a combination of a game mode and a difficulty setting.

|      Environment | Valid Modes                                                                                                                                                                         | Valid Difficulties | Default Mode |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------|--------------|
|     CrazyClimber | `[0, ..., 3]`                                                                                                                                                                       |           `[0, 1]` | `0`          |

You may use the suffix "-ram" to switch to the RAM observation space. In v0 and v4, the suffixes "Deterministic" and "Noframeskip" 
are available. These are no longer supported in v5. In order to obtain equivalent behavior, pass keyword arguments to `gym.make` as outlined in 
the general article on Atari environments.
The versions v0 and v4 are not contained in the "ALE" namespace. I.e. they are instantiated via `gym.make("CrazyClimber-v0")`.

### Version History
A thorough discussion of the intricate differences between the versions and configurations can be found in the
general article on Atari environments. 

* v5: Stickiness was added back and stochastic frameskipping was removed. The entire action space is used by default. The environments are now in the "ALE" namespace.
* v4: Stickiness of actions was removed
* v0: Initial versions release (1.0.0)
