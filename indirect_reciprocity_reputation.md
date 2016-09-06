# Janssen, M. (2006). Evolution of cooperation when feedback to reputation scores is voluntary. Journal of Artificial Societies and Social Simulation, 9(1).

<http://jasss.soc.surrey.ac.uk/9/1/17.html>

(models worth looking more into are tagged with "LOOK INTO")

Model:

- population of $n$ players
- they uniformly randomly play one-shot prisoner's dilemma games
- agents can cooperate, defect, or withdraw (not play)
- after a game, agents receive feedback of +1, 0, or -1
    - feedback is voluntary (it has a cost), not all agents may provide feedback
    - with probability $p_D$ an agent gives (negative) feedback when the opponent defected
    - with probability $p_C$ an agent gives (positive) feedback when the opponent cooperated
- each agent has a reputation score that is the sum of their feedback

They also use "symbols" (each agent has $s$ such symbols, in addition to reputation), ranging from 0 to 1, which is computed such that some relation exists between these symbols and the strategies of the agents. That way agents can use these symbols to infer trustworthiness.

There's a bit more to it, detailed in the paper, but this is the core of it.

---

# Pinyol, I., & Sabater-Mir, J. (2013). Computational trust and reputation models for open multi-agent systems: a review. Artificial Intelligence Review, 40(1), 1-25.

<http://www.iiia.csic.es/~jsabater/Publications/2013-AIRb.pdf>

Categorization of reputation models:

- Sabater et al:
    - Paradigm
        - cognitive (trust/reputation is built on beliefs and their degrees)
        - numerical (use game theoretical approaches that do not explicitly represent cognitive attitudes to describe trust and reputation)
    - Information sources
        - Direct experiences (direct interactions or direct observations)
        - Witness information (information gathered from other agents)
        - Sociological information (analysis of social relations among the agents)
        - Prejudice (an info source that allows bootstrapping of trust and reputation when no other information is available; similarly, stereotyping)
    - Visibility: is reputation a global property that all agents can observe or is it a private and subjective property that each agent builds themselves
    - Granularity: are there multiple contexts of reputation (e.g. buying/selling vs taking care of kids) or just one
    - Cheating Behavior
        - Level 0: cheaters are not considered (all agents honestly give information or only send false information by mitsake)
        - Level 1: agents can hide or bias communicated information, but never lie
        - Level 2: cheating is considered
    - Type of exchanged information (boolean vs continuous)
- Balke et al (several parts of this scheme are not clear at all):
    - focused on five stage processes
    - Stage 1: Recording of cooperative behavior: multi-context vs single-context
    - Stage 2: Rating of cooperative behavior:
        - mathematical: "pure game theoretical approaches where trust/reputation is considered as a subjective probability" (look at one final aggregate value)
        - cognitive: "more congitive approaches where a new rate affects the mental state of the agent" (may compute a final aggregate but also considers intermediate results)
    - Stage 3: Storage of cooperative behavior: centralized or distributed (per-agent)
    - Stage 4: Recall of cooperative behavior:
        - trust (witness information)
        - reputation (exchange of information)
    - Stage 5: Learning/adaptation strategy

Centralized models:

- Online reputation models (e.g. eBay-like models)
    - simple, easy to understand
    - shortcoming: "they lack in robustness; no reliability measures, no consideration of false information or cheating, no temporal issues. For instance, feedbacks remain countable forever. So, a seller with very high reputation value could start acting as a bad seller without having an immediate effect on its reputation value."
- Sporas and Histos
    - extension of the online reputation model
    - except that only recent feedback is considered
    - and reputation is not just a sum of feedbacks; the aggregation of feedbacks is instead designed to produce small changes for users with very high reputation and bigger changes for users with lower reputation
    - a reliability measure for user's reputation is also included
- Carter et al (LOOK INTO)
    - defines reputation of an agent as "the degree of fulfillments of roles ascribed to it by the society"
    - more concretely: "the reputation of each participant is the result of a weighted aggregation of the fulfillments achieved by the agent on each role"
- Dirichlet reputation systems
    - used where an agent's ratings are based on a discrete and finite sorted set, e.g. `[very bad, bad, neutral good, very good]`
    - an agent's reputation then is the probability distribution describing the probability an agent will act in one of these ways
    - thus involves approximating a Dirichlet distribution from agents' past behavior

Agent-oriented approaches (subjective/distributed):

- Abdul-Rahman and Hailes
    - trust is modeled as a discrete set of `[very trustworthy, trustworthy, untrustworthy, very untrustworthy]`
    - agents learn from direct experience and third party communication of direct experiences
    - for each agent and context the system keeps a tuple with the number of past own experiences or communicated experiences in each category
        - trust is computed by taking the maximum tuple (i.e. the most frequent trust value)
        - for ties between `very trustworthy` and `trustworthy` the system gives `mostly trustworthy`
        - for ties between `very untrustworthy` and `untrustworthy` the system gives `mostly untrustworthy`
        - for other ties, it returns `neutral`
- AFRAS (LOOK INTO)
    - uses fuzzy sets to represent reputation values
    - the old reputation value an agent has for another agent is updated through a weighted aggregation; the weight controls how much the agent weighs the latest interaction or the old reputation value
    - a wide fuzzy set indicates a high level of uncertainty, a narrow one implies more reliability
    - recommendations are also sent by other agents
        - the level of reliability of this witness information depends on the reputation of the senders
        - such that recommendations from a very highly-reputed sender could have the same weight as direct interactions
- Castelfranchi & Falcone
    - let $i, j$ be two agents
    - the cognitive components that make $i$ trust $j$ regarding the goal $g$:
        - goal seeking: $i$ has the goal $g$
        - competence belief: $i$ believes that $j$ is capable of obtaining $g$ from a set of actions (summarized in the action $\alpha$)
        - disposition belief: $i$ believes that $j$ will actually perform $\alpha$ to obtain $g$. This belief makes agents predictable
        - dependence belief: $i$ believes that they need/depend on $j$ to perform the task
    - the "core trust" is formed by the competence and disposition beliefs along with the goal
    - the ability and willingness of agent $j$ to achieve $g$ is also modeled
- ForTrust (LOOK INTO)
    - a cognitive model to differentiate "occurrent" from "dispositional" trust
        - occurrent trust: the trust on other agents to act here and now (similar to "core trust" as defined above)
            - defined as $OccTrust(i, j, \alpha, \phi)$ (agent $i$ trusts $j$ here and now to perform action $\alpha$ to obtain goal $\phi$).
            - like Castelfranchi & Falcone, builds on the following components:
                - $OccGoal_i(\phi)$ (occurrent goal)
                - $Belief_i(OccCap(j, \alpha))$ (occurrent capability belief)
                - $Belief_i(OccPower(j, \alpha, \phi))$ (occurrent power belief)
                - $Belief_i(OccIntends(j, \alpha))$ (occurrent intention belief)
        - dispositional trust: the disposition of the trustee to perform an action in order to obtain a potential goal when some conditions hold
            - defined similarly to occurrent trust (i.e. as $DispTrust(i, j, \alpha, \phi)$, with components:
                - $PotGoal_i(\phi)$ (potential goal)
                - $Belief_i(CondCap(j, \alpha))$ (conditional capability belief)
                - $Belief_i(CondPower(j, \alpha, \phi))$ (conditional power belief)
                - $Belief_i(CondIntends(j, \alpha))$ (conditional intention belief)
                - describes under which conditions agent $i$ believes that $j$ has the capability to execute $\alpha$, the power to achieve $\phi$ from $\alpha$, and the intention to perform $\alpha$
        - the "potential goal" refers to a goal that is not currently the case but at some point could be occurrent; this occurrent trust implies dispositional trust, but not the opposite
        - reputation is defined as $Rep(G, j, \alpha, \phi)$ where $G$ is a group of agents, and its components are:
            - $PotGoal_G(\phi)$
            - $GroupBelief_G(CondCap(j, \alpha))$
            - $GroupBelief_G(CondPower(j, \alpha, \phi))$
            - $GroupBelief_G(CondIntends(j, \alpha))$
            - note that group belief is defined as follows. For a group $G$, a belief $\phi$, and agents $i,j$ that belong to $G$: $GroupBel_{G\phi} = Bel_i(GroupBel_{G\phi}) \land Bel_i(Bel_j(GroupBel_{G\phi}))$; that is, each member of $G$ believes that the group has a group belief $\phi$ and believes that other members believe that the group has this group belief as well. It _does not_ imply that $Bel_{i\phi}$, that is, it does not imply that $i$ has the belief $\phi$.
- ReGreT (LOOK INTO)
    - uses:
        - direct experiences
        - third party information
        - social structures
    - trust is calculated only through direct experiences and reputation
    - reputation uses third party information, social network analysis, system reputation, and prejudices (to infer reputation values of unknown agents from their belonging group)
    - incorporates a credibility module to evaluate the truthfulness of witness information (takes into account the reputation and trust of the information provider)
    - provides reliability measures for trust, reputation, and credibility values
    - context is taken into account too: the trust of agent $a$ on $b$ towards a certain context $\phi$ is described $T_{a \to b\phi}$ (this context could be, for example, the desires or goals of the agent)
- FIRE
    - builds on Regret by incorporating a "certified reputation", which "are ratings presented by the rated agent about itself which have been obtained from its partners in past interactions" (sort of like recommendation letters or references)
    - uses role-based trust, similar to the context ontology of Regret
- Marsh
    - three kinds of trust:
        - basic trust, $T_x^t$, representing the trust disposition of agent $x$ at time $t$
        - general trust, $T_x(y)^t$, the general trust agent $x$ has on agent $y$ at time $t$ without specifying any situation
        - situational trust: $T_x(y, \alpha)^t$, the trust agent $x$ has on agent $y$ at time $t$ for a particular situation $\alpha$, computed: $T_x(y, \alpha)^t = U_x(\alpha)^t I_x(\alpha)^t \bar{T_x(y)^t}$, where $U_x(\alpha)^t$ is the utility agent $x$ gains from situation $\alpha$, $I_x(\alpha)^t$ is the importance for agent $x$ in situation $\alpha$, and $\bar{T_x(y)^t}$ is the estimatin of general trust after taking into account all information related to $T_x(y)^t$ (which can be calculated via the mean, max, or min of all past experiences)
- Mui et al
    - assumes each interaction is an independent Bernoulli experiment
    - defines a random variable as the sum of the Bernoulli distributions whose expectation is exactly the average
    - estimates lower and upper bounds using Chernoff bounds for the probability of success in the next trial
- Repage
    - distinguishes _image_ and _reputation_
        - _image_ is the belief a particular agent has about another target agent with respect to a certain context (role)
        - _reputation_ is the belief about how _others_ perceive the target agent
        - for example, agent $A$ may personally believe that agent $B$ is a good driver (image) but also recognize that everyone else thinks that $B$ is a terrible driver (reputation)
- BDI + Repage (LOOK INTO)
    - expands on Repage with a BDI (Belief-Desire-Intention) architecture
    - different contexts for belief, desire, intention, the Repage model, and two functional contexts (communication and planner)
        - Belief context: the believed knowledge of the agent, using probabilistic dynamic belief logic in which formulas like $(B_i[\alpha]\phi, p)$ indicate that agent $i$ believes that after the execution of action $\alpha$, the probability that formula $\phi$ holds is $p$
        - Desire context: a logic of prefences based on Lukasiewicz logic, i.e. the desires of the agent have the form $(D_i^+ \phi, d)$ and $D_i^- \phi, d)$, with $d \in [0, 1] \cap Q$, meaning the agent $i$ will have a level of satisfaction (the former) or disgust (the latter) $d$ if $\phi$ holds
        - Intention context: holds formulas like $(I_i \phi, d)$ where $d \in [0,1] \cap Q$, determining the trade-off between positive and negative countereffects of trying to achieve $\phi$
        - (note the paper has a strange character that looks like a misprinted $Q$ and doesn't clarify what it means, so I've just used $Q$)

---

# Wierzbicki, A., & Nielek, R. (2011). Fairness emergence in reputation systems. Journal of Artificial Societies and Social Simulation, 14(1), 3.

<http://jasss.soc.surrey.ac.uk/14/1/3.html>

Hypothesis: "in reputation (or trust management) systems, fairness should be an emergent property."

Fairness:

- _distributive fairness_: "usually related to the question of distribution of some goods, resources or costs...The goal of distributive fairness is to find a distribution of goods that is perceived as fair by concerned agents."
- _procedural fairness_: "focuses on the perceived fairness of procedures leading to outcomes"
- _retributive fairness_: "concerned with rule violation and the severity of sanctions for norm-breaking behavior."

Distributive fairness can be thought of as a special case of procedural fairness.

In the paper, the following general definition of fairness is used:

> _Fairness means the satisfaction of justified expectations of agents that participate in the system, according to rules that apply in a specific context based on reason and precedent._

and the primary focus is distributive fairness.

In a fair distribution problem we need to consider the outcomes of all agents. The "efficient optimization problem" has to do with optimizing the outcomes of all agents, but does not have to consider fairness. The result is an outcome vector $y=[y_1, \dots, y_n]$, where $y_i$ is the outcome for agent $i$.

We can compute the utilities of these outcomes with either an objective criteria (the same across all agents) or subjective criteria (varies across agents).

The assumption here is that all agents are equally entitled to/capable of good outcomes. There are schemes around this, e.g. dividing the outcome of each agent by that agent's contribution (to model varying entitlement).

(the paper goes on to specify how they measure fairness so they can determine if in fact fairness has emerged in their simulations)

The model itself doesn't seem too interesting


---

# Hauert, C., Traulsen, A., Brandt, H., Nowak, M. A., & Sigmund, K. (2007). Via freedom to coercion: the emergence of costly punishment. science, 316(5833), 1905-1907.

<http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2430058/>

> An impressive body of evidence shows that many humans are willing to pay a personal cost in order to punish wrong-doers (1–8). In particular, punishment is an effective mechanism to ensure cooperation in public goods interactions (9–11). All human populations seem willing to use costly punishment to varying degrees, and their willingness to punish correlates with the propensity for altruistic contributions (12). ...This raises a ’second order social dilemma’: costly punishment seems to be an altruistic act, since individuals who contribute, but do not punish, are better off than the punishers.
>
> The emergence of costly punishing behaviour is acknowledged to be a major puzzle in the evolution of cooperation. ”We seem to have replaced the problem of explaining cooperation with that of explaining altruistic punishment” (13).

The model:

- population of size $M$
- members live on a fixed income $\sigma$
- $N$ individuals are randomly selected and can optionally participate in a risky but possibly profitable public goods game
    - those who participate can decide to contribute an investment at cost $c$ to themselves
    - all individual contributions are added up and multiplied by a factor $r > 1$
    - the result is divided equally amongst all participants in the public good game
- each contributor can then impose a fine $\beta$ on each defector, at a personal cost $\gamma$ for each fine
- there are $x$ cooperators, $y$ defectors, $z$ non-participants, and $w$ punishers
- each non-participant receives a constant payoff $\sigma$
- the participants for the game are randomly selected: $N_x$ cooperators, $N_y$ defectors, and $N_w$ punishers. The game size is $S= N_x + N_y + N_w$, if $S>1$, each participant of the game obtains an income $r(N_x+N_w)c/S$ (this is just a formalization of the investment game described above). Otherwise, the game does not take place.
- the payoff for defectors is reduced by $\beta N_w$ and the payoff for punishers by $\gamma N_y$.
- $\sigma$ is restrained to $0 < \sigma <(r-1)c$

Strategies propagate through the game like so: players imitate each other; they are more likely to imitate those with a higher payoff. With some small probability $\mu$ a player may "mutate" and switch to another strategy irrespective of its payoff.

---

thoughts:

- each agent has a public (noisy, observable by others) and private state
- other agents use this public state as a feature vector, for example, to learn logistic regression models over who they can and can't trust
- it's better if reputation is not deterministic/doesn't use a hard threshold, but is stochastic (e.g. this reputation value represents my belief that they'll cheat me rather than some rule, e.g. if their reputation is over $T$ I'll always trust them)