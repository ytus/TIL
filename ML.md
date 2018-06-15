# ML

## ARIMA error: `Cannot cast ufunc subtract output from dtype('float64') to dtype('int64') with casting rule 'same_kind'`

`statsmodels.tsa.arima_model.ARIMA` throws en error: `Cannot cast ufunc subtract output from dtype('float64') to dtype('int64') with casting rule 'same_kind'`

It means the timeseries is a list of integers, not floats. Cast it to floats first: 

> list(map(lambda i: float(i), ts))

## Tutorials, courses, books ...
* [This tutorial will teach you the main ideas of Unsupervised Feature Learning and Deep Learning.](http://ufldl.stanford.edu/tutorial/)
* [ML Cheatsheet](http://ml-cheatsheet.readthedocs.io/en/latest/index.html)
* [edX Machine Learning](https://www.edx.org/course/machine-learning-columbiax-csmm-102x-4)
* [Machine Learning: a Probabilistic Perspective](http://www.cs.ubc.ca/~murphyk/MLbook/)
* [Dive into Machine Learning](http://hangtwenty.github.io/dive-into-machine-learning/)

## Forecasting

📘🎓
* [Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/index.html)
* [Python for Data Analysis](https://github.com/wesm/pydata-book)
* [Online Statistics Education: An Interactive Multimedia Course of Study](http://onlinestatbook.com/2/index.html)
* [PennState STAT 510 -	Applied Time Series Analysis](https://onlinecourses.science.psu.edu/stat510/)
* [Engineering Statistics Handbook](https://www.itl.nist.gov/div898/handbook/index.htm)
* [Forecasting: principles and practice](https://www.otexts.org/fpp/)
* [Forecasting: principles and practice - second edition](https://otexts.org/fpp2/)
* [Vincent Zoonekynd - Time series](http://zoonek2.free.fr/UNIX/48_R/15.html)
* [ARIMA models for time series forecasting](https://people.duke.edu/~rnau/411arim.htm#ses)

📄
* [Anomaly.io](https://anomaly.io/blog/)
* [Holt-Winters Forecasting for Dummies](https://grisha.org/blog/2016/01/29/triple-exponential-smoothing-forecasting/)
* [Demand forecasting](http://warwickdf.weebly.com/menu.html)
* [Methods for Intermittent Demand Forecasting](http://www.lancaster.ac.uk/pg/waller/pdfs/Intermittent_Demand_Forecasting.pdf)
* [From Holt-Winters to ARIMA Modelling](https://www.ons.gov.uk/ons/guide-method/ukcemga/publications-home/publications/archive/from-holt-winters-to-arima-modelling--measuring-the-impact-on-forecasting-errors-for-components-of-quarterly-estimates-of-public-service-output.pdf)
* [BOARD Enterprise Analytics Modelling (BEAM)](https://www.board.com/sites/default/files/learn/pdf/BOARD_BEAM_EN_1602_WEB.pdf)
* [Wikipedia - Predictive modelling](https://en.wikipedia.org/wiki/Predictive_modelling)
* [Avoiding Common Mistakes with Time Series](https://svds.com/avoiding-common-mistakes-with-time-series/)
* [Forecasting at Scale (Facebook Prophet)](https://peerj.com/preprints/3190.pdf)
* [A Guide to Time Series Forecasting with ARIMA in Python 3](https://www.digitalocean.com/community/tutorials/a-guide-to-time-series-forecasting-with-arima-in-python-3)

💾
* [StatsModels](http://www.statsmodels.org/0.6.1/examples/index.html)
* [The X-13ARIMA-SEATS Seasonal Adjustment Program](https://www.census.gov/srd/www/x13as/)
