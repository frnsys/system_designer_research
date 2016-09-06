Grazzini, Jakob (2012) 'Analysis of the Emergent Properties: Stationarity and Ergodicity' Journal of Artificial Societies and Social Simulation 15 (2) 7 <http://jasss.soc.surrey.ac.uk/15/2/7.html>. doi: 10.18564/jasss.1929

With simulated time series we will be interested in seeing the ergodicity and stationarity of statistical moments.

There are many tests for stationarity, many of which introduce assumptions about the stochastic data generation process to increase the power of the test (i.e. to decrease the amount of information necessary for it, i.e. to decrease the number of required observations). These assumptions imply that these tests are parametric. With simulation the test power is not a concern since the cost is virtually zero to produce more observations (just run the simulation again).

With simulations we can use the nonparametric test (therefore we don't introduce assumptions about the data generation process), a variant of the Wald-Wolfowitz test, also called the Runs Test. This tests the fitness of a function (i.e. how well it fits the time series). A 1 is assigned to observations that are above the fitted line and 0 to the observations that are below the fitted line. If a point fits exactly on the line, it is ignored.

Then we look at the sequences of 1s and 0s. Each continuous sequence of a value is a "run". For example, with the sequence `1,0,0,1,1,1,0` we have four runs: `[1],[0,0],[1,1,1],[0]`. We look at the number of runs, which is called the $U$-statistic. We notate the number of points above the fitted function as $m$ and the points below as $n$. The mean and variance of the $U$-statistic under the null hypothesis are:

$$
\begin{aligned}
E(U) &= \frac{2mn}{m+n} + 1 \\
\text{Var}(U) = \frac{4mn(2mn - m -n)}{(m+n)^2(m+n-1)}
\end{aligned}
$$

(the null hypothesis being that the moment is stationary)

As the number of observations goes towards infinity (i.e. $m$ and $n$ go towards infinity), the asymptotic null-distribution of $U$ is a normal distribution with an asymptotic mean and asymptotic variance.

The number of runs tells us about how randomly distributed these observations are around the fitted function.

We can use this test to check for the stationarity of a time series. We want to check if some statistical moment (e.g. the mean) is stationary; to do so we check if it is constant in time. So we compute the "overall moment" across the entire time series, then break the time series into $w$ windows (sub-time series) and compute moments ("window moments") for those.

Then we treat the overall moment as our fitted function and apply the Runs Test using the window moments as our "observations". (there are some good graphics in the paper that illustrate this)

In terms of time series length and window length, it's suggested to use a long time series and long window lengths (so that you can have many long windows). According to the paper's experiments, a window length of 1000 seems to work best (over a 100,000 sample time series).

The type-I error (incorrect rejection of a true null hypothesis/a false positive, i.e. saying the moment is not stationary when it is) here is ~5%.

The stationarity of each moment must be tested individually, since the stationarity of one does not necessarily imply the stationarity of another.

Whereas the stationarity test tells us if the model converges towards a statistical equilibrium state, the ergodicity test tells us whether such an equilibrium is unique.

> Supposing that we want to know the properties of a model with a given set of parameters, if the model is ergodic (and stationary) the properties can be analyzed by using just one long time series. If the model is non-ergodic it is necessary to analyze the properties over a set of time series produced by the same model with the same set of parameters but with different random seeds (that is with a different sequence of random numbers). It is even more important to take ergodicity into consideration if the model is compared with real data. If the data generator process is non-ergodic, the moments computed over real data cannot be used as a consistent estimation of the real moments, simply because they are just one realization of the data generator process, and the data generator process produces different results in different situations.
>
> A typical example of a stationary non-ergodic process is the constant series. Supposing for example that a process consists of the drawing of a number $y_1$ from a given probability distribution, and that the time series is $y_t = y_1$ for every $t$. The process is stationary and non-ergodic. __Any observation of a given realization of the process provides information only on that particular process and not on the data generator process.__

(emphasis mine)

The proposed way to test for ergodicity is to generate two samples from the model with different seeds and compare them using the Wald-Wolfowitz test/the Runs Test. Here we use the original variant which tests whether two samples come from the same population.

We take our two samples $\{x_t\}$ and $\{y_t\}$ (which must have the same length), supposed to come from continuous distributions $f(x)$ and $g(x)$, and join them (union) into a set $Z$. We arrange $Z$ in ascending order of magnitude. Then we create another set $V$ by the following process:

- $v_i = 0$ if $z_i \in {x_t}$
- $v_i = 1$ if $z_i \in {y_t}$

Then we apply the same idea of "runs" to $V$ with the $U$-statistic and so on. If the null hypothesis $f(x)=g(x)$ is true, the distribution of $U$ is independent of them both. If they are different, $U$ tends to decrease, so the null hypothesis is rejected if it is too low.

Like the with the stationarity test, this test is conducted for a particular moment.

Given that, prior to the time series' convergence, two samples may look very different (thus the test can incorrectly identify an ergodic process as non-ergodic), you will want to select samples from a region after the time series has converged to the long run mean.