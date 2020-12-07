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

**Keywords:** Time series forecasting, deep learning.

## 1. Introduction

Rank Forecasting in Car Racing.
Indy500 is the premier event of the IndyCar series. Each year, 33 cars compete on a 2.5-mile oval track for 200 laps. 
The track is split into several sections or timeline. E.g., SF/SFP indicate the start and finish line on the track or on the pit lane, respectively.
A local communication network broadcasts race information to all the teams, following a general data exchange protocol\cite{IndyCar_Understanding_nodate}.

## 2. Background Research and Previous Work
Indy500 is the premier event of the IndyCar series. Each year, 33 cars compete on a 2.5-mile oval track for 200 laps. The track is split into several sections or timeline. E.g., SF/SFP indicate the start and finish line on the track or on the pit lane, respectively.A local communication network broadcasts race information to all the teams, following a general data exchange.
![alt text](https://github.com/cybertraining-dsc/fa20-523-349/blob/main/project/figure/fig1.png)
In motorsports, a \textbf{pit stop} is a pause for refueling, new tires, repairs, mechanical adjustments, a driver change, a penalty, or any combination of them.Unexpected events happen in a race, including mechanical failures or a crash. Depending on the severity level of the event, sometimes it leads to a dangerous situation for other cars to continue the racing with high speed on the track. In these cases, a full course yellow flag rises to indicate the race entering a \textbf{caution laps} mode, in which all the cars slow down and follow a safety car and can not overtake until another green flag raised. 

## 3. Choice of Data-sets

We select races of superspeedway after 2013 with at least 5 years data each, and after removing corrupted data, get a dataset of 25 races from four events.
Among all the events, Indy500 is the most dynamic one which has both the largest PitLapsRatio and RankChangesRatio, Iowa is the least. 

We will train models separately for each event. Races of the first five years are used as the training dataset, the remains are used as testing data. Since Pocono has only five years of data in total, its training set uses four of them. 
First, we start from Indy500 and use Indy500-2018 as validation set. Then we investigate the generalization capability of the model on data of the other events.

## 4. Methodology
First, we have a naive baseline which assumes that the rank positions will not change in the future, denoted as CurRank. 
Secondly, We implement machine learning regression models as baselines that follow the ideas in \cite{tulabandhula_interactions_2014} which forecast changes of rank position between two consecutive pit stops, including RandomForest, SVM, and XGBoost that do pointwise forecast.
Thirdly, we test with four latest deep forecasting models as the choice of RankModel, including DeepAR(2017)\cite{salinas_deepar_2017}, DeepState(2018)\cite{rangapuram_deep_2018}, DeepFactor(2019)\cite{wang_deep_2019}, N-BEATS(2020)\cite{oreshkin_n-beats_2020}.
PitModel has three implementations. For example for RankNet, we have 1. RankNet-Joint is the model that train target with pit stop jointly without decomposition. 2. RankNet-Oracle is the model with ground truth TrackStatus and LapStatus as covariates input. It represents the best performance that can be obtained from the model given the caution and pit stop information for a race. 3. RankNet-MLP deploys a separate pit stop model, which is a multilayer perceptron(MLP) network with probability output, as in Fig.  

![alt text](https://github.com/cybertraining-dsc/fa20-523-349/blob/main/project/figure/fig4.png)

## 5. Inference
Table shows the evaluation results of two laps rank position forecasting. 
CurRank demonstrates good performance. 73\% leader prediction correct and 1.16 mean absolute error on Indy500-2019 indicates that the rank position does not change much within two laps. 

DeepAR is a powerful model but fails to exceed CurRank, which reflects the difficulty of this task that the patterns of the rank position variations are not easy to learn from history.
When adding an oracle PitModel, DeepAR-Oracle shows a 28\% improvement in MAE over CurRank. 
By adding further optimizations, RankNet-Oracle(which uses DeepAR as RankModel) achieves significantly better performance than CurRank, with 23\% better in Top1Acc and 51\% better in MAE. 
These results demonstrate the effectiveness of model decomposition and domain knowledge-based optimizations.

Comparing the four state-of-the-art deep forecasting models as the choice of RankModel, we find DeepAR and N-BEATS obtains similar performance, but the N-BEATS is limited in supporting covariates which prevents it to be adopted into RankNet. DeepState and DeepFactor demonstrate very poor forecasting performance on this problem. 
We speculate that the model assumption is critical to how well the model fits the problem. These four deep models are all capable of capturing global dependencies among multiple time series, but through different assumptions. N-BEATS and DeepAR do not introduce strong assumptions and learns similarity among time series through shared the same network in training all the time series. DeepState is a state-space model that assumes a linear-Gaussian transition structure and assumes the time series are conditional independent of the model parameters. DeepFactor, as a factor model, requires the data to be exchangeable time series and assumes to be able to explicitly model global dependency by line combination of global factors. As the car racing rank forecasting problem is challenging in its highly dynamic with complex global dependency among the cars, models with strong assumptions of the structure of the global dependency do not perform as well as the one with weaker assumptions. And also this is a data sparse problem, which prefers the model that can provide forecasts for items that have little history available, where DeepAR has advantages\cite{salinas_deepar_2017}.

Other machine learning models, and RankNet-Joint all failed to get better accuracy than CurRank.
RankNet-MLP, our proposed model, is not as good as RankNet-Oracle, but still able to exceed CurRank by 7\% in Top1Acc and 19\% in MAE. It also achieves more than 20\% improvement of accuracy on 90-risk when probabilistic forecasting gets considered. 
%Detailed comparsion are presented in apeedix~\ref{sec:appendix_performance_improve_shotterm}.
Evaluation results on PitStop Covered Laps, where pit stop occurs at least once in one lap distance, show the advantages of RankNet-MLP and Oracle come from their capability of better forecasting in these extreme events areas.

![alt text](https://github.com/cybertraining-dsc/fa20-523-349/blob/main/project/figure/table.png)


## 6. Conclusion
In this project, we use deep learning models to the challenging problem of modeling sequence data with high uncertainty and extreme events. With the IndyCar car racing data, we find that the model decomposition based on the cause-effect relationship is critical to improving the rank position forecasting performance. 
We compare several state-of-the-art deep forecasting models: DeepAR, DeepState, DeepFactors,and N-BEATS. The results show that they cannot perform well on the global dependency structure. 
Finally, we propose RankNet, a combination of the encoder-decoder network and a separate MLP network that capable of delivering probabilistic forecasting, to model the pit stop events and rank position in car racing. 
In this way, we incorporate domain knowledge to enhance the deep learning method.
Our proposed model achieves significantly better accuracy than baseline models in the rank position forecasting task. The advantages of needing less feature engineering efforts and providing probabilistic forecasting enable racing strategy optimizations. 
## 7. Acknowledgements

The author would like to thank Dr. Gregor Von Laszewski, Dr. Geoffrey Fox, and the associate instructors in the *FA20-BL-ENGR-E534-11530: Big Data Applications* course (offered in the Fall 2020 semester at Indiana University, Bloomington) for their continued assistance and suggestions with regard to exploring this idea and also for their aid with preparing the various drafts of this article.

## 8. References

[^1]: IndyCar Dataset.https://racetools.com/logfiles/IndyCar/. visited  on 04/15/2020

[^2]: M4 Competition.https://forecasters.org/resources/time-series-data/m4-competition/.

[^3]: Ding,  M.  Zhang,  X.  Pan,  M.  Yang,  and  X.  He.  Modeling  extremeevents  in  time  series  prediction.InProceedings  of  the  25th  ACMSIGKDD, pages 1114–1122, New York, NY, USA, 2019.

[^4]: N.  Oreshkin,  D.  Carpov,  N.  Chapados,  and  Y.  Bengio.   N-BEATS:Neural basis expansion analysis for interpretable time series forecasting.InProceedings  of  International  Conference  on  Learning  Representa-tions(ICLR), 2020.
