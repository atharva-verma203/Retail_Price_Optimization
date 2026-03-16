## 🛍️ Retail Price Optimization - Two Distinct Lenses
This project explores retail price optimization through two distinct computational lenses: Neural Networks for high-dimensional predictive modeling and Bayesian Inference for structured demand estimation and uncertainty quantification. By applying these methods to retail transaction data, the project demonstrates how different algorithms can be used to identify the "sweet spot" for pricing to maximize revenue and profit.

## 📊 Overview
* **Introduction**:

  In retail analytics, maximizing product profitability requires a precise understanding of the optimal balance between sales volume and gross revenue generated across different competing product lines. The first part of this project describes the planning and execution of a Neural Network (NN) regression framework to model and predict monthly revenue, which serves as the core performance metric for evaluating different pricing strategies, some of which have been used in the data collection. The underlying dataset incorporates diverse pricing strategies like demand pricing, dynamic pricing, competitive pricing, and bundle pricing. By comparing neural networks with different activation functions like Sigmoid, Rectified Linear Unit (ReLU), and Leaky ReLU, the aim is to verify that by mitigating the vanishing gradient problem, the **ReLU activation function** will provide the highest predictive power necessary to attain an optimized price-revenue equilibrium.

  Further, pricing decisions in retail and e-commerce are often made under considerable uncertainty about demand sensitivity to price changes. The second part of this project deals with the development of a Bayesian framework for price optimization that combines core ideas from Bayesian inference—priors, posterior updating, loss functions, prior odds and prior sampling—with (ii) an applied model for estimating price elasticities and choosing profit-maximizing prices under uncertainty. A hierarchical log–linear demand model is specified, priors are elicited using both substantive knowledge and weakly informative assumptions, and posterior inference is used to construct a decision rule that maximizes posterior expected profit. The Bayesian approach naturally quantifies uncertainty in elasticities and propagates it to the optimal price recommendation.

* **Objectives**:
    1. To model the relationship between price, competitor behavior, and quantity demanded across diverse product categories.
    2. To compare the predictive power of neural networks with the statistical interpretability of Bayesian methods.  
* **Methodology**:
    1. **Neural Networks (ML)**: Implemented to capture non-linearities and complex interactions in retail demand forecasting.
    2. **Bayesian Modeling**: Utilized to estimate price elasticity while accounting for product-level and temporal hierarchies.
* **Data Description** : Retail price data using features like product categories, competitor-wise prices and user ratings, and datetime related features
    1. **Dataset**: [Kaggle Dataset](https://www.kaggle.com/datasets/suddharshan/retail-price-optimization/data)
* **Tools**: R (brms, cmdstanr, dplyr, ggplot2, posterior, tidyverse)

## 💡 Project Highlights

1.  **The Neural Network Approach (for Pattern Recognition)**:
* **Non-Linear Dynamics**: Capable of detecting threshold effects (e.g., demand dropping sharply only after a certain price point) that linear models might miss.
* **Feature Interaction**: Automatically models how competitor pricing impacts demand relative to the primary product's price without manual interaction terms.

2.  **The Bayesian Approach (for Interpretability)**:
* **Multilevel Hierarchy**: Uses random intercepts for product_id and month, allowing the model to "borrow strength" across different products.
* **Elasticity Estimation**: Directly estimates the Own-Price Elasticity coefficient (Log-Log model), providing a clear percentage-based impact of price changes on demand.
* **Uncertainty Quantification**: Instead of a single "best" price, it generates a posterior distribution of optimal prices, showing the confidence interval for profit maximization.

## 📈 Guide to Interpretation
Since this project serves as a technical framework, focus on these metrics when reviewing the output:

1.  **Price Elasticity ($\beta$ for $ln_price$)**:
* If $\beta < -1$: Demand is Elastic (Price sensitive; small price hikes significantly hurt volume).
* If $-1 < \beta < 0$: Demand is Inelastic (Price insensitive; price hikes likely increase total revenue).
* If $\beta \geq 0$ (Anomalous): Indicates potential "Veblen" behavior or presence of confounding variables (e.g., seasonal spikes correlating with price hikes).

    _Note: "Veblen" behaviour, coined from the work by economist Thorstein Veblen, is the phenomenon which states that demand for a luxury good increases as its price rises, defying standard supply-demand laws._

2.  **Profit Maximization**:
* The model identifies the Posterior Median Optimal Price. If the current price is significantly higher than this optimum, the model suggests "Leaving money on the table" due to lost volume.

3.  **Convergence & Reliability**:
* In the Bayesian summary, ensure Rhat values are exactly 1.00. This confirms the Stan chains have converged, which indicate well-sampled posterior distributions, leading to a statistically stable "Optimal Price".

## ⚠️ Technical Note for Stan
This repository uses the $cmdstanr$ backend for R.

1. **Temp Directory**: To avoid Windows permission errors during C++ compilation, the script redirects temp files to C:/Users/Atharva/R_Temp (file path can be adjusted according to user's needs).
2. **Reproducibility**: If running on a new machine, please ensure this folder exists or update the custom_temp variable in the script accordingly.

## 📈 Conclusion
This project demonstrates that retail price optimization is most effective when viewed through a hybrid analytical lens. While the Neural Network framework excels at navigating complex, non-linear feature interactions to provide high-accuracy revenue forecasts, the Bayesian Multilevel Model offers the necessary structural transparency to understand price elasticity and the uncertainty inherent in market responses.

By integrating these methodologies, businesses can move beyond simple "best-guess" pricing and toward a data-driven strategy that balances predictive precision with statistical confidence. This dual approach provides a robust roadmap for identifying the optimized price-revenue equilibrium across diverse and competing product categories.
