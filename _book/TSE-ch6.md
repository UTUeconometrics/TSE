<div id="part-ch6" class="chapter-title">
# Parameter estimation
</div>

In this section, we will consider the estimation of ARMA($p,q$) model (or ARIMA($p,d,q$) model when introducing it in the latter Sections). In a nutshell, we observe the estimation to be possible with different methods depending on the model at hand:

- In the case of an AR($p$) model estimation can be done by (conditional) ordinary least squares (OLS).
    
- In the case of ARMA($p,q$) models, due to the MA($q$) part, estimation is more complicated. However, estimation can be carried out by the method of maximum likelihood, which is naturally also available for the AR($p$) model as well.


## Estimation of AR models with conditional OLS

Estimation of the AR($p$) model can be carried out with ordinary least squares (OLS), conditioning on the first $p$ observations. The AR($p$) model (including constant term) can be rewritten as
\begin{equation*}
y_t= \boldsymbol{x}^{\prime}_t \boldsymbol{\beta} + u_t,
\end{equation*}
where $\boldsymbol{x}_t=[1 \quad y_{t-1} \, \cdots \, y_{t-p}]^{\prime}$ and $\boldsymbol{\beta}=[\nu \quad \phi_1 \, \cdots \, \phi_p]^{\prime}$. The OLS estimators of $\boldsymbol{\beta}$ (and $\sigma^2$) can be constructed in the usual way familiar from past studies related to linear regression models. That is, the conditional OLS estimator of $\boldsymbol{\beta}$ is
\begin{equation*}
\widehat{\boldsymbol{\beta}} = \Big(\sum_{t=1}^T \boldsymbol{x}_t \boldsymbol{x}^{\prime}_t \Big)^{-1} \sum_{t=1}^T \boldsymbol{x}_t y_t.
\end{equation*}
In this case (notation), it is assumed that the required $p$ initial values $y_{-p+1},\ldots, y_0$ are available. 

- Notice that the summation in the OLS estimator starts from $t=1,2,\ldots$ due to these available initial values. Depending on, mainly notational choices, alternatively the OLS estimator is at times written as
\begin{equation*}
\widehat{\boldsymbol{\beta}} = \Big(\sum_{t=p+1}^T \boldsymbol{x}_t \boldsymbol{x}^{\prime}_t \Big)^{-1} \sum_{t=p+1}^T \boldsymbol{x}_t y_t,
\end{equation*}
if treating observations $y_1,\ldots, y_p$ as initial values.

The usual (asymptotic) statistical properties of the resulting OLS estimator hold. In particular, it can be shown that:

- As the error term $u_t$ is uncorrelated with the lags of $y_t$, we have $\mathsf{E}(\boldsymbol{x}_t u_t)=\mathbf{0}$ (that is, $\mathsf{E}(u_t (y_{t-j}-\mu)) = 0$ for $j=1,2,\ldots,p$), and the OLS estimator $\widehat{\boldsymbol{\beta}}$ is a consistent estimator of $\boldsymbol{\beta}$.

- Heteroskedasticity-autocorrelation consistent (HAC) standard errors, such as Newey-West standard errors, can, and often should, be automatically used to take the potential remaining conditional heteroskedasticity and autocorrelation in the residuals into account for detailed statistical inference (if this is the main objective in empirical analysis).

&nbsp;

## Maximum likelihood estimation

Estimation of ARMA (ARIMA) models with a moving average component is somewhat more complicated than the OLS based estimation of autoregressive models. The essential problem in estimating these models stems from the fact that $u_t$ is not observable. 

The estimation of an ARMA($p,q$) model, including also the AR($p$), can be based on (conditional) method of maximum likelihood by making an assumption of the distribution of the error $u_t$. A typical case would be to assume the error term is Gaussian $u_t\sim \mathsf{nid}(0,\sigma^2)$. 

- It is worth noting that regardless of the errors being exactly Gaussian or not, the maximum likelihood estimator (MLE) can be interpreted as a **quasi-MLE (QMLE)** where the possible error in the model specification can be taken into consideration by using a robust parameter covariance matrix in formulation of the standard errors.

- We will come back to this QMLE interpretation within the context of AR-GARCH model. Similar argumentation as there can be used also in this context (without the GARCH errors).

&nbsp;

We will next consider details on so called conditional maximum likelihood technique. The exact method (exact method of maximum likelihood) will be introduced at the end of next section in Extra material.

&nbsp;

**Conditional maximum likelihood method**. The (exact) ML estimation of ARMA models requires the necessary selections for the initial values of $y_t$ and $u_t$. By conditioning to the initial values, we get the conditional maximum likelihood technique. If the sample size (length of the time series) is large, the conditional and exact MLEs are close to each other (both lead to the same asymptotic distributions). Moreover, in practice, numerical methods can be used to maximize the log-likelihood function in both cases.

&nbsp;

Let us consider a concrete example case of an ARMA(1,1) model
\begin{equation*}
y_t = \nu + \phi_1 y_{t-1} + u_t + \theta_1 u_{t-1},
\end{equation*}
where $u_t \thicksim \mathsf{nid}(0,\sigma^2)$. That is, the normality assumption of the error term is assumed. The goal is to estimate the vector of parameters $\boldsymbol{\vartheta}=(\nu, \phi_1, \theta_1, \sigma^2)$.

- We use the notation $\boldsymbol{\vartheta}$ ("vartheta") to denote a general parameter vector containing all the parameters of the model.

- Even though we concentrate on the ARMA(1,1), the following argumentation generalizes readily to more general ARMA processes, which are of the form $y_t = \mathsf{E}_{t-1}(y_t) + u_t$ where $\mathsf{E}_{t-1}(y_t)$ corresponds to the employed model structure (systematic part of the model). Here $\mathsf{E}_{t-1}(\cdot)$ denotes the conditional expectation and it will be introduced more detail in Forecasting section. In this ARMA(1,1) case, we get $\mathsf{E}_{t-1}(y_t) = \nu + \phi_1 y_{t-1} + \theta_1 u_{t-1}$, whereas, e.g., in the AR($p$) case we get $\mathsf{E}_{t-1}(y_t) = \nu + \phi_1 y_{t-1} + \cdots + \phi_p y_{t-p}$.

In the ARMA(1,1) model, taking the initial values for $y_0$ and $u_0$ as given, the sequence of $u_1, \ldots, u_T$ can be constructed from $y_1, \ldots, y_T$ by iterating
\begin{equation*}
u_t = y_t  - \nu - \phi_1 y_{t-1} - \theta_1 u_{t-1}, \quad t=1,\ldots,T.
\end{equation*}
When conditioning on $y_{t-1}$ and $u_{t-1}$, which are included in the information available at time $t-1$, we end up that the conditional distribution of $y_t$ that is (conditionally) normally distributed due to the normality assumption of $u_t$:
\begin{equation*}
y_t|(y_{t-1}, u_{t-1}) \thicksim \mathsf{N}(\nu + \phi_1 y_{t-1} + \theta_1 u_{t-1}, \sigma^2).
\end{equation*}
The specific form of the conditional density function of $y_t$, conditional on $y_{t-1}$ and $u_{t-1}$, is hence
\begin{equation*}
f_{y_t|y_{t-1}, u_{t-1}}(y_t|y_{t-1}, u_{t-1}; \boldsymbol{\vartheta}) = \frac{1}{\sqrt{2 \pi \sigma^2}} \mathrm{exp} \Big(- \frac{(y_t - \nu - \phi_1 y_{t-1} - \theta_1 u_{t-1})^2}{2 \sigma^2}  \Big).
\end{equation*}


&nbsp;

**Construction of the log-likelihood function**. The (conditional) log-likelihood function can based on the conditional density functions for single observations. Here we are not just restricting ourselves to the ARMA(1,1) and/or Gaussian case. That is the following steps can be generalized also to other modelling choices such as ARMA models.

Denote $\ubar{\mathbf{Y}}_{t}= (y_1 \ldots y_t)$ and, therefore, the sample of observations is denoted by $\ubar{\mathbf{Y}}_T=(y_1, \ldots y_T)$. The joint conditional density function (without arguments) $f_{\ubar{\mathbf{Y}}_{T}}(\ubar{\mathbf{Y}}_{T})$ is obtained as the product of conditional density functions
\begin{equation*}
f_{\ubar{\mathbf{Y}}_T}=f_{y_T|\ubar{\mathbf{Y}}_{T-1}}\cdot f_{\ubar{\mathbf{Y}}_{T-1}}=f_{y_T|\ubar{\mathbf{Y}}_{T-1}} f_{y_{T-1}|\ubar{\mathbf{Y}}_{T-2}}\cdot f_{\ubar{\mathbf{Y}}_{T-2}}=\cdots=\prod_{t=1}^{T} f_{y_t|\ubar{\mathbf{Y}}_{t-1}}\cdot f_{\ubar{\mathbf{Y}}_0}.
\end{equation*}
By conditioning on $\ubar{\mathbf{Y}}_0$, which contains the necessary initial values (depending on, e.g., the lag lengths $p$ and $q$ of the ARMA($p,q$) model), the conditional density function gets the form
\begin{equation*}
    \prod_{t=1}^{T} f_{y_t|\ubar{\mathbf{Y}}_{t-1}},
\end{equation*}
which then leads to the the (conditional) log-likelihood function
\begin{eqnarray*}
l(\boldsymbol{\vartheta}) = \sum_{t=1}^{T} \mathrm{log} \, f_{y_t|\ubar{\mathbf{Y}}_{t-1}}(y_t|\ubar{\mathbf{Y}}_{t-1}; \boldsymbol{\vartheta}).
\end{eqnarray*}

- Going back to the specific example of Gaussian ARMA(1,1) model, the conditional log-likelihood function is hence
\footnotesize
\begin{eqnarray*}
l(\boldsymbol{\vartheta}) = -\frac{T}{2} \mathrm{log}(2 \pi) - \frac{T}{2} \mathrm{log}(\sigma^2) - \frac{1}{2 \sigma^2} \sum_{t=1}^{T} 
u^2_t,
\end{eqnarray*}
\normalsize
where $u_t = y_t - \nu - \phi_1 y_{t-1} - \theta_1 u_{t-1}$ in this ARMA(1,1) case.

The maximum likelihood estimate (MLE) of $\boldsymbol{\vartheta}$ is obtained by maximizing the conditional log-likelihood function. This requires numerical optimization methods. These numerical (iterative) algorithms require initial values and/or possibly also preliminary estimation of the parameters, but econometric/statistical programs and packages are carrying out these steps straightforwardly.

&nbsp;

**AR($p$) case**. We will next show that, in the case of the AR($p$) model, the conditional maximum likelihood estimation actually leads to the (conditional) least squares estimates when the error term is Gaussian ($u_t \thicksim \mathrm{nid}(0, \sigma^2)$). 

Since $y_t$ is a linear combination of $u_t, u_{t-1}, \ldots$ (given stationarity and corresponding MA($\infty$) representation), it follows that $u_s$ and $\boldsymbol{x}_t$ are independent $\forall s \ge t$, where, as above, $\boldsymbol{x}_t=[1 \quad y_{t-1} \, \cdots \, y_{t-p}]^{\prime}$. By assuming the normality of the error term, we get 
\begin{equation*}
    y_t|\ubar{\mathbf{Y}}_{t-1} \thicksim \mathsf{N}(\boldsymbol{x}^{'}_t \boldsymbol{\beta}, \sigma^2),
\end{equation*}
and the conditional density function of $y_t$ is
\begin{equation*}
    f_{y_t|\ubar{\mathbf{Y}}_{t-1}}(y_t|\ubar{\mathbf{Y}}_{t-1}) = \frac{1}{\sqrt{2 \pi \sigma^2}}\mathrm{exp}\Big(-\frac{1}{2\sigma^2}(y_t -\boldsymbol{x}^{'}_t \boldsymbol{\beta})^2 \Big).
\end{equation*}
From this we get the (sample) log-likelihood function
\begin{equation*}
l(\boldsymbol{\vartheta}) \equiv l(\boldsymbol{\beta}, \sigma^2)=-\frac{T-p}{2} \mathrm{log}(2\pi)-\frac{T-p}{2} \mathrm{log}(\sigma^2)-\frac{1}{2\sigma^2}\sum_{t=1}^{T}(y_t-\boldsymbol{x}^{'}_t \boldsymbol{\beta})^2.
\end{equation*}
where the first term can also be removed because it does not depend on the parameters $\boldsymbol{\vartheta}$. This corresponds the (conditional) log-likelihood function of a Gaussian linear regression model, but now for time series observation $(y_1,\ldots, y_T)$. Maximizing this gives us the same conditional least squares estimator $\widehat{\boldsymbol{\beta}}$ (and $\widehat{\sigma}^2$) as obtained above.


&nbsp;

**Exact method of maximum likelihood**. The exact log-likelihood function contains also the impact of initial values when constructing the log-likelihood function. Some details on this technique is provided below.

&nbsp;

<div class="toggle-button" onclick="toggleCode('Extra10')">Extra: Exact maximum likelihood estimation of ARMA models</div>
<div id="Extra10" style="display:none;">

Let us take a closer look at exact maximum likelihood (ML) based estimation.

**The exact likelihood function**. For the purpose of estimation based on the exact method of maximum likelihood, consider the \emph{Gaussian} ARMA($p,q$) process
\begin{equation*}
    y_{t} = \nu + \phi_{1}y_{t-1}+\cdots+\phi_{p}y_{t-p}+u_{t}+\theta_{1}u_{t-1}+\cdots+\theta_{q}u_{t-q},\,\, u_{t}\sim\mathsf{nid}\left(  0,\sigma^{2}\right),
\end{equation*}
and assume the stationarity, invertibility and the identification condition of the ARMA process hold. Suppose $\boldsymbol{y}=\left(  y_{1},\ldots,y_{T}\right)$ is a vector of observations generated by this process. As before, denote $\boldsymbol{\phi}=(\phi_{1},\ldots,\phi_{p})$, $\boldsymbol{\theta}=\left(  \theta_{1},\ldots,\theta_{q}\right)$ and $\boldsymbol{\boldsymbol{\beta}}=(\boldsymbol{\phi},\boldsymbol{\theta})$. Making use of the general formulas for the mean and autocovariance function of a linear process, it can be seen that $\mathsf{E}\left(\boldsymbol{y}\right) = \boldsymbol{0}$ and $\mathsf{Cov}\left(  \boldsymbol{y}\right)  =\sigma^{2} \boldsymbol{\Sigma}$, where the (positive definite) matrix $\boldsymbol{\Sigma} = \boldsymbol{\Sigma}\left(\boldsymbol{\boldsymbol{\beta}}\right)$ $\left(  T\times T\right)$ is a function of the parameter $\boldsymbol{\boldsymbol{\beta}}$\ (but not of the parameter $\sigma^{2}$).

Since linear transformations of Gaussian distributions are also Gaussian (this holds also for infinite dimensional transformations), $\boldsymbol{y}\sim \mathsf{N}\left(\boldsymbol{0},\sigma ^{2} \boldsymbol{\Sigma} \right)$.

<!-- - Again, a non-zero expected value can be taken into consideration by subtracting the mean (or more generally the trend estimated by LS or the seasonal component) without affecting the asymptotic properties of the ML-estimators for$\boldsymbol{\boldsymbol{\beta}}$ and $\sigma ^{2}$. Alternatively, a constant term can be added to the ARMA equation just as in the case of the AR($p$) model. -->

- In addition to the constant term, a trend component can be inserted in without affecting the asymptotic properties of the ML-estimators for$\boldsymbol{\boldsymbol{\beta}}$ and $\sigma ^{2}$.

The density function of the random vector $\boldsymbol{y}$ is 
\begin{equation*}
    f_{\boldsymbol{y}}\left( \boldsymbol{y}\right) =\left( 2\pi \right) ^{-T/2}\det\left( \sigma ^{2}\boldsymbol{\Sigma }\right) ^{-1/2}\exp\left\{ -\frac{1}{2\sigma ^{2}}\boldsymbol{y}^{\prime}\boldsymbol{\Sigma}^{-1}\boldsymbol{y}\right\} .
\end{equation*}
Making use of properties of the determinant, $\det\left(  \sigma^{2}\boldsymbol{\Sigma}\right)=\sigma^{2T}\det\left(\boldsymbol{\Sigma}\right)$, so that the log likelihood function becomes
\begin{equation*}
    l\left( \boldsymbol{\beta},\sigma ^{2}\right) =-\frac{T}{2}\log \sigma ^{2}-\frac{1}{2}\log \det \left(\boldsymbol{\Sigma }\left( \boldsymbol{\beta} \right)\right) -\frac{1}{2\sigma ^{2}}\boldsymbol{y}^{\prime }\boldsymbol{\Sigma}\left(\boldsymbol{\beta} \right) ^{-1}\boldsymbol{y}.
\end{equation*}
Because the matrix $\boldsymbol{\Sigma}\left(  \boldsymbol{\boldsymbol{\beta}}\right)$\ is a rather complicated function of the parameter $\boldsymbol{\boldsymbol{\beta}}$, the log-likelihood function cannot be expressed in a simple form and, consequently, the above expression is difficult to be used directly to maximize the likelihood function. In practice, one has to resort to numerical methods to maximize the likelihood function. This involves computing the inverse matrix $\boldsymbol{\Sigma}\left(  \boldsymbol{\boldsymbol{\beta}}\right)  ^{-1}$\ and the determinant $\det\left(  \boldsymbol{\Sigma}\left(  \boldsymbol{\boldsymbol{\beta}}\right)\right)$\ for a range of given values of $\boldsymbol{\boldsymbol{\beta}}$. For a given value of $\boldsymbol{\boldsymbol{\beta}}$, the matrix $\boldsymbol{\Sigma}\left(  \boldsymbol{\boldsymbol{\beta}}\right)$\ can be computed as described in Section \@ref(ARMAprocesses).

Many different algorithms have been proposed to solve the maximization problem described above.
<!-- .  One of these is based on the so-called Cholesky decomposition of a positive definite matrix. When applied to the matrix $\boldsymbol{\Sigma}$, this decomposition tells us that $\boldsymbol{\Sigma}$\ can be written as 
\begin{equation*}
    \boldsymbol{\Sigma}=\boldsymbol{CC}^{\prime},
\end{equation*}
where $\boldsymbol{C}=\left[c_{ij}\right]$ $\left(  T\times T\right)$ is a lower diagonal matrix (that is, $c_{ij}=0$ for $i<j$) satisfying $c_{ii}>0,$ $i=1,\ldots,T$. When the value of the parameter $\boldsymbol{\boldsymbol{\beta}}$\ is fixed, modern computer programs can without difficulty calculate this decomposition. The same holds for the inversion of the matrix $\boldsymbol{C}$ due to its lower diagonal nature (from a computational point of view, inversion is analogous to solving the linear equation $\boldsymbol{a} = \boldsymbol{Cz}$, which can in this lower diagonal case performed recursively). Because we also have $\det\left(\boldsymbol{C}\right) = c_{11}\cdots c_{TT}$, the log-likelihood function can be written as
\begin{equation}
    l\left( \boldsymbol{\beta},\sigma ^{2}\right) =-\frac{T}{2}\log \sigma^{2}-\sum_{t=1}^{T}\log c_{tt}\left( \boldsymbol{\beta} \right) -\frac{1}{2\sigma ^{2}}\mathsf{S}\left( \boldsymbol{\beta} \right),  
(#eq:Logusk)
\end{equation}
where $\mathsf{S}\left(  \boldsymbol{\boldsymbol{\beta}}\right)=\boldsymbol{y}^{\prime}\boldsymbol{C}\left(  \boldsymbol{\boldsymbol{\beta}}\right)^{\prime-1}\boldsymbol{C}\left(\boldsymbol{\boldsymbol{\beta}}\right)^{-1}\boldsymbol{y}$ and where we have been explicit about the dependence of the matrix $\boldsymbol{C}$\ on the parameter $\boldsymbol{\boldsymbol{\beta}}$.

As in the case of a linear model (or normal model) for a given value of $\boldsymbol{\boldsymbol{\beta}}$, the log-likelihood function $l\left(  \boldsymbol{\boldsymbol{\beta}},\sigma^{2}\right)$\ is maximized when $\sigma^{2} = T^{-1}\mathsf{S}\left(\boldsymbol{\boldsymbol{\beta}}\right)$. Therefore, if $\boldsymbol{\widehat{\boldsymbol{\beta}}}$\ and $\widehat{\sigma}^{2}$ are the ML estimators of $\boldsymbol{\boldsymbol{\beta}}$ and $\sigma^{2}$, it holds that
\begin{equation*}
    \widehat{\sigma}^{2}=T^{-1}\mathsf{S}(\boldsymbol{\widehat{\boldsymbol{\beta}})}.
\end{equation*}
In addition, the M estimator $\boldsymbol{\widehat{\boldsymbol{\beta}}}$ of the parameter $\boldsymbol{\boldsymbol{\beta}}$ can be obtained by maximizing the so-called profile log-likelihood function
\begin{equation*}
    l_{\mathsf{p}}\left(  \boldsymbol{\boldsymbol{\beta}}\right)  =-\frac{T}{2}\log\mathsf{S}\left(  \boldsymbol{\boldsymbol{\beta}}\right)  -\sum_{t=1}^{T}\log c_{tt}\left(\boldsymbol{\boldsymbol{\beta}}\right).
\end{equation*}
Maximizing the profile log-likelihood function requires numerical methods. 
<!-- One begins from an initial value, say 
$\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(0\right)}$, and then proceeds iteratively to estimates $\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(1\right)}$, $\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(2\right)}$, \ldots, which (hopefully) converge to the maximum likelihood estimate $\boldsymbol{\widehat{\boldsymbol{\beta}}}$. A general iteration formula takes the form 
\begin{equation*}
    \boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(i+1\right)}=\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(i\right)}+a^{\left(i\right)}\boldsymbol{d}^{\left(i\right)},
\end{equation*}
where $\boldsymbol{d}^{\left(i\right)}$ is a so-called direction vector that indicates to which direction should the $i$th estimate $\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(i\right)}$ be changed to, and the (scalar) $a^{\left(i\right)}$ is a so-called step length that determines the magnitude of this change. The iterative algorithm should (typically) choose these in a way that ensures $l_{\mathsf{p}}(\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(i+1\right)})\geq l_{\mathsf{p}}(\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(i\right)})$. For example, in a well-known maximization algorithm called the Newton-Raphson method, the direction vector is given by $\boldsymbol{d}^{\left(i\right)}=-\bigl(\partial^{2}l_{\mathsf{p}}(\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(  i\right)})/\partial\boldsymbol{\boldsymbol{\beta}}\partial\boldsymbol{\boldsymbol{\beta}}^{\prime}\bigr)^{-1}\partial l_{\mathsf{p}}(\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(i\right)})/\partial\boldsymbol{\boldsymbol{\beta}}$.

- This can be motivated based on the Taylor approximation
\begin{equation*}
    l_{\mathsf{p}}\left(\boldsymbol{\boldsymbol{\beta}}\right)\approx l_{\mathsf{p}}(\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(i\right)}\boldsymbol{)+}(\partial l_{\mathsf{p}}(\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(i\right)})/\partial\boldsymbol{\boldsymbol{\beta})}(\boldsymbol{\boldsymbol{\beta}}\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(i\right)})\boldsymbol{+}\frac{1}{2}(\boldsymbol{\boldsymbol{\beta}}-\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(i\right)  }\boldsymbol{)}^{\prime}\left(\partial^{2}l_{\mathsf{p}}(\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(i\right)})/\partial\boldsymbol{\boldsymbol{\beta}}\partial\boldsymbol{\boldsymbol{\beta}}^{\prime}\right)(\boldsymbol{\boldsymbol{\beta}}-\boldsymbol{\widehat{\boldsymbol{\beta}}}^{\left(i\right)}\boldsymbol{)},
\end{equation*}
whose maximization with respect to $\boldsymbol{\boldsymbol{\beta}}$ produces as result the above mentioned $\boldsymbol{d}^{\left(i\right)}$. 

With modern computational resources, computing values of the profile log-likelihood $l_{\mathsf{p}}\left(\boldsymbol{\boldsymbol{\beta}}\right)$ is straightforward, and these can be further used to compute numerical approximations of the partial derivatives in the preceding expression.
-->

</div>


&nbsp;

**Statistical inference**. It can be shown that when the stationarity, invertibility, and identification conditions hold, the "usual" asymptototic properties of an maximum likelihood estimator (exact or conditional) hold. In particular, the estimators $\boldsymbol{\widehat{\boldsymbol{\beta}}}$\ and $\widehat{\sigma}^{2}$ are both consistent, asymptotically normally distributed and asymptotically independent. In other words, it holds
\begin{equation*}
    \boldsymbol{\widehat{\boldsymbol{\beta}}}\underset{as}{\sim}\mathsf{N}\left(  \boldsymbol{\boldsymbol{\beta}},\boldsymbol{V}\left(\boldsymbol{\boldsymbol{\beta}}\right)  ^{-1}\right),
\end{equation*}
where the matrix $\boldsymbol{V}\left(\boldsymbol{\boldsymbol{\beta}}\right)=\mathsf{E}\left[-\partial^{2}l(\boldsymbol{\boldsymbol{\beta}},\sigma^{2})/\partial\boldsymbol{\boldsymbol{\beta}}\partial\boldsymbol{\boldsymbol{\beta}}^{\prime})\right]$ is the so-called Fisher information matrix of the parameter $\boldsymbol{\boldsymbol{\beta}}$ (the parameter $\sigma^{2}$ does not appear in the final expression of $\boldsymbol{V}\left(\boldsymbol{\boldsymbol{\beta}}\right)$ as a result of taking the expectation). 

- These asymptotic results hold also without the normality assumption, although in that case the estimators are no longer (asymptotically)\ efficient. It should be noted that the stationarity, invertibility, and identification conditions are required for the above asymptotic distribution result, which can give a poor approximation also when these conditions are "nearly violated".

&nbsp;

**Hypothesis testing**. Using the empirical counterpart of $\boldsymbol{V}\left(\boldsymbol{\boldsymbol{\beta}}\right)$, namely $\widehat{\boldsymbol{V}}(\boldsymbol{\widehat{\boldsymbol{\beta}},\widehat{\sigma}^{2}})=-\partial^{2}l(\boldsymbol{\widehat{\boldsymbol{\beta}}},\widehat{\sigma}^{2})/\partial\boldsymbol{\boldsymbol{\beta}}\partial\boldsymbol{\boldsymbol{\beta}}^{\prime}$ (the so-called empirical or observed information matrix of the parameter $\boldsymbol{\boldsymbol{\beta}}$), the asymptotic distribution result above can be used to construct statistical Wald tests and confidence intervals concerning the parameter $\boldsymbol{\boldsymbol{\beta}}$ 

- The partial derivatives appearing in this expression can in practice be approximated with their numerical counterparts. 

In particular, the square roots of the diagonal elements of the matrix $\widehat{\boldsymbol{V}}(\boldsymbol{\widehat{\boldsymbol{\beta}}},\widehat{\sigma}^{2}\boldsymbol{)}^{-1}$ can be used as approximate standard errors of the components of the estimator $\boldsymbol{\widehat{\boldsymbol{\beta}}}$. For instance, an individual estimated component of $\boldsymbol{\widehat{\boldsymbol{\beta}}}$ would be interpreted as "significantly" different from zero if its absolute value is at least 2 (or 1.96) times the size of its approximate standard error. Formally, $\boldsymbol{V}(\boldsymbol{\beta}, \sigma^2)^{-1} = [v^{ij}]$, its empirical counterpart is $\widehat{\boldsymbol{V}}(\widehat{\boldsymbol{\beta}}, \widehat{\sigma}^2)^{-1} = [\widehat {v}^{ij}]$, and
\begin{equation*}
    \widehat{\boldsymbol{\beta}}_i \underset{as.}{\thicksim} \mathsf{N}(\boldsymbol{\beta}_i, v^{ii}).
\end{equation*}
Thus null hypothesis $\beta_i=0$ gets rejected at the 5\% significance level if the $t$-ratio (cf. $t$-test)
\begin{equation*}
    \Big|\frac{\widehat{\boldsymbol{\beta}}_i}{\sqrt{\widehat {v}^{ii}}}\Big|\ge 1.96 \Leftrightarrow|\widehat{\boldsymbol{\beta}}_i| \ge 1.96 \sqrt{\widehat {v}^{ii}}
\end{equation*}
and the 95\% confidence intervals for $\beta_i$ can be obtained by
\begin{equation*}
    \widehat{\beta}_i \pm 1.96 \cdot \mathrm{s.e.}(\widehat{\beta}_i) =1.96\sqrt{\widehat {v}^{ii}}.
\end{equation*}
Tests constructed using likelihood ratio principles can also be used in a conventional manner. 


&nbsp;

**Empirical examples**. In the previous section, we concluded an AR(2) model to be one possible candidate for the quarterly U.S real GDP growth (1985:Q1--2007:Q2). The conditional maximum likelihood estimation of this model gives us
\begin{equation*}
    y_{t} = \underset{\left(0.197\right) }{1.693} + \underset{\left(0.101\right) }{0.160} y_{t-1} + \underset{\left(0.101\right) }{0.287} y_{t-1} + \widehat{u}_{t}, \quad \widehat{\sigma}^{2}=3.536,
\end{equation*}
where under the estimates in brackets are the approximate standard errors. Especially the estimate for the AR(2) coefficient is statistically significant at the 5\% significance level and hence the model cannot be shrinked. Alternatively, if reporting the estimation result for the demeaned process, we then obtain
\begin{equation*}
    \bar{y}_{t} = \underset{\left(0.101\right) }{0.160}\bar{y}_{t-1} + \underset{\left(0.102\right) }{0.287}\bar{y}_{t-2} +\widehat{u}_{t},
\end{equation*}
where $\bar{y}_{t}=y_{t}-3.061$ is the demeaned GDP growth series. 


<!-- (ii) We also saw that the AR(2) model based on the autocorrelation and partial autocorrelation functions of the sunspot series could be justifiable to enlarge into an ARMA(2,1) model. The ML-estimates of this model are $\widehat{\phi}_{1}=1.225$ $\left(0.113\right)$, $\widehat{\phi}_{2}=-0.561$ $\left( 0.108\right)$ and $\widehat{\theta}_{1}=0.385$ $\left( 0.133\right)$ showing, the estimate of the MA parameter to be statistically ``significant''. In general these examples show, that it is not always easy to choose the ARMA model orders based on the (partial) autocorrelation functions. % (see also the GDP growth example in Figure \ref{fig:usrealbktacf}). -->


&nbsp;
