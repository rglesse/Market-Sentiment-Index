# Building a Market Sentiment Index for the Chinese Stock Market
Program developed for academic purposes at PHBS (Peking University HSBC Business School).

The first code "Static PCA" is an adaptation of the market index building methodology developed by Malcolm Baker and Jeffrey Wurgler (2007) to the Chinese Market.
The final purpose of the code is to create an index to measure market sentiment in the Shanghai Stock Exchange and test its returns. The code starts by selecting the
better indicators that will compose the index. Better indicators here are those that explain the most variance in the data. In order to 
do this, we use Principal Component Analysis of 7 indicators of market sentiment both in time t and time t+1. We selected the indicators that have  stronger correlation with the first PCA.

Next, after selecting 7 proxies, we regress them against macroeconomic indicators, to get only the residuals. The rationale for this is that sentiment might be "rational" to the extent that it reflect optimism or pessimism grounded in the current macroeconomic situation. To build the index itself we again use Principal Component Analysis (PCA). The first PCA weights will be our index.

Finally, we compute average sentiment and its standard deviation for our trading strategy. The trading strategy mirror Peter's Lynch Cocktail Part: 
"Enter the market when investor have too lower expectation or just start rising; leave when the expectation is too high or the market begins to decline."
To do this, we buy the market index (SSE 300) when it is trading between mean sentiment and std deviation of sentiment or when it is trading below
mean-std deviation of sentiment. In contrast, we sell the market index and buy the risk free asset when the index is trading above one std deviation or below 
mean sentiment (but above mean-std deviation).

The last piece of code test the results and plot the returns.


The second code does essentially the same, but the process by which it does so makes it more applicable in real life. The first code is using same data to both get
the market sentiment index and to test it. The second code, "Dynamic PCA" gets the residuals against macroeconomic data on a rolling regression basis. Therefore it only considers past data when testing for results.
This is also divided in two methods: Fixed Window and Cumulative Window rolling regression. The Fixed Window uses the data from the past 12 months only,
while the cumulative uses all past data (as we advance through time) to generate the market index.

The main finding is that the Cumulative Window Rolling Regression method performs better as it is fed with more past data. Therefore, the trading
strategy based on this method gives the best results, if we don't compare with the Static method, which is not replicable in real life.
