# Epstein, J. M. (2001). Learning to be thoughtless: Social norms and individual computation. Computational economics, 18(1), 9-24.

<http://www.brookings.edu/~/media/files/rc/reports/1999/09fixtopicname_epstein/thoughtless.pdf>

Social norms have two components:

- their development, spread, adoption
- how they are used without thinking

Many models examine the development, spread, and adoption of norms but not how they come to replace deliberate thought in individuals.

The model detailed here captures both these components - agents learn what norm to adopt _and_ how much to think about how to behave.

- agents update their norms by observing agents within some sampling radius (which varies across agents). This radius could literally be around the agent or it could refer to agent neighbors in a network
- agents update their sampling radius $r$ with the following rule:
    - they observe the norms adopted by agents within their sampling radius, computing the relative frequency of each norm, $F(r)$
    - then they make the same observation at sampling radius $r+1$, i.e. they compute $F(r+1)$
    - if $F(r) \neq F(r+1)$ (within some tolerance), increase the search radius to $r+1$
    - otherwise, compute $F(r-1)$. If $F(r) = F(r-1)$, reduce the search radius to $r-1$
    - otherwise, keep the same search radius $r$
- the norm update rule then is to simply match the majority norm within the search radius

This approach is called _Best Reply to Adaptive Sample Evidence_.

There's additionally some noise (agents with some probability adopt a random norm).

---

# Buskens, V., Corten, R., & Weesie, J. (2008). Consent or conflict: Coevolution of coordination and networks. Journal of Peace Research, 45(2), 205-222.

<http://www.rug.nl/research/portal/files/2705303/BuskensV-Consent-2008.pdf>

"polarization": "the social or ideological separation of a society into two or more groups"

> The extent to which a society will polarize into possibly opposing camps is likely to be influenced by the patterns of social relations through which members of the society influence each other, and through which opinions, behaviors, and ideologies diffuse.

This paper examines "the interplay between polarization of behavior and social structure." In particular, coordination over a dynamic social network:

> How do the polarization and efficiency of the emerging distribution of behavior depend on the initial distribution of behavior, the initial network, the tie costs, and the payoffs in the coordination games?

Measure of polarization: _index for qulitative variation_ (IQV). For a binary norm Y:

$$
IQV = p(Y)(1 - p(Y))
$$

where $p(Y)$ is the proportion of the population choosing $Y$.

The model:

- actors organized in a network of $n$ actors with an $n \times n$ adjacency matrix representing the social network
    - relationships are undirected
- actors choose 0 or 1 for a binary behavior
- there is a payoff that depends on their chosen behavior and the behaviors of the actors they are connected to
    - their behavior does not vary with each connected actor
- connections have a cost to form and maintain
    - connections have an increasing marginal cost, so the more connections you have, the more "effort" is required for another
    - total cost of $t$ connections: $k(t) = \alpha t + \beta t^2$, where $\alpha > 0, \beta \geq 0$. If $\beta = 0$, connection costs are linear (no increasing marginal costs)
    - connections can be created only with the consent of both actors ("two-sided link formation process")
    - their deletion is free and can happen unilaterally

The payoff is determined by a simple coordination (Prisoner's Dilemma) game:

|   | 0    | 1    |
| 0 | a, a | c, b |
| 1 | b, c | d, d |

Such that $b < c < a < d$.

Two variants:

- $(a-b)<(d-c)$, "choosing $Y$ not only can lead to efficient payoff $d$ but is also less risky because the expected payoff from playing $Y$ is relatively high if you do not know what others will do"
- $(a-b)>(d-c)$, "choosing $Y$ is the risky choice because the expected payoff from playing $Y$ is relatively low if you do not know what others will do.

Main findings:
> It turns out that the initial network structure might affect the emerging distribution of behavior. The most important result with respect to polarization is that dense networks lead to more homogeneous behavior, while more segmented and segregated networks have the opposite effect. The latter effect becomes especially important if the initial behavior is already polarized. If polarized societies are indeed more prone to end up in conflicts, conflicts are less likely in dense cohesive societies, while conflicts are more likely in segregated and segmented societies, especially if the initial attitudes in sensitive issues are correlated with initial groups in social networks. The effect of centralization is multifold: centralization of the initial network increases the probability that all actors behave in the same way, but if this is not the case, centralization slightly promotes the extent of polarization.

These papers explores something similar, using very similar if not identical models:

- Goyal, S., & Vega-Redondo, F. (2005). Network formation and social coordination. Games and Economic Behavior, 50(2), 178-207.
    - <http://www.sfs.uni-tuebingen.de/~Roland/Literature/Goyal(05)_network_formation_and_social_coordination.pdf>
- Corten, R., & Buskens, V. (2010). Co-evolution of conventions and networks: An experimental study. Social Networks, 32(1), 4-15.
    - <https://pure.rug.nl/ws/files/14665291/2010-CortenR-CoEvolution.pdf>