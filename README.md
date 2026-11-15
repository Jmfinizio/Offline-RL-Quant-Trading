# Offline Reinforcement Learning for Quantitative Trading

**DS 543 Final Project · Boston University · May 2025**
Johnathan Finizio and Sachiel Chukrow

Testing a trading policy live costs real money when it's wrong. These agents learn entirely from historical market data using conservative offline RL. **Conservative Q-Learning (CQL)** and **Batch-Constrained Q-Learning (BCQ)** prevent the model from overestimating actions the data never showed.

## Results
| Strategy | Return |
|---|---|
| **CQL Actor-Critic** | **81.7%** |
| CQL Actor-Free | 80.7% |
| Buy and hold | 74.7% |
| S&P 500 | 65.8% |

BCQ was trained on 1990–2019 and tested on 2020–2025 across 71 S&P 500 stocks. The fully offline version returned ~120.2%, beating the market by 5.65 points.

## Approach
- **Environment:** daily steps with prices, dividends, volume, the 10-year Treasury rate, cash, and S&P 500 data, using a continuous allocation action space.
- **Reward:** % change in portfolio value minus % change in the S&P 500, with a per-trade cost to discourage churn.
- **Baselines:** linear regression, random forest, and DQN.
- **CQL Actor-Free:** double-Q network trained on an expert momentum strategy (top 10 by Sharpe ratio, 95% invested).
- **CQL Actor-Critic:** trained on random actions, with an entropy bonus to encourage diversification.
- **BCQ:** a VAE generates plausible actions and a perturbation actor adjusts them. Partially online and fully offline versions were compared.

## Contents
- `Offline_RL_for_Quantitative_Trading.pdf`: the full paper.
