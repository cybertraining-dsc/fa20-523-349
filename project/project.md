# TBD

- [ ] please use our template as posted in piazza
- [ ] please leanr markdown
- [ ] please add refernces

Jiayu Li

## Introduction

Rank Forecasting in Car Racing.
Indy500 is the premier event of the IndyCar series. Each year, 33 cars compete on a 2.5-mile oval track for 200 laps. 
The track is split into several sections or timeline. E.g., SF/SFP indicate the start and finish line on the track or on the pit lane, respectively.
A local communication network broadcasts race information to all the teams, following a general data exchange protocol\cite{IndyCar_Understanding_nodate}.

## Dataset

We select races of superspeedway after 2013 with at least 5 years data each, and after removing corrupted data, get a dataset of 25 races from four events.
Among all the events, Indy500 is the most dynamic one which has both the largest PitLapsRatio and RankChangesRatio, Iowa is the least. 

We will train models separately for each event. Races of the first five years are used as the training dataset, the remains are used as testing data. Since Pocono has only five years of data in total, its training set uses four of them. 
First, we start from Indy500 and use Indy500-2018 as validation set. Then we investigate the generalization capability of the model on data of the other events.

## Plan

We will use a variety of time series forecasting models to make forecasts and compare the differences between different models.

## Refernces

TBD
