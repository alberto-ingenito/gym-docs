---
layout: env
title: Riverraid
grid:
   - Action Space: Discrete(18)
   - Observation Shape: (210, 160, 3)
   - Observation High: 255
   - Observation Low: 0
   - Import: <code>gym.make("ALE/Riverraid-v0")</code>
---

### Description
You control a jet that flies over a river: you can move it sideways and fire missiles to destroy enemy objects. Each time an enemy object is destroyed you score points (i.e. rewards). 

You lose a jet when you run out of fuel: fly over a fuel depot when you begin to run low. 

You lose a jet even when it collides with the river bank or one of the enemy objects (except fuel depots). 

The game begins with a squadron of three jets in reserve and you're given an additional jet (up to 9) for each 10,000 points you score.

Detailed documentation can be found on [the AtariAge page](https://atariage.com/manual_html_page.php?SoftwareLabelID=409)

### Actions
By default, all actions that can be performed on an Atari 2600 are available in this environment.Even if you use v0 or v4 or specify `full_action_space=False` during initialization, all actions will be available in the default flavor.

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
Score points are your only reward. You get score points each time you destroy an enemy object:
| Enemy Object | Score Points |
|--------------|--------------|
| Tanker       |  30|
| Helicopter   |  60|
| Fuel Depot   |  80|
| Jet          | 100|
| Bridge       | 500| 

For a more detailed documentation, see [the AtariAge page](https://atariage.com/manual_html_page.php?SoftwareLabelID=409).

### Arguments

```
env = gym.make("ALE/Riverraid-v5")
```

The various ways to configure the environment are described in detail in the article on Atari environments.
It is possible to specify various flavors of the environment via the keyword arguments `difficulty` and `mode`. 
A flavor is a combination of a game mode and a difficulty setting.

|      Environment | Valid Modes  | Valid Difficulties | Default Mode |
|------------------|-----------|--------------------|--------------|
|             Riverraid | `[0]`     |      `[0,1]` | `0`          |

You may use the suffix "-ram" to switch to the RAM observation space. In v0 and v4, the suffixes "Deterministic" and "NoFrameskip" 
are available. These are no longer supported in v5. In order to obtain equivalent behavior, pass keyword arguments to `gym.make` as outlined in 
the general article on Atari environments.
The versions v0 and v4 are not contained in the "ALE" namespace. I.e. they are instantiated via `gym.make("Riverraid-v0")`.

### Version History
A thorough discussion of the intricate differences between the versions and configurations can be found in the
general article on Atari environments. 

* v5: Stickiness was added back and stochastic frameskipping was removed. The entire action space is used by default. The environments are now in the "ALE" namespace.
* v4: Stickiness of actions was removed
* v0: Initial versions release (1.0.0)
