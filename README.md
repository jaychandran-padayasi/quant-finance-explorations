# Explorations in Quantitative Finance and Financial Mathematics

This repository holds four mini-projects that I completed during the Summer 2025 offering of Intro to Quantitative Methods in Finance bootcamp by The Erdos Institute. The projects span foundational topics in financial mathematics, namely modern portfolio theory, empirical testing of financial assumptions, analytical behavior of option pricing formulas, and stochastic volatility modeling. Together, they reflect a blend of mathematical rigor, empirical analysis, and computational implementation in Python, using real-world financial data. 

---

## 1. Portfolio Optimization with Liquidity Constraints

The first mini-project explores portfolio optimization using Modern Portfolio Theory. The objective was to create sample portfolios consisting of stocks with different risks. I aimed to create a highly customizable Jupyter notebook that can be modified easily to create many custom portfolios. 

I began by scraping the S\&P 500 ticker list along with their sector classifications, then randomly selected 20 stocks from 3 different sectors. Using historical price data, I computed mean daily returns and the covariance matrix for these stocks. I use yfinance for stock date.

As we learnt in the lectures, the _efficient frontier_ of a set of stocks is given by the set of portfolios which are not dominated by any other portfolio. This means that one cannot construct a portfolio that has _both_ a higher expected return and a lower risk. The Jupyter notebook has a function that can be customized to generate the efficient frontier. I used the mean of simple returns over a year as proxy for expected return of the stocks.  

Additionally, I incorporated the effects of liquidity, with the understanding that low liquidity implies that one cannot trade high volumes of the stock without altering the market price. The "liquidity aware objective" was defined with a Lagrange multiplier $\lambda$ that punishes low liquidity as follows: 
```math
\mathcal{O}[w] = w^T\cdot\Sigma\cdot w + \lambda\left(\frac{w^T\cdot w}{V}\right) 
```
where $w$ is the weight vector, $\Sigma_{ij} = \text{Cov}(S_i, S_j)$ and $V_i$ are the average volumes traded over the period of one year. However, I found that the S&P 500 companies are all too big for this to make a noticeable difference in the efficient frontier. Nevertheless, this function is included in the notebook if one chooses to trade in more illiquid assets. 

In the notebook, I have generated a sample portfolio for both the high-risk and low-risk scenarios by sampling the efficient frontier with $\lambda = 0$. Their stats are as follows:

  * High-risk portfolio: 20.05% annualized volatility, 0.21% mean daily return
  * Low-risk portfolio: 13.23% volatility, 0.07% mean daily return

### Key goals achieved:
  * Developed a module that can be used to compute the efficient frontier of any given set of stocks.
  * Implemented a liquidity aware algorithm that can be used to protect against illiquid assets.
