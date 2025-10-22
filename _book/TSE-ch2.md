<div id="part-ch2" class="chapter-title">
# A primer on time series models
</div>

## Starting point 

**Relation to the linear regression for cross-sectional datasets**. In standard econometrics or statistics courses, linear regression models are typically introduced using cross-sectional data. A key assumption for these models is the absence of autocorrelation in the error term. With time series data, however, autocorrelation is a fundamental characteristic and is almost always present.

- While linear regression can be applied to time series variables, the notation changes to reflect the temporal ordering. Variables are indexed by time, such as $y_t$ and $x_t$ (instead of $y_i$ and $x_i$ for cross-sectional observations).

We will return to multivariate regression models with time series variables later. First, we will explore **a pure time series approach** (as characterized by Verbeek, 2008).

- In this approach, the current value of a univariate time series, $y_t$, is modeled as a function of its past values, either directly or indirectly.

- The emphasis is therefore entirely on using the information contained in $y_t$ and its own history for modeling and forecasting purposes.


&nbsp;


## Notes on deterministic components

In time series analysis and models for such data, we often decompose a time series process $y_t$ into a deterministic and stochastic parts. This allows us to separate deterministic parts, like the mean and trend, from the random fluctuations that are the primary focus of stochastic models, such as in ARMA or VAR models to be introduced in this course.

The general decomposition and starting point in our notation throughout this material is given by:
\begin{equation*}
y_t = \mu_t + z_t,
\end{equation*}
where the components are defined as:

- $\mu_t$: This term represents the **deterministic part**.

- $z_t$: This is the **stochastic part**, representing (random) fluctuations around the deterministic component. A crucial assumption is that this process has a zero mean, i.e., $\mathsf{E}(z_t)=0$. Therefore, $z_t$ represents the demeaned and detrended time series process, which may, and typically, have its own autocorrelation structure and hence importantly $z_t$ is not just pure random noise.

By this construction, the expected value of $y_t$ is simply its deterministic component:
\begin{equation*}
\mathsf{E}(y_t) = \mathsf{E}(\mu_t + z_t) = \mu_t + \mathsf{E}(z_t) = \mu_t
\end{equation*}

&nbsp;

**Common forms of the deterministic component**. The functional form of $\mu_t$ depends on the underlying characteristics of the data and application in general. Two of the most common specifications are:

- **Constant mean**: If the time series fluctuates around a fixed, time-invariant level, the deterministic component is simply a constant
  \begin{equation*}  
    \mu_t = \mu.
  \end{equation*}
Here, $\mu$, or at times $\mu_0$, represents the unconditional mean of the process $\mathsf{E}(y_t)$. In general, almost all real-life time series have nonzero mean.

- **Constant and linear time trend**: If the series exhibits a persistent upward, or downward, movement over time, we also include a linear trend (together with the constant term). The deterministic component then includes both a constant and a time trend
  \begin{equation*}
    \mu_t = \mu_0 + \mu_1 t
  \end{equation*}
where $\mu_0$ is the constant (the value of $\mu_t$ at $t=0$), and $\mu_1$ is the trend coefficient, representing the average change in $y_t$ from one period to the next.

In practice, at times we first estimate the parameters of the deterministic part $\mu_t$, e.g., via Ordinary Least Squares, and then work with $z_t$ as a residual between $y_t - \mu_t$. This is the tactic as described in Section 1 in connection to simple detrending techniques. Alternatively, and more often, modelling deterministic and random components will be carried out simultaneously.

- In our notation, $x_t$, or $\boldsymbol{x}_t$ in the case of multiple time series, is used for a general time series process (for different notational purposes) and most often they are explanatory (predictive) variables.


&nbsp;
