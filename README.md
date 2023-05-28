# lumber_price_predict
This repository will predict the price of lumber futures with LSTM model.
## Data Set
Data set is from Kaggle, the "Commodity Futures Price History". It is available here: </br>
https://www.kaggle.com/datasets/mattiuzc/commodity-futures-price-history

## Methodology
### Exploratory Data Analysis
The lumber future price history is read into a pandas dataframe. It was processed and checked, and data before 2008, after 2020 are discarded due to missing data or extreme volatility. Log return is then added to the dataframe, along with the close price.

### Train test split
The first 90% of the time series data is used as training data, followed by 5% as validation, 5% as test data.

### Feature Engineering
To allow LSTM model to better capture temporal patterns and dependencies, a rolling window is introduced in the input data. In the prelimiary model of rolling windows of 3 days is introduced to input data set X. Our target, remains as the close price of lumber futures at particular day.

### Model Training
A simple model consists of an input layer, an LSTM layer serving as the first hidden layer, a dense layer with 32 units and ReLU activation as the second hidden layer, and an output layer, was first constructed. It has successfully predicted the val set with mean-squared-error of ~66.6.

Afterwards, we used GridSearchCV to optimize the hyperparameters, and it was found that the best model has the following parameters:</br>
n = 5</br>
Layers = 1</br>
No. of nodes = 16</br>

We then further introduced dropout to the model, trying to mitigate the overfitting issue. The final model has input layer, LSTM layer with 16 nodes, dense layer with 16 nodes (relu), dropout layer of 0.1, and output layer.

## Conclusion
For the final model with dropout, the validation MSE remains nearly unchanged at 65, compared with other models we have built. The test MSE is 77.7, which is slightly lower than our initial trial of 79.3.</br>
To further lower the error, we may train with the followings:
1. Getting a time series of shorter time frame, from daily(what we have in this model) to hours/minutes/seconds.
2. Further feature engineering, like varying the length of rolling window.
3. Adding additional raw data for analysis, like volume.

The LSTM model showcased here serves as an instructive exercise in utilizing advanced techniques to predict future stock/commodity prices. However, it is vital to acknowledge the intricacies of the market and the presence of investment banks and quantitative funds employing sophisticated algorithms for trading. It is unrealistic to harbor the belief that constructing a model alone can easily outperform these established players. It is crucial to approach such endeavors with a realistic perspective, recognizing the challenges involved, rather than expecting immediate financial gains.



