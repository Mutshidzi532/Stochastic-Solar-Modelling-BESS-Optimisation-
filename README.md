# Stochastic-Solar-Modelling-BESS-Optimisation-
An engineering mathematics and statistical risk project optimising BESS capacity. Deploys Beta probability distributions, Monte Carlo probability formulations, matrix calculus, and sensitivity analysis to quantify weather uncertainty without relying on software libraries.
# Stochastic Solar Resource Modelling & BESS Capacity Optimisation

**Author:** Mutshidzi Madavha  
**Field:** Renewable Energy Systems / Engineering Mathematics  
**Focus:** Applied Statistics, Probability Density Functions, Matrix Calculus, Asset Optimisation, Engineering Economics  
**Methodology:** Pure Mathematical & Statistical Formulations (Non-Software Dependent)  

---

## 1. Executive Summary
Deterministic renewable models rely heavily on static "average day" parameters. In real-world grid operations, meteorological volatility introduces massive resource uncertainty. 

This project develops a complete mathematical and statistical framework to model solar irradiance volatility and optimise Battery Energy Storage System (BESS) sizing. By deploying continuous probability distributions, joint probability matrices, and differential sensitivity calculus, the model calculates the exact financial inflection point where expanding storage capacity balances out asset risk, independent of external programming software.

---

## 2. Statistical Resource Modelling

### 2.1 Clearness Index & Beta Probability Distributions
To model the random behavior of cloud cover obscuring a 100 MW solar field, the hourly global horizontal irradiance ($GHI$) is converted to a dimensionless Clearness Index ($K_t$):

$$K_t = \frac{GHI}{GHI_{\text{clear-sky}}}$$

Because solar irradiance limits are bounded strictly between 0 (complete darkness) and 1 (perfectly clear sky), standard Gaussian (normal) distributions fail. The resource is instead modeled using a continuous **Beta Probability Density Function (PDF)**:

$$f(K_t; \alpha, \beta) = \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha)\Gamma(\beta)} K_t^{\alpha-1} (1 - K_t)^{\beta-1} \quad \text{for } 0 \le K_t \le 1$$

Where $\Gamma$ represents the standard Gamma function. The shape parameters ($\alpha, \beta$) are calculated analytically from historical site datasets using the statistical Mean ($\mu$) and Variance ($\sigma^2$) of the solar resource:

$$\alpha = \mu \left[ \frac{\mu(1 - \mu)}{\sigma^2} - 1 \right] \quad \text{and} \quad \beta = (1 - \mu) \left[ \frac{\mu(1 - \mu)}{\sigma^2} - 1 \right]$$

---

## 3. Mathematical System Optimisation

### 3.1 Objective Function Formulation
To determine the ideal battery scale, the project formulates a multi-variable capital optimisation problem. The goal is to maximize the lifetime Net Present Value ($NPV$) of the storage asset:

$$\max_{E_{\text{BESS}}, P_{\text{BESS}}} NPV = \sum_{y=1}^{N} \frac{\Delta R_y(E_{\text{BESS}}, P_{\text{BESS}}) - \text{OPEX}_y}{(1 + r)^y} - \text{CAPEX}(E_{\text{BESS}}, P_{\text{BESS}})$$

**Subject to the following strict physical boundary conditions:**
1. **Power Envelope Constraint:** $0 \le P_{\text{charge}}(t) \le P_{\text{BESS}}$ and $0 \le P_{\text{discharge}}(t) \le P_{\text{BESS}}$
2. **Energy Bounds:** $SOC_{\text{min}} \cdot E_{\text{BESS}} \le E_{\text{stored}}(t) \le SOC_{\text{max}} \cdot E_{\text{BESS}}$
3. **Continuity Differential:** $E_{\text{stored}}(t) = E_{\text{stored}}(t-1) + \left(P_{\text{charge}}(t) \cdot \eta_{\text{c}}\right) \Delta t - \left(\frac{P_{\text{discharge}}(t)}{\eta_{\text{d}}}\right) \Delta t$

---

## 4. Analytical Sensitivity & Risk Evaluation

### 4.1 Partial Derivatives for Marginal Returns
To find the exact inflection point of diminishing returns, the model evaluates the partial derivative of Curtailment Reduction ($\Delta C$) relative to incremental steps in Battery Energy Capacity ($\partial E_{\text{BESS}}$):

$$\frac{\partial \Delta C}{\partial E_{\text{BESS}}} = f\left(K_t, \text{Load}, \eta_{\text{round-trip}}\right)$$

As the capacity expands, this derivative approaches zero:

$$\lim_{E_{\text{BESS}} \to \infty} \frac{\partial \Delta C}{\partial E_{\text{BESS}}} = 0$$

This mathematical proof demonstrates that over-sizing the battery leads to systemic asset under-utilisation.

