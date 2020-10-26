# Rank Forecasting in Car Racing

- [ ] please use our template as posted in piazza
- [ ] please leanr markdown
- [ ] please add refernces

Jiayu Li

## Abstract

## 1. Introduction

Rank Forecasting in Car Racing.
Indy500 is the premier event of the IndyCar series. Each year, 33 cars compete on a 2.5-mile oval track for 200 laps. 
The track is split into several sections or timeline. E.g., SF/SFP indicate the start and finish line on the track or on the pit lane, respectively.
A local communication network broadcasts race information to all the teams, following a general data exchange protocol\cite{IndyCar_Understanding_nodate}.

## 2. Background Research and Previous Work

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

[^1]: Valada A., Velagapudi P., Kannan B., Tomaszewski C., Kantor G., Scerri P. (2014) Development of a Low Cost Multi-Robot Autonomous Marine Surface Platform. In: Yoshida K., Tadokoro S. (eds) Field and Service Robotics. Springer Tracts in Advanced Robotics, vol 92. Springer, Berlin, Heidelberg. <https://doi.org/10.1007/978-3-642-40686-7_43>

[^2]: M. Ludvigsen, J. Berge, M. Geoffroy, J. H. Cohen, P. R. De La Torre, S. M. Nornes, H. Singh, A. J. Sørensen, M. Daase, G. Johnsen, Use of an Autonomous Surface Vehicle reveals small-scale diel vertical migrations of zooplankton and susceptibility to light pollution under low solar irradiance. Sci. Adv. 4, eaap9887 (2018). <https://advances.sciencemag.org/content/4/1/eaap9887/tab-pdf>


