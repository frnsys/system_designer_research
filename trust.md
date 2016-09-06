# Will, O. (2009). Resolving a replication that failed: news on the Macy & Sato model. Journal of Artificial Societies and Social Simulation, 12(4), 11.

<http://jasss.soc.surrey.ac.uk/12/4/11.html>


---

# Bravo, G., Squazzoni, F., & Boero, R. (2012). Trust and partner selection in social networks: An experimentally grounded model. Social Networks, 34(4), 481-492.

<http://www.academia.edu/download/30864283/TrustPartnerSelectionSocialNetworks.FSquazzoni2012.pdf>

---

# Chiang, Y. S. (2013). Cooperation could evolve in complex networks when activated conditionally on network characteristics. Journal of Artificial Societies and Social Simulation, 16(2), 6.

<http://jasss.soc.surrey.ac.uk/16/2/6.html>

- many network cooperation models assume that an agent uses the same behavior with each neighbor (e.g. if they choose to cooperate, they do so invariantly with all neighbors). This is unrealistic; people adopt different behaviors depending on who they're interacting with.
- one such variant method is _conditional cooperation_, e.g. cooperating with
    - genetic-related kin
    - members of the same group
    - strangers with reputation of being cooperative to
        - the focal player (direct reciprocity)
        - third others (indirect reciprocity)
    - strangers with distinct and recognizable biological or cultural marks

Each agent has some "nodal attribute"; for agent $i$ we denote this as $A_i$. This is what cooperation is conditioned on.

For example, the nodal attribute could be node degree, and an agent might only cooperate with neighbors that have a higher degree than theirs ($A_i - A_j < 0$).

Here agents are always aware of the network structure around them (to an extent) and can strategize accordingly:

>  Not only can individuals perceive social networks, but also they can use their understanding of it to achieve personal gains. For example, the structural-hole theory, proposed by economic sociologists, argues that people in the business domain would strategically occupy certain positions in networks, such as a bridge linking two otherwise disconnected communities, to grasp advantages in brokerage that would not be rendered by other positions (Burt 1995; Buskens and van de Rijt 2008). Similarly, the growing literature on social capital theory shows how individuals use their personal connections to access collective benefits, such as job-opening information, that would flow in social networks (Lin et al. 2001; Mouw 2006).

The model:

- $n$ agents
- each agent can decide whether to cooperate or defect with their neighbor
    - cooperation has a cost $c=1$ to deliver help valued at $b=5$ to a neighbor
    - the agent cooperates if $e_l < A_i - A_j \leq e_h$, where $e_l, e_h$ are upper and lower bounds representing a strategy in the game. For instance, $e_l = -\infty, e_h = \infty$ represents unconditional cooperation, and unconditional defection is $e_l > e_h$.

The nodal attributes used include:

- degree (node's connectedness)
- clustering coefficient (cohesiveness of connections in a node's local neighborhood)
- betweenness (assess a node's role in mediating traffic flow in networks)
- eigenvector centrality (also a node's role in mediating traffic flow in the network)

Since these nodal attributes are sensitive to network size, they are standardized:

$$
\begin{aligned}
A_i^* &= \frac{A_i - \bar A}{sd_A} \\
\bar A &= \frac{1}{n} \sum_{j=1}^n A_j \\
sd_A &= \sqrt{\frac{\sum_{j=1}^n (A_j - \bar A)^2}{n}}
\end{aligned}
$$

The authors experimented with a few different network structures.

---

# Eguíluz, V. M., Zimmermann, M. G., Cela‐Conde, C. J., & San Miguel, M. (2005). Cooperation and the emergence of role differentiation in the dynamics of social networks1. American journal of sociology, 110(4), 977-1008.

<http://arxiv.org/pdf/0712.1351>

> The question posed is..._to explore how social structure might evolve in tandem with the collective action it makes possible_.
...
> In this paper we address explicitly the problem of co-evolution [of cooperation and network topology] in a version of the Prisoner's Dilemma (PD) (Rapoport and Chammah 1965) in which players interact through a network that adapts to the results of the game, and therefore to the actions of the players.
...
> A main result of our analysis...is the _emergence_ of a process of social differentiation together with the building-up of a network with hierarchical relations. Starting from random partnership among equivalent individuals, a social structure emerges. In this emerging structure, the topology of the network of social relations identifies individuals with different social roles: leaders, conformists and exploiters.

Alternatively, the Social Evolution Model (SEM) (de Vos et al, 2001; Zeggelink et al, 2000) "leads to the formation of cohesive egalitarian clusters".

> We propose a simple model where the actions of individuals that form the social network are driven by their level of satisfaction, choosing their actions by imitation of their best neighbor. Moreover, we introduce _social plasticity_...as the capacity of the individuals to choose partners, being able to change their neighborhood as time goes on.

The model:

- $n$ agents
- random choice of strategies
- random network
- discrete time steps in three stages
    - each agent $i$ plays prisoner's dilemma with its neighbors, collecting an aggregate payoff $\Pi_i$
    - each agent updates its current strategy, imitating the strategy of the neighbor with the largest payoff including themselves (whenever more than one equivalent neighbor with a larger payoff exists, one of them is randomly selected);
    - if agent $i$ imitates a Defector, then agent $i$ replaces with probability $p$ this link with the imitated D-neighbor by a new one pointing to a randomly chosen partner from the whole network

Play is undirected so if agent $i$ plays agent $j$, $j$ is considered to have played with $i$ as well.

Agents are assumed to play the same strategy with all neighbors.

All strategies are zero-memory (agents dont consider past encounters).

Any targeted agent always accepts a new partner. When agents look for a new partner, they select one at random.

The plasticity parameter $p$ measures how easy it is both to sever a collaboration and find a new partner. For $p=0$, this means the cost is extremely large, for $p=1$, the cost is small. $p$ controls the rate at which the network structure evolves, if $p << 1$ then strategies change faster than network evolution (closer to $p=0$ means a frozen network), for $p=1$ strategies and network evolve at the same rate ("fluid" social network).

A _satisfied_ agent is one that does not imitate any other agent (i.e. they have the largest payoff in their neighborhood); otherwise, they are unsatisfied.

The network can be visualized as an _imitation network_ in which an edge is drawn from an imitator to who they are imitating.

From this, social differentiation emerges:

- leaders: satisfied cooperators
    - the "absolute leader" is the agent with the largest payoff in the whole network (i.e.t he "most" satisfied agent)
    - these tend to have many links
    - as the satisfied agent in their neighborhood, they influence other agents to adopt their strategy
- conformists: unsatisfied cooperators
    - they do not have the maximum payoff in their neighborhood but they imitate another agent with their same strategy
    - they constitute a majority of the nodes
- exploiters: defectors who take advantage of other's actions.
    - they have a larger payoff than their cooperative neighbors and are satisfied
    - they have no link in the imitation network because no agent imitates them

Alternative rules:

---

some thoughts:

- "trust" here is encoded as willingness to enter a prisoner's dilemma, also called "partner selection"
- peer influence may be too strong sometimes, e.g. perhaps someone by happenstance is around people they do not like and they don't necessarily become more like them...so for each individual perhaps there's a personal tolerance continuum about a particular behavior, which slows down the adoption of disapproved-of behaviors, but can be worn down by attribution/long-term exposure to them


---

from _Collective Action and Exchange: A Game-Theoretic Approach to Contemporary Political Economy_ (William Ferguson), pp78-79:

> Broadly speaking, there are two categories of strategic moves. _Unconditional strategic moves_ involve binding commitments to follow a strategy, such as driving straight in a game of chicken. _Conditional strategic moves_ are if-then statements (e.g. if you do $x$, then I will do $y$) that take the form of either threats or promises. ... A _credible_ move or statement...is one that others expect [the player] to adhere to at every point where she may be called upon to do so--even if the indicated action appears to undermine her interest at that point.

p81:

> Conditional strategic moves...take the form of two-part if-then statements: if you do $x$ then I will do $y$; if you do not do $x$, then I will not do $y$. There are two basic types of conditional strategic moves: (i) threats (e.g., if you misbehave ($x$), then I will punish you ($y$)) and (ii) promises (e.g., if you behave ($x$), then I will reward you ($y$)). Furthermore, each threat contains an implied promise: if you do behave, then I will not punish you: $\lnot x \to \lnot y$. Likewise, each promise contains an implied threat: if you behave badly ($\lnot x$), then no reward ($\lnot y$).
>
> Both parts of each statement...require credibility to be effective. _Primary credibility_ concerns the first part--the direct threat or promise ($x \to y$). Because executing threats or honoring promises is costly to the parties who issue them, recipients may not believe such statements. ... Thus establishing primary credibility requires some commitment of resources. By contrast, _secondary credibility_ (that pertaining to the second part--the implied statement $\lnot x \to \lnot y$ is usually automatic for the same reason...In some cases, however, a party must devote resources to establishing both primary and secondary credibility.

