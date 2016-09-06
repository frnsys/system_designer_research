# Epstein, J. (2013). Agent_zero : toward neurocognitive foundations for generative social science. Princeton, New Jersey: Princeton University Press.

## Outline of the model

For agent $i$ at time step $t$ we have the following components:

- emotional/affective, $V_i(t)$
- cognitive/deliberative, $P_i(t)$
- social/network

These aggregate (e.g. sum) into a _disposition_ $D_i(t)$.

The _solo disposition_ of an agent:

$$
D_i^{\text{solo}}(t) = V_i(t) + P_i(t)
$$

Social influence is the weighted sum of other agents' solo dispositions:

$$
\sum_{j \neq i} \omega_{ji} D_j^{\text{solo}}(t)
$$

Thus behavior is not directly contagious, but disposition is.

So the _total disposition_ of agent $i$:

$$
D_i^{\text{total}}(t) = D_i^{\text{solo}} + \sum_{j \neq i} \omega_{ji} D_j^{\text{solo}}(t)
$$

Agents have an action threshold $\tau_i \geq 0$.

If $D_i^{\text{total}}(t) > \tau_i$ then the action acts.

So we can additionally define _net disposition_ as:

$$
D_i^{\text{net}}(t) = D_i^{\text{total}}(t) - \tau_i
$$

For a binary action, we can summarize this as a (binary) _action rule_ $A_i$:

$$
A_i = H[\mathbb \omega_{ji} \cdot (\mathbb V_j + \mathbb P_j) - \tau_i]
$$

Where $H$ is the Heaviside unit step function.

p13 surveys extensions to this basic model.

## Conditioning

Conditioning causes agent's to learn new associations between stimuli.

The _Rescorla-Wagner_ model of conditioning is used here.

The difference equation (i.e. for discrete time steps):

$$
\begin{aligned}
v_{t+1} - v_t &= \alpha \beta (\lambda - v_t) \\
v_t &= \lambda [1- ( 1- \alpha \beta)^t]
\end{aligned}
$$

The differential equation (i.e. for continuous time):

$$
\begin{aligned}
\frac{dv}{dt} &= \alpha \beta (t-v) \\
v(t) &= \lambda (1 - e^{- \alpha \beta t})
\end{aligned}
$$

Using the notation for the discrete time case here.

$v_t$ is the _associative strength_ of an unconditioned stimulus (US) and a conditioned stimulus (CS) at trial (pairing) $t$. That is, it's the extent to which the conditioned stimulus elicits the unconditioned response.

$\lambda$ is the maximum associative strength, i.e. $v_{\text{max}}$. $\lim_{t \to \infty} v_t = \lambda$.

We can think of $\lambda - v_t$ as "surprise".

$\alpha, \beta \geq 0$ are the salience of the CS and the salience of the US respectively; they can be thought of as learning rates.

There are two phases to conditioning:

1. acquisition
2. extinction

For extension, we use these same equations but set $\lambda=0$ and $v_0$ to the original (learned) associative strength.