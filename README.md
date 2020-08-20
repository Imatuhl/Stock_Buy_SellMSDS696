# Stock_Buy_Sell
forecasting stock price with sentiment analysis, LSTM and ARIMA

## Introduction

The purpose of this experiment is to use sentiment analysis paired with forecasting machiine learning methods to determine future trends for stock prices.

Using these two methods will hopefully give us enough insight to determine the future direction of a stock so that we can determine if it should be bought sold or held.

## The Data

The sentiment data was obtained from Kaggle and included many different headlines from many different sources. The features of this data included article count, headline, url, publisher, date, and stock. The stock price data was obtained from fidelity investments and included pricing data from a ten year time frame. The data's features were date, open, high, low, close, and volume. 

The headlines were chosen for sentiment data because I worked under the assumption that investors are irrational and they do not read an entire article to obtain all of the facts. So to complete the sentiment analysis I removed the all of the other features and focused on the headlines. Then the headlines were cleaned removing any whitespace, capital letters, specail characters, and more.

The stock price data needed to be maniuplated to remove disclosure information and other data not valuable to the analysis. Closing price was chosen to complete the analysis for the stock pricing data as it is the final price over a day of trading.

## Exploration

To explore the sentiment data intial graphs were created to see how data was distributed. Next, I created word coulds to see if I could see which words appeared the most. 

![GitHub Logo](/images/CSCONEWSgraph.png)![GitHub Logo](/images/DukNewgraph.png)![GitHub Logo](/images/JpmNewsgraph.png)![GitHub Logo](/images/LuvNewsgraph.png)

Price graphs with added rolling mean and standard deviation were generated to obtain a good idea of the shape and trend of the overall pricing data. 

![GitHub Logo](/images/cscopricegraph.png)![GitHub Logo](/images/dukpricegraph.png)![GitHub Logo](/images/jpmpricegraph.png)![GitHub Logo](/images/luvpricegraph.png)




