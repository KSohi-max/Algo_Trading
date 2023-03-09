# Algorithmic Trading_Machine Learning

The following provides an analysis of fine tuning a Machine Learning model for a basic Algorithmic Trading strategy to improve predictability of returns.

### Data

Dataset used in Algo Trading Machine Learning model is (OHLCV) data from Morgan Stanley Capital International (MSCI)–based emerging markets exchange-traded fund (ETF):
- date
- open
- high
- low
- close
- volume

Investments in emerging markets make up an important aspect of a well-diversified investment portfolio.

### Baseline Performance

A baseline performance of Algo Trading Machine Learning model was established:

![Baseline Actual v. Strategy Returns](https://github.com/KSohi-max/Algo_Trading/blob/main/Images/Baseline_ActualvStrategy_Ret.png)

Based on the plot above, the predictions seem to be good for the first two years but move further apart over the next three years. Acutal values seem to be below those predicted by the Strategy Returns.

### Tuning Baseline Algorithm

#### Increasing Training Data

First part of fine tuning exercise adjusted the training data (X, y).  `X_train` and `y_train` are establish based on dates using `training_begin` and `training_end`.  For this tuning exercise the `training_end` date's month `DateOffset` was varied from baseline 3 months to 7, 10, 24 and 60.  The best results were observed at 24 months based on the illustrated plot.

![24M_ActualvStrategy_Ret](https://github.com/KSohi-max/Algo_Trading/blob/main/Images/24M_ActualvStrategy_Ret.png)

With 24 Months of training data, the Actual and Strategy Returns seem to be alligned from mid-2017 to 2020.  In 2020 the Actual Returns decrease vs. Strategy Returns.  Given that 2020 + were exceptional years for any Machine Learning model, the results are better in terms of weighted average Precision and Accuracy.

#### Adjusting Rolling Window of `Long Window` for SMA

In second part of fine tuning exercise, both the `Short Window` and the `Long Window` were changed and tested.  The values of 2, 3, 5, 10, 20, 30 were tested for `Short Window` and the best results seem to be at the baseline value of 4.  The `Long Window` was tested for values of 60, 80, 90, 106, 109, 112, 120, 200 while keeping the `Short Window` at baseline of 4. The best result seen were bewteen 106 and 112.  That is, the Accuracy increased to 0.56 from 0.55. 

![LW109_ActualvStrategy_Ret](https://github.com/KSohi-max/Algo_Trading/blob/main/Images/LW109_ActualvStrategy_Ret.png)

In reviewing the plot, it is important to note that there wasn't as much impact on the alignment of Actual v. Strategy Returns compared to the change in training data but the gap between the two Returns has narrowed when compared to the baseline plot above.

#### Tuning for Best Returns

In the final part of tuning, a combination of both 24 Months training data and `Long Window` of 109 for SMA was used to plot the Actual vs. Strategy Returns.  

![LW10924M_ActualvStrategy_Ret](https://github.com/KSohi-max/Algo_Trading/blob/main/Images/LW10924M_ActualvStrategy_Ret.png)

The plot seems to be a significant improvement over the baseline plot but is similar to the 24 Month training data plot above.

#### New Machine Learning Classifier

For a new Machine Learning Classifier model trial, `AdaBoostClassifier` was used in place of `SVC Classifier`. The following is the plot for Actual v. Strategy Returns:

![AdaBoost_ActualvStrategy_Ret](https://github.com/KSohi-max/Algo_Trading/blob/main/Images/AdaBoost_ActualvStrategy_Ret.png)

With baseline parameters, AdaBoostClassifier did not improve the model.  Based on the plot, Actual Returns performed far better than the Strategy Returns.  I would not recommend `AdaBoostClassifier` over the baseline `SVC Classifier` for this Algo Trading model.

#### Conclusion

The fine tuning exercise indicates that training data seems to have a significant impact on the predictability of Algorithm Trading ML models. This is generally true for most models.  There can be some improvement from adjusting the SMA parameters but it seems to be minimal for this model.

Clearly, black swan events like the 2020 pandemic global lockdowns or 2008 financial crisis do not follow any predictive patterns. So it is difficult to train a ML model to predict the Strategy Returns for these periods of sudden events.  As the volatility in the market continues to persists based on inflation, interest rate increases, etc. it is now far more important to look at the fundamentals of a company before making any investment decisions. Algo Trading is only as good as the data it is trained on and most of that comes from past.
