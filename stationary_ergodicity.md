A _stationary_ process (time-series):

- $E[X_t] = \mu$; the expected value is invariant to time, i.e. $\mu$ is not a function of time
- $\text{Var}(X_t) = \sigma^2$; the variance is also not a function of time
- $\text{Cov}(X_t, X_{t+h}) = f(h)$; that is the covariance of between two times is also not a function of time

That is, the data generating process that produces $X_t$ is the same across all time steps.

An _ergodic_ process (time-series):

- a "sizable"/"sufficiently long" sample is statistically representative of the whole
- different initial conditions have asymptotically convergent properties (the process will eventually "forget" the past)

> A typical example of a stationary non-ergodic process is the constant series. Supposing for example that a process consists of the drawing of a number $y_1$ from a given probability distribution, and that the time series is $y_t = y_1$ for every $t$. The process is stationary and non-ergodic. Any observation of a given realization of the process provides information only on that particular process and not on the data generator process.

from: Grazzini, Jakob (2012) 'Analysis of the Emergent Properties: Stationarity and Ergodicity' Journal of Artificial Societies and Social Simulation 15 (2) 7 <http://jasss.soc.surrey.ac.uk/15/2/7.html>. doi: 10.18564/jasss.1929