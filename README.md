# Time-Series-Analysis
Using a Seasonal ARIMA Model to Predict ISP Revenue

# Contents  
[Purpose](#Purpose)
[Method Justification](#Method Justification)

## Purpose

At a very high level, the upper-most tiers of leadership including the board of directors of an ISP may be interested in a quick summary of overall revenue trends. Seasonal fluctuations and possible predictions for future time periods should be available for such a broad measure after the first 2 years of operations.

An analyst or data scientist may begin their approach to such an insight driven task by asking themselves if there exists any periodic repetetiveness over time for overall revenue. During the first 2 years of operations is there a significant difference in the revenenue for Q2 from the other quarters or seasons? Perhaps a more interesting report would say whether revenue is expected to increase in future months. Crucial decisions regarding investor engagement and top-down reorganization of the company may impinge upon these results.

Method Justification
In addition to periodic fluctuation in revenue over time there may exist larger upward or downward trends over the 2 year span of available data. A smoothed out pattern of mean revenue could be plotted to help visualize this if that were the case. On the other hand, too much fluctuation on a smaller scale may indicate noise which could impeede efforts to make predictions. A machine learning model may place too much emphasis on this noise and result in overfitting on test data. A transformation to mitigate larger trends can ensure stationarity of time series data, while spectral decomposition can aid with reducing random noise. All these factors should be considered when building a predictive time series model.

Autocorrelation takes samples of times series data over the same time intervals and measures strength of correlation between them. An example of a single lag could be correlating one month of data with the previous month. When more previous months, or any lengths of time period are correlated the lag count increments by 1 for each successive interval. With more lag intervals there are more possibilities of interactions amongst sub-intervals, and autocorellation treats all of these. Partial autocorellation looks only at interactions between adjacent lags. (Abhishek, 2019) An Auto Regressive (AR) model uses partial auto-correlation, and yields an equation of the form:

Y(t) = B1 + M1Y(t-1) + M2Y(t-2) + ... + MpY(t-p),

where p is the lag order in the time series, and the Ms are the weights of lagged observations.

Moving Average (MA) treats errors in the lagged observations from AR. The resulting equation is of the same form as the one derived from partial autocorrelation.

Yt = B2 + w1E(t-1) + w2E(t-2) + ... + wqE(t-q) + Et.

Here the w's are weights of the error terms E, and q is the size of the moving window.

When AR and MA are combined the equations is:

Yt = (B1 + B2) + (M1Y(t-1) + ... + MpY(t-p))

           + (w1E(t-1) + w2E(t-2) + ... + wqE(t-q) + Et)
Another important feature of a time series to consider is the behavior of means and standard deviations within lagged intervals. One way that means may differ is if there are seasonal trends in the data. While the means within fall and winter months may not differ too much, the larger fall and winter means might. This indicates seasonality within the time series. Distributions amongnst intervals may also exist, which would indicate the MA error term is not constant. For a time series to be stationary the means and standard deviations of lagged samples need to be constant, and there should be no seasonality.

An Integrated ARMA (ARIMA) model mitigates moving means. This can be accomplished by taking the difference of successive lagged intervals, or perhaps using a log or other form of transform. Before ensuring the stationarity assumption and performing any transformation, it is imperitive to check for any missing values and deal with outliers.

