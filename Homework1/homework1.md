# Homework 1

## Limit Order Book High-Frequency Trade Execution
### What is the Problem：

A limit order is a type of order to purchase or sell a security at a specified price or better. Limit order trading problem is about when to sell (buy) stocks and how many stocks should be sold (bought) when the trader holds the long (short) stocks. This problem can not only be obtained through the market intuition, the understanding of enterprise information, reasoning and judgment of trader but also through the quantitative method. Quantitative method can make better use of historical information to make decisions. Here I change this problem into a big data problem and make decisions through quantitative methods. First of all, I will show that the problem is a big data problem from three aspects：

***volume:*** In order to solve this problem, I need to collect a large number of data, which is the stock's high-frequency market trading data. Suppose I collect the basic information of all limit orders and collect the first ten bid prices and corresponding volumes, and the first ten ask prices and corresponding volumes every minute. For an active stock, such as Facebook, I can get 1GB of trading data in just ten minutes.

***variety:*** Market transaction data includes two parts, one is the information of each transaction, including transaction type, specific time of transaction, stock volume of transactions, transaction code, transaction price, etc. The other part is the orderbook information of the stock, including bid and ask prices, and the corresponding limit order quantity. Diverse data satisfies variety. Also abundant data can help us to generate useful features as input for decision-making and help us to select the optimal decision.

***velocity:*** The data update speed is fast, and the database needs to be updated frequently. In the trading, when the environment changes, the trader must make a decision immediately, so every minute the trader must make a judgment based on the current latest information. If there is a delay, the information becomes invalid and the strategy may be useless

### How to Solve the Problem？：

***Workflow：***
![Image text]()
***Explain：***

First, the order information data and the stock's limit order book data are collected, and the data is processed into features that can be used as input variables. These features include average of highest bid price and lowest small price, bid ask spread, standard deviation, volatility, the misbalance of bid ask volume, the number of remaining shares of trader, etc.

Second, a part of data is taken as training set and I use reinforcement learning to help trader make decisions. Its essence is to solve the sequence decision making problem. It mainly contains four elements, agent, environmental state, action, reward, and the goal of reinforcement learning is to get the most cumulative reward. In this problem, agent is trader, environment is the data I collect, action is the time and volume of trading, and reward is the gain and loss brought by the change of stock price. Because there are too many states, I choose to train neural network to get reward. I use loss function to maximize reward and minimize loss to control risk and optimize strategy.

Third, take a part of data as the test set. When the reward yield is higher than other strategies on the trading set, I will apply the strategy to the real market

Fourth, the process of using strategy to trade is also the process of constantly generating new data. Every fixed period of time, the data set should be updated, and the strategy should be updated.

## Databases：

I chose KDB + as the database. KDB + is a time series database, its single integrated platform makes it very effective to analyze super large datasets. KBD + supports distributed expansion and it has low latency. KDB + is columnar storage and has many statistical calculation methods

KDB + has three advantages for limit order book high-frequency trade execution problem. First of all, the data of financial transaction problems are all time series data, which can be more efficient through KDB + time series database when collecting information. Secondly, when dealing with features, KDB + column storage can help us to deal with them quickly. Finally, the problem of financial transactions requires low latency, which is the biggest advantage of KDB + compared with other similar databases. The time taken for quick decision-making is very important for profit.
