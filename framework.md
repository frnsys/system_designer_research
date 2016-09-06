Notes from [Pandora: A Versatile Agent-Based Modeling Platform for Social Simulation](https://www.thinkmind.org/download.php?articleid=simul_2014_2_20_50030) (Xavier Rubio-Campillo).

- distributing agents
    - the distribution of agents is strongly dependent on the nature of the problem and properties of the system (degree of interaction b/w agents, complexity of behavior, etc), thus there is no universally optimal way to do so
- core component: the scheduler:
    - updates the agents and the environment
    - manages order of execution of agents
    - manages how agents interact with other components (other agents, environment, etc)
    - again, there is no optimal scheduling algorithm because of the heterogeneity of problems
- scheduling becomes especially hard when dealing with distributed simulations
    - agents need to gather knowledge from the surrounding environment & other agents
    - when agents take an action, they modify the environment
    - synchronization of these is tricky; there may be issues of accessing/modifying the same data at the same time (collisions)
- an agent's execution can be broken into three parts:
    - updating its knowledge - in this part, the agent only accesses information from the environment and other agents; it does not modify anything
    - selecting action - the agent engages its decision-making process to decide what action to do; again, it does not modify anything
    - taking the action/updating state - this is the only part where collisions may occur

---

<http://jasss.soc.surrey.ac.uk/11/4/10.html>

> Unfortunately, predicting the communication patterns within an ABM is at least as difficult as actually simulating the system. As a consequence, costly synchronization is inevitable (Som et al. 2000). To date, cluster based parallel computing has failed to deliver the requisite scalability. There is a point of diminishing return where adding more processors actually reduces performance because of communication overhead.

...

> Another solution that has been proposed for model scalability is agent compression (Wendell et al. 2007). The basic idea is to group similar agents into an aggregate agent that behaves as a single agent within the simulation. In static agent compression (Stage 1993), at the beginning of the simulation, each agent is a point in a multi-dimensional space of attributes. Agents are clustered into aggregate agents based on the values of the attributes. An aggregate agent's attributes represent the core of the cluster. An expansion factor is included to represent the number of agents. In dynamic agent compression (Wendell et al. 2007), an agent moves in and out of aggregate agents depending on how well it differentiates from other agents in the aggregate. The system itself contains a compression manager to compress and decompress agents, an agent container to represent aggregate agents, and individual agents. Agent compression works only in cases where model heterogeneity is even. Wendell et al. (Wendell et al. 2007) report that performance gain in computation time for a model containing a million individual agents is about 10 as compared to the uncompressed version.

---

<http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.111.9569&rep=rep1&type=pdf>

> Before  an  agent federate can move a tile it must obtain ownership of the tile’s position attribute.  Once the tile has been moved by this agent, the second agent’s move should become invalid, as the tile is no longer at the position at which the agent initially perceived it.  To ensure that attributes are mutually exclusive, we only allow transfer of ownership once per simulation cycle for any given attribute.  A federate will then only relinquish ownership of an attribute if it has not already been updated at the current cycle.

...

> The problem of detecting action conflicts is intractable in general, and it is up to  the simulation developer to design a SIMAGENT simulation so as to avoid conflicts.  One way to do this is to arrange for each action to check that its preconditions (i.e., the state the environment was in when the action was selected) still hold before performing the update and otherwise abort the action.  For example, one agent changing the position of a tile violates the precondition for any other action (by the same or another agent) which attempts to move the tile. However, this is not feasible in a distributed setting, since any attribute updates resulting from the actions of agents simulated by other federates are not propagated until the end of the cycle. We  therefore  extend  current  practice  in SIMAGENT and require that attribute updates be mutually exclusive.
> A mutually exclusive attribute is one which cannot be updated twice in the same cycle.  For example, we may require that the position of an object can only change once in  any  given  cycle.   This  extension  does  not  solve  the ramification problem, it simply provides some additional tools for a simulation developer to manage inconsistent updates.

good step-by-step in this paper too, section 4.5

---

see: ~/stuff/library/simulation/framework/Antelmi.pdf
for overviews on graph partitioning algorithms


---

from Simulation Level-of-Detail, Stephen Chenney

> Game developers frequently choose to ignore the motion of some out of view objects. For example, Joe Adzima recently described the AI for Midtown Madness, in which cars are simulated only within a sphere around the viewer and are reflected at the boundaries. No work is done for parts of the city beyond the sphere. These existing approaches are acceptable if nothing should ever happen far from the view to influence the game-play. Hence, while they work for games with local action, they are not applicable for games where events beyond the view may have a major impact on the outcome of the game, such as global strategy games. For example, it makes a difference if your out-of-view opponent can accumulate enough resources to launch an attack on your base. Some work must be done to ensure that the attack happens at all – if nothing is done for out-of-view motion then nothing new can ever enter the view by itself.

...

> The best way to think about motion and outcomes is in terms of _events_: the model says that certain things should happen in the world that are important to game-play, and any implementation must ensure that those things do happen. On the other hand, there is no need to be concerned with other events, which is where savings can be found. For example, as your opponent is gathering resources, it doesn't matter which paths their workers take, only that the workers gather a certain amount by a certain time, triggering the important attack event.

---

from Simulation Culling and Level-of-Detail, Stephen Chenney

> Simulation culling and level-of-detail techniques offer tools to reduce the resource cost of dynamic simulation in large environments. Culling algorithms [4] avoid computations for simulations that a  viewer cannot see, hence enabling truly scalable environments on a single machine. With effective culling, it is possible to experience an entire city simulated on one computer, as most of the motion is out of view and hence costs nothing. Level-of-detail methods [2, 5] aim to reduce the cost of dynamics when the system is far from the viewer , thus allowing for environments with large visible areas yet rich dynamic content. With effective simulation level-of-detail, a viewer could look out across a simulated crowd and see reasonable motion without the cost of accurate dynamics for everyone.

---

from Managing Simulation Level-of-Detail with the LOD Trader, Ben Sunshine-Hill

> Simulation LOD (SLOD) allows larger and more richly detailed worlds to be simulated with the available computing power, by using cheaper and simpler simulation techniques for less important entities. For example, a character in the same room as the viewer may use a high-quality planning algorithm to determine his actions, while a character at the other end of the city may simply follow a fixed schedule, or be frozen in place entirely.

...

> a SLOD system should optimize quality while placing guaranteed constraints on resource usage. LOD should never be reduced unless necessary to maintain performance; and when it does become necessary, perception-focused heuristics should be used to determine which entities to simplify and which to maintain at full accuracy.

---

from: Proxy Simulations for Efficient Dynamics, Stephen Chenney, Okan Arikan, D.A. Forsyth

"dynamics culling" is where systems that are outside of the "view" are ignored _completely_, when they re-enter the view, their states are updated with deterministic and statistical approximations to reflect the expected change in state while the system was out of view

particular _events_ may happen out-of-view that are important, e.g. _view entry_ events in which the non-visible object enters the viewing region, or other salient events like a car crash or enemy attack. these events should happen at a "reasonable" rate, and produce "reasonable" states (e.g. the particulars of the enemy attack should be reasonable), the specific definition of "reasonable" dependent on the simulation.


---

can do LOD like this:

- have users implement their own different "decide" methods and use a decorator to tag their level-of-detail (0 being max, and decreasing from then on)
- the user (or maybe it's just part of the framework) has some way of determining when to switch to what level of detail (e.g. criteria by which to decrease or increase it)
- user can also specify grouping criteria for agents (e.g. a function that, given two agents, returns true if they should be grouped together). but then we need to consider how an agent joins a larger group (e.g. do we check that this function returns true across all agents already in the group? or just over some certain threshold? etc)
- then the user can specify how a _group_ behaves. the group is sort of like a "big" agent, so it would just use the normal "decide" process (? there are probably cases where this wouldn't be so straightforward) and we compute a "group state", again defined by the user (e.g. maybe one variable takes the max of the agents in the group, or the mean, or the sum, etc)


refer to _Dynamic Level of Detail for Large Scale Agent-Based Urban Simulations_ for more details
