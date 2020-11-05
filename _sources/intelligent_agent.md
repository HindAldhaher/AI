Implementing a simple intelligent agent
================

## The national power grid

```{figure} figures/Kantaverkko.png
---
width: 500px
align: center
name: fig:reflexagent
---

The finnish power transmission grid maintained by the Finngrid. The distribution grid is connected to the transmission grid and is operated by distribution operators.
```

National power grid is critical infrastructure which flawless operation is extremely important for all sectors of the society. For this reason, the power system can be also a target for intentional sabotage. 

Traditionally, energy was produced by a few large power stations and consumed by consumers. This kind of power grid is simple and cost efficient. 

```{figure} figures/TreeGrid.svg
---
width: 500px
align: center
name: fig:treegrid
---

A tree structured power grid. The production is mostly centralized and consumption in on the leaves. The blue vertices are substations.
```

The substations takes care of the delivery of the power to the branches and they also monitor the power distribution, and possible faults. If a fault is found it can cut off power on some branches. The branches are protected by so called *protection relays*, which monitor the voltages and current in the distribution line. This kind of protection relay could be implemented as as simple reflex agent. 

```{figure} figures/protectionRelays.png
---
width: 500px
align: center
name: fig:reflexagent
---

An example of protection in a substation.
```


```{figure} figures/reflex_agents.png
---
width: 500px
align: center
name: fig:reflexagent
---

The simple reflex agent which monitors the power grid through current and voltage sensors.
```

### Perceptions

An intelligent agent needs to maintain it's awareness of the situation by perceptions. In power systems the perceptions are usually obtained by current and voltage sensors. The agent can further process this information by calclating for example the sum of three phase voltages and calculate total power flown trough a cable. Quite often the agent also monitors the frequency of the powerline through these current measurements. More advanced protection relays may also monitor the shape of the current and react if it deviates from a sinusoidal waveform. The percepts directly and indirect calculated features provide information about the environment, which lets the agent to know enough from the state of the environment to decide actions. 

```{figure} figures/PV_system_fault.svg
---
width: 500px
align: center
name: fig:reflexagent
---

An example of the measurements of three phase currents during a fault starting at 8.66 s. The figure displays also the sum of all currents calculated by the individual phase current measurements. 
```

Some more advanced protection relays may also make other observations. For example arc protection relays monitor optically if they can see an electric arc due to short cuts. These arc protection relays can potentially find and react some serious faults faster than those only measuring the powerline only.

### Decision rules
The decisions rules of the reflex agent are rather simple, since it does not have a model of the system. It can for example act as follows:

  - If one of the phase currents are above the nominal threshold, say 0.75 of the maximum, there is probably a shortcut on the line, then act by cutting down the power from that line.
  - If the combined power exceeds a threshold, for example 0.75 of the maximum power, then there is probably a shortcut or overloading situation, then cut down the power on the power line in question.
  
These decision rules are simple and they can be described using logics and programmed directly 
  

### Telecommunication based protection

Some of these protection relays may also implement some additional commands over telecommunication network. These can be for example:

 - Remote control. A remote system can send direct commands to shut down power in a specific powerline. In this case the decision is made already in the extenal node and it just simply overrides the decision mechanism of the agent.
 - Another node can send remote observations over telecommunication network. For example a pair of agents can monitor the currents in both ends of the powerline segment to detect leakage. Then one of the relays can react to potentially dangerous leakage by cutting the power out of the powerline segment.
 
### Actions
Typically the protective action made by a protecting relay is that it sends a command to switch to open, in order to cut the power from a power line. 

Sometimes the fault in the powerline can be intermittent, and a protection relay can also carry out a recovery procedure which includes disconnecting the power for a short while, and then try to reconnect it back. This procedure may be enough to shut down arcs on the cable, after which the system starts working again.


## Smart grid

The power system has been under a lot of changes during last decades due to changes in power production to reduce the CO2 emissions. Some of them are:

 - The introduction of Variable Renewable Energy (VRE) sources, like wind and solar power.
 - Large scale distributed energy production
 - Heat is increasingly produced by electricity, often by heat pumps
 - Energy storage is becoming more difficult
 
In the future smart grid, energy flows bi-directionally and distributed production and consumers need to participate in keeping the network stable, maintaining the balance of consumption and production. The situational awareness needs to known at global level and produceres and consumers needs to co-operate. The fault diagnosis and control in bi-directional power grid cannot be accomplished by local measurements alone any longer.


```{figure} figures/SmartNetwork.svg
---
width: 500px
align: center
name: fig:smartGrid
---

A Smart power grid with network structure due to redundancy and bi-directional power flow due to distributed power production.
```

The smart grid shown in the figure above is an inevitable consequence of the changes in the power production. Due to local production, some parts of the power grid could operate as separate islands in case of failure of the main transmission grid. To protect the consumers and to secure the flawless power delivery, the decisions for reacting faults and possibly changing oeration modes need to be made very fast, but at the same time the number of different options have grown exponentially due to combinatorial explosion of options. 

But if Alpha-Go was able to play Go-game, which is even more challenging problem, could it be also take care of operating smart grid better than a human operator?

### Intelligent agent as a smart grid operator

An agent capable of operating a smart grid needs to be more powerfull than a simple reflex agent. The fault locating and control decisions cannot be made on only local measurements any longer, but a wider area situational awareness is needed. A model of the power grid is the first prerequisite for smarter operation. The structure of the power grid can be modelled as bi-directional network graph, including loops. 

The graph can include information about the cable lengths, capacities and other properties on the edges. The nodes (or vertices) would be the end points of cables: power stations, substations (power distribution structures in the branches of the grid) or consumers. The nominal power of consumers and power plants would be stored in the vertices. 

```{figure} figures/utility_agents.png
---
width: 500px
align: center
name: fig:utilityagent
---

The utility agents extend the simple reflex agent by including a model having capability to plan actions and considering the utility gained by reaching the goal through different action sequences.
```


#### Fault detection by machine learning
The currents and voltages on the powerline would be monitored by sensors connected to local computational devices, which would locally calculate relevant features about the measurements using suitable signal processing methods. The features would be sent to the computing center which would apply machine learning algorithms to judge if the situation is normal or not. For example, a classifier trained for anomaly detection (or outlier detection) could be used. Regression methods could be used to calculate additional information to improve situational awareness. 

The fault detection algorithm running on the computing center could use many measurements from different locations to make the fault detection more powerfull.

These algorithms would need potentially plenty of training data. They could be run at first on side by side by the human operator, and it could learn to perform in the same way. But it is often find out afterwards that the decisions made by a human operator were not after all very optimal. Deeper analysis can be used to find out optimal solutions and those can be trained to the AI agent, to train it to react better than human operator. 

#### Fault location by graph search 
When a fault is detected and cannot be automatically fixed, it needs to located to make the manual reparation faster.  Some new methods 

#### Commercial solutions
A company called *safegrid*


