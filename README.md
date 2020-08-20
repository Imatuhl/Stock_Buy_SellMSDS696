# Stock_Buy_Sell
forecasting stock price with sentiment analysis, LSTM and ARIMA

Disclaimer: THIS IS NOT STOCK ADVICE DO NOT USE THIS FOR PERSONAL USE.

## Introduction

The purpose of this experiment is to use sentiment analysis paired with forecasting machiine learning methods to determine future trends for stock prices.

Using these two methods will hopefully give us enough insight to determine the future direction of a stock so that we can determine if it should be bought sold or held.

## The Data

The sentiment data was obtained from Kaggle and included many different headlines from many different sources. The features of this data included article count, headline, url, publisher, date, and stock. The stock price data was obtained from fidelity investments and included pricing data from a ten year time frame. The data's features were date, open, high, low, close, and volume. 

The headlines were chosen for sentiment data because I worked under the assumption that investors are irrational and they do not read an entire article to obtain all of the facts. So to complete the sentiment analysis I removed the all of the other features and focused on the headlines. Then the headlines were cleaned removing any whitespace, capital letters, specail characters, and more.

The stock price data needed to be maniuplated to remove disclosure information and other data not valuable to the analysis. Closing price was chosen to complete the analysis for the stock pricing data as it is the final price over a day of trading.

## Exploration

To explore the sentiment data intial graphs were created to see how data was distributed. Next, I created word coulds to see if I could see which words appeared the most. 

![GitHub Logo](/images/CSCONEWSgraph.png)![GitHub Logo](/images/DukNewGraph.png)![GitHub Logo](/images/JpmNewsGraph.png)![GitHub Logo](/images/LuvNewsGraph.png)

![GitHub Logo](/images/CscoWordCloud.png)![GitHub Logo](/images/DukWordCloud.png)![GitHub Logo](/images/JPMWordCloud.png)![GitHub Logo](/images/LuvWordCloud.png)

Price graphs with added rolling mean and standard deviation were generated to obtain a good idea of the shape and trend of the overall pricing data. 

![GitHub Logo](/images/cscopricegraph.png)![GitHub Logo](/images/dukpricegraph.png)![GitHub Logo](/images/jpmpricegraph.png)![GitHub Logo](/images/luvpricegraph.png)

Kernal Density Graphs were created to see what the probabily of a stock being a particular price might be and Volume graphs created to see what trading volatility would look like.

![GitHub Logo](/images/cscodensity.png)![GitHub Logo](/images/dukdensity.png)![GitHub Logo](/images/jpmdensity.png)![GitHub Logo](/images/luvdensity.png)
![GitHub Logo](/images/cscovolume.png)![GitHub Logo](/images/dukvolume.png)![GitHub Logo](/images/jpmvolume.png)![GitHub Logo](/images/luvvolume.png)

## Sentiment Analysis

Sentiment Analysis was done using a VADER Lexicon Approach. This method uses a dictionary method that assigns values to words where the values have been predetermined. Vader uses a sentiment intensity range of -1 to 1 where -1 is highly negative and 1 is very positive. A second analysis was completed using data from FINVIZ to compare results.

Overall the sentiment analysis of the headlines came out to be very slightly positive and very close to neutral. This could be due to the VADER model not understanding the Financial market termanology. Even the second source from FINVIZ yielded similar results. To adjust for this A different lexicon could be used that would better understand the terminology of the Financial system. Another alternative is a source such as stocktwits could be used to analyze sentiment from investors as opposed to analyzing headlines.

![GitHub Logo](/images/cscovader.png)![GitHub Logo](/images/dukvader.png)![GitHub Logo](/images/jpmvader.png)![GitHub Logo](/images/luvvader.png)![GitHub Logo](/images/finviz.png)

The Sentiment Analysis was still positive so we will consider that in the final decision after the forecasting analysis.

## LSTM model

A Long Short Term Memory recurrent neural network (LSTM) was chosen to complete the first analysis of the closing price data for this project. It was chosen because of its simplicity, ease of use, minimal preprocessing, and powerful ability to predict time series data. To normalize the data we needed to scale it and turn it into a numpy array. Then the LSTM model was created keras. 

![GitHub Logo](/images/LSTMSingle.png)

The same model architecture was used for all of the stock pricing data. The model was fitted then predicted the data.

![GitHub Logo](/images/LSTMpredictions.png)

This first model performed very well with root mean squared error all being very low and even making a single step forecast resulted in predictions that were only a few dollars off of the actual closing price.

## Arima Model

The ARIMA model was more time consuming. This model I needed to check to see if the data was stationary and if not manipulate it to make it stationary. I also needed to check for other factors like seasonality by decomposing the data.

A Dickey-Fuller test was done on each stock price data and it was determined that the data was not stationary. I manipulated the data using a log function and completed another Dickey-Fuller test. This made the data stationary. I also completed a weighted average manipulation but this resulted in less stationary data.

Next, I decomposed the data using a decompose function.

![GitHub Logo](/images/cscodecomp.png)![GitHub Logo](/images/dukdecomp.png)![GitHub Logo](/images/jpmdecomp.png)![GitHub Logo](/images/luvdecomp.png)

This did not show any major seasonality so the normal ARIMA model was used instead of the SARIMA model. The ARIMA models were then fit to the pricing data.

![GitHub Logo](/images/cscoarima.png)![GitHub Logo](/images/dukarima.png)![GitHub Logo](/images/jpmarima.png)![GitHub Logo](/images/luvarima.png)

The RSS score on all of these models was very low which indicates a good fit to the ARIMA model. Finally, I used the ARIMA model to forecast 60 days into the future with the pricing data. 

![GitHub Logo](/images/cscoarima.png)![GitHub Logo](/images/dukarima.png)![GitHub Logo](/images/jpmarima.png)![GitHub Logo](/images/luvarima.png)

All of these models show an excellent fit to the data but show a wide variation of price in the 60 day forecast window. Pairing the sentiment analysis with this data and seeing an upward trend we might classify these stocks as a neutral/hold or buy for the purpose of this experiment.
