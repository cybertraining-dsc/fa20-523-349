# Rank Forecasting in Car Racing

[![Check Report](https://github.com/cybertraining-dsc/fa20-523-349/workflows/Check%20Report/badge.svg)](https://github.com/cybertraining-dsc/fa20-523-349/actions)
[![Status](https://github.com/cybertraining-dsc/fa20-523-349/workflows/Status/badge.svg)](https://github.com/cybertraining-dsc/fa20-523-349/actions)
Status: final, Type: Project

- [ ] comments have been send to piazza

* Jiayu Li, fa20-523-349 
* [Edit](https://github.com/cybertraining-dsc/fa20-523-349/blob/master/project/project.md)

{{% pageinfo %}}

## Abstract

Rank forecasting in car racing is a challenging problem, which is featured with highly complex global dependency among the cars, with uncertainty resulted from existing exogenous factors, and as a sparse data problem. Existing methods, including statistical models, machine learning regression models, and several state-of-the-art deep forecasting models all perform not well on this problem. By elaborative analysis of pit stops events, we find it is critical to decompose the cause effects and model them, the rank position and pit stop events, separately. We propose RankNet, a combination of encoder-decoder network and separate MLP network that capable of delivering probabilistic forecasting to model the pit stop events and rank position in car racing. Further with the help of feature optimizations, RankNet demonstrates a significant performance improvement over the baselines.

Contents

{{< table_of_contents >}}

{{% /pageinfo %}}

**Keywords:** Time series forecasting, deep learning.

## 1. Introduction

Rank Forecasting in Car Racing.
Indy500 is the premier event of the IndyCar series. Each year, 33 cars compete on a 2.5-mile oval track for 200 laps. 
The track is split into several sections or timeline. E.g., SF/SFP indicate the start and finish line on the track or on the pit lane, respectively.
A local communication network broadcasts race information to all the teams, following a general data exchange protocol\cite{IndyCar_Understanding_nodate}.



## 2. Background Research and Previous Work

In many real-world applications, data is captured over the course of time, constituting a Time-Series. Time-Series often contain temporal dependencies that cause two otherwise identical points of time to belong to different classes or predict different behavior. This characteristic generally increases the difficulty of analysing them. 
The IndyCar Series is the premier level of open-wheel racing in North America. Computing System and Data analytics is critical to the game, both in improving the performance of the team to make it faster and in helping the race control to make it safer. IndyCar ranking prediction is a practical application of time series problems. We will use the LSTM model to analyze the state of the car, and then predict the future ranking of the car.

## 3. Choice of Data-sets

We select races of superspeedway after 2013 with at least 5 years data each, and after removing corrupted data, get a dataset of 25 races from four events.
Among all the events, Indy500 is the most dynamic one which has both the largest PitLapsRatio and RankChangesRatio, Iowa is the least. 

We will train models separately for each event. Races of the first five years are used as the training dataset, the remains are used as testing data. Since Pocono has only five years of data in total, its training set uses four of them. 
First, we start from Indy500 and use Indy500-2018 as validation set. Then we investigate the generalization capability of the model on data of the other events.
![alt text](https://raw.githubusercontent.com/cybertraining-dsc/fa20-523-349/main/project/images/fig3.png)

## 4. Methodology

Data preprocessing
The Multi-Loop Protocol is designed to deliver specific dynamic and static data that is set up and
produced by the INDYCAR timing system. This is accomplished by serially streaming data that is broken
down into different record sets. This information includes but is not limited to the following:

Completed lap results
Time line passing or crossing results
Completed section results
Current run or session information
Flag information
Track set up information including segment definitions
Competitor information
Announcement information


The INDYCAR MLP is based on the AMB Multi-Loop Protocol version 1.3. This document contains the
INDYCAR formats for specific fields not defined in the AMB document.

Record Description:

Every record starts with a header and ends with a CR/LF. Inside the record, the
fields are separated by a “broken bar” symbol 0xA6 (not to be confused with the pipe symbol 0x7C). The
length of a record is not defined and can therefore be more than 256 characters. The data specific to
each record Command is contained between the header and CR/LF.

Feature selection


The future ranking of a car is mainly affected by two factors:
One is its current position: the car that is currently leading has a greater probability of being ahead in the future; the other is the time of the last pit stop: because the fuel tank of each car is limited, Entering pit stop, the possibility of it leading in the future will be reduced.

Therefore, we choose the following characteristics to predict ranking:

The current position of each car (Lap and Lap Distance)
Time of the last Pit Stop of each car

Time series prediction problems are a difficult type of predictive modeling problem. Unlike regression predictive modeling, time series also adds the complexity of a sequence dependence among the input variables. A powerful type of neural network designed to handle sequence dependence is called recurrent neural networks. The Long Short-Term Memory network or LSTM network is a type of recurrent neural network used in deep learning because very large architectures can be successfully trained.


## 5. Inference

Table 2 shows the experimental results, which verify our hypothesis that the time series prediction model based on deep learning obtained the highest accuracy. Although the LSTM model achieves the highest accuracy, its advantages are not as obvious as RankNet. This is because the telemetry data of racing cars is non-public, and the data available for training are limited.

According to the experimental results in Table 6, we draw the following conclusions:
1. The LSTM model has higher accuracy in time series forecasting.
2. Limited by the size of the training data set (only the telemetry data for 2 games is available), the accuracy improvement obtained by LSTM is not as obvious as RankNet.


## 6. Conclusion

The prediction problem of racing cars has the characteristics of non-linearity, non-periodicity, randomness, and timing dependence. The traditional statistical learning model (Naive Bayes, SVM, Simple Neural Networks) is difficult to deal with the problem of time series prediction, since the model is unable to understand the time-series dependence of data. Traditional time series prediction models such as ARMA / ARIMA can only deal with linear time series with certain periodicity. The anomaly events and human strategies in the racing competition make these methods no longer applicable. Therefore, time series prediction models (RNN, GRU, LSTM, etc.) based on deep learning are more suitable for solving such problems.



## 7. Acknowledgements

The author would like to thank Dr. Gregor Von Laszewski, Dr. Geoffrey Fox, and the associate instructors in the *FA20-BL-ENGR-E534-11530: Big Data Applications* course (offered in the Fall 2020 semester at Indiana University, Bloomington) for their continued assistance and suggestions with regard to exploring this idea and also for their aid with preparing the various drafts of this article.

## 8. References

[^1]: IndyCar Dataset.https://racetools.com/logfiles/IndyCar/. visited  on 04/15/2020

[^2]: M4 Competition.https://forecasters.org/resources/time-series-data/m4-competition/.

[^3]: Ding,  M.  Zhang,  X.  Pan,  M.  Yang,  and  X.  He.  Modeling  extremeevents  in  time  series  prediction.InProceedings  of  the  25th  ACMSIGKDD, pages 1114–1122, New York, NY, USA, 2019.

[^4]: N.  Oreshkin,  D.  Carpov,  N.  Chapados,  and  Y.  Bengio.   N-BEATS:Neural basis expansion analysis for interpretable time series forecasting.InProceedings  of  International  Conference  on  Learning  Representa-tions(ICLR), 2020.

[^5]: C. L. W. Choo.   Real-time decision making in motorsports: analytics forimproving  professional  car  race  strategy, PhD  Thesis,  MassachusettsInstitute of Technology, 2015.

[^6]: T.  Tulabandhula.Interactions  between  learning  and  decision  making.PhD Thesis, Massachusetts Institute of Technology, 2014.

[^7]: D.Salinas, V. Flunkert, and  J. Gasthaus.DeepAR: Probabilisticforecasting with autoregressive recurrent networks.arXiv:1704.04110[cs, stat], Apr. 2017
