# League-of-Legends-Investigation

## Introduction

<!-- Provide an introduction to your dataset, and clearly state the one question your project is centered around. Why should readers of your website care about the dataset and your question specifically? Report the number of rows in the dataset, the names of the columns that are relevant to your question, and descriptions of those relevant columns. -->
League of Legends (LoL) is perhaps one of the most popular and well know Massive Multiplayer Online Battle Arena (MoBA). This game is played across the world, and has a major South Korea, North America, and Europen pressence. The game premise is very simple, there are two teams with 5 players each, and the objective is destroy your opposing team's base. However, there are many intricacies to the game (such as, champion diversity, items, objectives, etc) that make predicting the winner of games very challeging! Just watch any esports event on LoL, and you will find how deep the game really goes.

The purpose of this investigation is to answer: Is it possible to predict the outcome of the game, based on a variety of stats collected during the game?

The dataset I will be using comes from Oracle Elixer, which where you can find statistics and data on previous pro league games. The dataset collects a variety of different of information from each game. For this investigation, I will be using the "2022_LoL_esports_match_data_from_OraclesElixir.csv" dataset.
[Details on Dataset Definitions](https://oracleselixir.com/definitions)

However, from looking at the dataset myself, sometimes, the names of the columns do not match exactly with those listed on the website. However, sometimes the labels are self explanitory.

Each game in the dataset is represented as 12 row, with two of the rows containing a summary for each team. Ten of the rows represents a player on either team (team size is 5).
There are 150588 rows and 161 columns.

That is a alot of data, but we are only interested in a subset of the data. Namely the player rows and :

| Column Name | Definition |
| --- | --- |
| result | Value can be 1 or 0, which indicates if a player or team has won (1) or loss (0). |
| goldat* | The total gold a player has **at** time *, which can be 10, 15, 20, or 25 minutes in this dataset. |
| xpat* | The total eXperience Points (XP) a player has **at** time *, which can be 10, 15, 20, or 25 minutes in this dataset.  |
| csat* | The total Creep Score (CS) a player has **at** time *, which can be 10, 15, 20, or 25 minutes in this dataset. This keeps track of how many minions, jungles monsters, and other creatures the player has killed. |

### Question:
<!-- In other words, is it possible to predict the games outcome at 15 minutes? If so, how much can we be sure? -->
In other words, what champions snow ball the most in the early game? Does their early lead result into wins?


## Data Cleaning and Exploratory Data Analysis


## Framing a Prediction Problem


## Baseline Model


## Final Model