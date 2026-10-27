# Value at Risk (VaR) and Expected Shortfall (ES)

This project implements three common methods for calculating Value at Risk (VaR) and Expected Shortfall (ES) using Python: Historical Simulation, Variance-Covariance, and Monte Carlo Simulation.

## 1. Historical Simulation Method (Non-Parametric)

**Theory:** Uses historical returns to estimate potential losses without assuming a specific probability distribution.

**VaR Formula:**

$$
\operatorname{VaR}_{\alpha}=-Q_{1-\alpha}(R)
$$

**Expected Shortfall (ES):**

$$
\operatorname{ES}_{\alpha}
=-E[R\mid R\leq Q_{1-\alpha}(R)]
$$

Where:
- $\alpha$ = Confidence level (e.g., 95%)
- $R$ = Historical portfolio returns
- $Q_{1-\alpha}(R)$ = Lower-tail return quantile

ES measures the average loss in the lower tail of the return distribution.

## 2. Variance-Covariance Method (Parametric)

**Theory:** Assumes returns follow a normal distribution. VaR is estimated using the mean, standard deviation, and the appropriate z-score.

**For a Single Asset:**

$$
\operatorname{VaR}_{\alpha}=z_{\alpha}\sigma-\mu
$$

**For a Portfolio:**

$$
\mu_p=w^T\mu
$$

$$
\sigma_p=\sqrt{w^T\Sigma w}
$$

$$
\operatorname{VaR}_{\alpha,p}=z_{\alpha}\sigma_p-\mu_p
$$

**Parametric Expected Shortfall:**

$$
\operatorname{ES}_{\alpha,p}
=-\mu_p+\frac{\sigma_p\phi(z_{\alpha})}{1-\alpha}
$$

Where:
- $\mu$ and $\mu_p$ = Expected asset and portfolio returns
- $\sigma$ and $\sigma_p$ = Asset and portfolio volatility
- $z_{\alpha}=\Phi^{-1}(\alpha)$ = Standard normal quantile
- $w$ = Portfolio weight vector
- $\Sigma$ = Covariance matrix
- $\phi$ = Standard normal probability density function

## 3. Monte Carlo Simulation Method

**Theory:** Generates random scenarios using estimated means, volatilities, and correlations to simulate potential future portfolio returns.

**Steps:**
1. Estimate expected returns and the covariance matrix.
2. Generate correlated random shocks using Cholesky decomposition.
3. Simulate asset returns.
4. Calculate portfolio returns for each scenario.
5. Estimate VaR and ES from the simulated returns.

**Simulation Formula:**

$$
R_{\text{sim}}=\mu+LZ,\qquad Z\sim\mathcal{N}(0,I)
$$

Where $L$ is the lower-triangular Cholesky factor satisfying $\Sigma=LL^T$.

**VaR and ES Formulas:**

$$
\operatorname{VaR}_{\alpha}^{MC}=-Q_{1-\alpha}(R_{\text{sim}})
$$

$$
\operatorname{ES}_{\alpha}^{MC}
=-E[R_{\text{sim}}\mid R_{\text{sim}}\leq Q_{1-\alpha}(R_{\text{sim}})]
$$

Here, $Q_{1-\alpha}(R_{\text{sim}})$ is the empirical lower-tail quantile of simulated portfolio returns.