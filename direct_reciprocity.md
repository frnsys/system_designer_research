# Back, I., & Flache, A. (2006). The viability of cooperation based on interpersonal commitment. Journal of Artificial Societies and Social Simulation, 9(1).

<http://jasss.soc.surrey.ac.uk/9/1/12.html>

> The most prominent explanation of endogenous cooperation in durable relationships is reciprocity under a sufficiently long "shadow of the future" (Axelrod, 1984; Friedman, 1971). In this view, actors engage in costly cooperation because they expect future reciprocation of their investment or because they feel threatened by future sanctions for non-cooperation (Falk et al., 2001; Fehr and Gächter, 2002; Fehr and Schmidt, 1999).

> recent empirical studies of cooperative behavior, in particular in interpersonal relationships, indicate that often reciprocity may be much less strict and actors much less intent on keeping the books balanced than the original reciprocity argument suggests. A short excerpt from Nesse (2001) offers good examples:
>
> > Perhaps the strongest evidence that friendships are based on commitment and not reciprocity is the revulsion people feel on discovering that an apparent friend is calculating the benefits of acting in one way or another. People intuitively recognize that such calculators are not friends at all, but exchangers of favors at best, and devious exploiters at worst. Abundant evidence confirms this observation. Mills has shown that when friends engage in prompt reciprocation, this does not strengthen but rather weakens the relationship (Mills and Clark, 1982). Similarly, favors between friends do not create obligations for reciprocation because friends are expected to help each other for emotional, not instrumental reasons (Mills and Clark, 1994). Other researchers have found that people comply more with a request from a friend than from a stranger, but doing a favor prior to the request increases cooperation more in a stranger than a friend (Boster et al., 1995).
> Moreover, there is solid empirical evidence indicating that people have a tendency to build long-term cooperative relationships based on largely unconditional cooperation, and are inclined to hold on to them even in situations where this does not appear to be in line with their narrow self-interest (see e.g. Wieselquist et al., 1999). Experiments with exchange situations (Lawler and Yoon, 1996,1993; Kollock, 1994) point to ongoing exchanges with the same partner even if more valuable (or less costly) alternatives are available. This commitment also implies forgiveness and gift-giving without any explicit demand for reciprocation (Lawler, 2001; Lawler and Yoon, 1993). One example is that people help friends and acquaintances in trouble, apparently without calculating present costs and future benefits. Another, extreme example is the battered woman who stays with her husband (Rusbult et al., 1998; Rusbult and Martz, 1995).

The model:

Based on a "delayed exchange dilemma game".
Played by $n$ agents in successive rounds.
First round: all agents are given $f_i$ fitness points.
Each round, "Nature" selects a number of agents with a given individually independent probability $P_d$ who experience distress and need other agents to help preserve their fitness level. They ask others for help. Providing help costs $f_h$ fitness points, and each agent can help only one other agent, and only non-distressed agents can help. If help is refused, the agent can ask up to a total of $m$ agents altogether for help. If the agent does not receive help, at the end of the round if loses $f_d$ fitness. If it falls below $f_c$, it "dies".

Agents decide whether to help based on utilities (which includes emotional utility), available information, and in a bounded-rational way (myopic, considering only the subsequent state of the world).

Agents remember who helped them and who didn't, who they helped and who didn't, and how often. For an agent $i$ and another agent $j$, from the perspective of $i$, these values are $AH_{ij}, AR_{ij}, EH_{ij}, ER_{ij}$ respectively.

The _utility of donating_ $U_{ij}^D$ that agent $i$ gains from helping agent $j$ is:

$$
U_{ij}^D = U_m^D + eh_i^D EH_{ij} + er_i^D ER_{ij} + ah_i^D AH_{ij} + ar_i^D AR_{ij}
$$

where:

- $U_m^D$ is the materialistic costs of interaction
- $eh_i^D, er_i^D, ah_i^D, ar_i^D$ are agent-specific parameters (traits) for donation of agent $i$

There's an additional probability $P_e$ that the agent will make a random decision, to model noise in communication or miscalculation by the agent.

The _utility of seeking_ $U_{ij}^S$ is similar:

$$
U_{ij}^S = U_m^S + eh_i^S EH_{ij} + er_i^S ER_{ij} + ah_i^S AH_{ij} + ar_i^S AR_{ij}
$$

When choosing who to help, the agent chooses the partner with the highest utility, if that utility is above an agent-specific threshold $U_i^t$. For ties, a random agent is chosen.

If an agent $i$ is asked to donate to an agent $j$ with no prior interaction, $i$ assumes that $AH_{ij}=1$ (i.e. assumes one good interaction). Suspicious strategies can be defined by choosing a utility threshold $U^t$ to be high enough that without any prior action the utility of seeking or donation is lower than this threshold.

When choosing who to task for help, agents also choose the partner with the highest utility but there is no required threshold.

A strategy $S$ can be described by the eight agent-specific parameters and the utility threshold. Ranges of these parameters can correspond to personality types, e.g. "commitment":

$$
ah^D, ah^S > 0; er, ar = 0
$$

If $U^t$ is zero or negative and $ah^D > U^t$, the agent starts by cooperating if able to. Otherwise it behaves as "suspicious commitment".

Other strategies are enumerated in the paper.

The population then evolves via replicator dynamics (i.e. in subsequent generations, each strategy is represented proportionally to its success in the previous generation).

To keep population constant, when an agent dies, a new agent is created of strategy $S$ with probability equal to the proportion of collective fitness held by agents of that strategy.

The results are worth looking through too