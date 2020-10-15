# Listed Companies Valuation on NYSE, AMEX, NASDAQ
 
#### Introduction 

Many investors buy a stock, because they feel it is a 'good' company due to a strong product or business model the company has. Based on the individual interpretation of the company, investors buy a share of the company in the hopes of the company results, i.e. valuation increases, making their investment payoff. 
 
We deemed a human to be healthy or in 'good' condition based on one's blood pressure, cholestrol level, blood test etc., are we able to safely say a human is 'good' condition because he/she completes a triathlon every year.

Just like a human, a company has vitals too, which is its financial data, such as Price to Earnings Per Share ratio, Operating Margin, Current Ratio, Sales Growth etc. and we can use such data points to determine the valuation of a company. 

With multiple financial data vitals, it is difficult to clearly state which vitals can tell with claritiy which are useful in telling the company valuation.

#### Problem Statement

My model aims to study the stocks listed on the US exchanges, NYSE, AMEX, and NASDAQ, and each stock's vitals  to determine market capitalisation (i.e. valuation) of a company. By comparing to other companies, a predicted valuation of a company will tell an investor whether a company has more room to grow in valuation (i.e. the predicted market cap is higher than the current market cap)  or the company is currently overvalued ( i.e the predicted market cap is lower than the current market cap ). 

Regression models will be used in this study, with the metrics of Root Mean Square Error (RMSE). The RMSE is a efficient metric when dealing with large errors, which is practical, as the market valuations varies in the thousands amongst companies. 

#### Outcome
By the end of this study, an investor will be able to know which company vitals is essential in predicting valuation, also an optimal model to predict the valuation of a company. 

With such information, from retail investors to institutional investors that manages pension funds, will  have that slight advantage in the stock market, to make the right investment!

#### Process Flow
1. Check for data types
2. Prelimnary EDA
3. Drop no target variable 
4. 2nd Preliminary EDA
5. Analysis on imputing data
6. Imputing missing values
7. Feature Engineering
8. Final EDA
9. Modelling
10. Model Evaluation
11. Conclusion