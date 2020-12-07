# Rank Forecasting in Car Racing

[![Check Report](https://github.com/cybertraining-dsc/fa20-523-349/workflows/Check%20Report/badge.svg)](https://github.com/cybertraining-dsc/fa20-523-349/actions)

- [ ] Gregor fixed template
- [ ] please leanr markdown
- [ ] refernces are not cited in text
- [ ] background missing
- [ ] what is progress?
- [ ] Please add keywords (Vibhatha)
- [ ] Also add content to the missing topics (Vibhatha)

* Jiayu Li, fa20-523-349 
* [Edit](https://github.com/cybertraining-dsc/fa20-523-349/blob/master/project/project.md)

{{% pageinfo %}}

## Abstract

Rank forecasting in car racing is a challenging problem, which is featured with highly complex global dependency among the cars, with uncertainty resulted from existing exogenous factors, and as a sparse data problem. Existing methods, including statistical models, machine learning regression models, and several state-of-the-art deep forecasting models all perform not well on this problem. By elaborative analysis of pit stops events, we find it is critical to decompose the cause effects and model them, the rank position and pit stop events, separately. We propose RankNet, a combination of encoder-decoder network and separate MLP network that capable of delivering probabilistic forecasting to model the pit stop events and rank position in car racing. Further with the help of feature optimizations, RankNet demonstrates a significant performance improvement over the baselines.

Contents

{{< table_of_contents >}}

{{% /pageinfo %}}

**Keywords:** TBD.

## 1. Introduction

Rank Forecasting in Car Racing.
Indy500 is the premier event of the IndyCar series. Each year, 33 cars compete on a 2.5-mile oval track for 200 laps. 
The track is split into several sections or timeline. E.g., SF/SFP indicate the start and finish line on the track or on the pit lane, respectively.
A local communication network broadcasts race information to all the teams, following a general data exchange protocol\cite{IndyCar_Understanding_nodate}.

## 2. Background Research and Previous Work
Indy500 is the premier event of the IndyCar series. Each year, 33 cars compete on a 2.5-mile oval track for 200 laps. The track is split into several sections or timeline. E.g., SF/SFP indicate the start and finish line on the track or on the pit lane, respectively.A local communication network broadcasts race information to all the teams, following a general data exchange.

In motorsports, a \textbf{pit stop} is a pause for refueling, new tires, repairs, mechanical adjustments, a driver change, a penalty, or any combination of them.Unexpected events happen in a race, including mechanical failures or a crash. Depending on the severity level of the event, sometimes it leads to a dangerous situation for other cars to continue the racing with high speed on the track. In these cases, a full course yellow flag rises to indicate the race entering a \textbf{caution laps} mode, in which all the cars slow down and follow a safety car and can not overtake until another green flag raised. 

## 3. Choice of Data-sets

We select races of superspeedway after 2013 with at least 5 years data each, and after removing corrupted data, get a dataset of 25 races from four events.
Among all the events, Indy500 is the most dynamic one which has both the largest PitLapsRatio and RankChangesRatio, Iowa is the least. 

We will train models separately for each event. Races of the first five years are used as the training dataset, the remains are used as testing data. Since Pocono has only five years of data in total, its training set uses four of them. 
First, we start from Indy500 and use Indy500-2018 as validation set. Then we investigate the generalization capability of the model on data of the other events.

## 4. Methodology

## 5. Inference

## 6. Conclusion

## 7. Acknowledgements

The author would like to thank Dr. Gregor Von Laszewski, Dr. Geoffrey Fox, and the associate instructors in the *FA20-BL-ENGR-E534-11530: Big Data Applications* course (offered in the Fall 2020 semester at Indiana University, Bloomington) for their continued assistance and suggestions with regard to exploring this idea and also for their aid with preparing the various drafts of this article.

## 8. References

[^1]: IndyCar Dataset.https://racetools.com/logfiles/IndyCar/. visited  on 04/15/2020

[^2]: M4 Competition.https://forecasters.org/resources/time-series-data/m4-competition/.

[^3]: Ding,  M.  Zhang,  X.  Pan,  M.  Yang,  and  X.  He.  Modeling  extremeevents  in  time  series  prediction.InProceedings  of  the  25th  ACMSIGKDD, pages 1114–1122, New York, NY, USA, 2019.

[^4]: N.  Oreshkin,  D.  Carpov,  N.  Chapados,  and  Y.  Bengio.   N-BEATS:Neural basis expansion analysis for interpretable time series forecasting.InProceedings  of  International  Conference  on  Learning  Representa-tions(ICLR), 2020.
