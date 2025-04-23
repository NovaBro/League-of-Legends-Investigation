# League-of-Legends-Investigation

## Introduction

<!-- Provide an introduction to your dataset, and clearly state the one question your project is centered around. Why should readers of your website care about the dataset and your question specifically? Report the number of rows in the dataset, the names of the columns that are relevant to your question, and descriptions of those relevant columns. -->
League of Legends (LoL) is perhaps one of the most popular and well know Massive Multiplayer Online Battle Arena (MoBA). This game is played across the world, and has a major South Korea, North America, and Europen pressence. The game premise is very simple, there are two teams with 5 players each, and the objective is destroy your opposing team's base. However, there are many intricacies to the game (such as, champion diversity, items, objectives, etc) that make predicting the winner of games very challeging! Just watch any esports event on LoL, and you will find how deep the game really goes.

The purpose of this investigation is to answer: Is it possible to predict the outcome of the game, based on a variety of stats collected during the game? In particular, from looking at the stats (gold, cs, exp) across time?

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


## Data Cleaning and Exploratory Data Analysis

#### Data Cleaning
As mentioned previously, some rows represent the team summary, which we need to remove. This ends up leaving us 125480 rows, which is 12548 games!

The results column did not have any missing values. However, the stats listed above (goldat*, xpat*, and csat*), had a significant amounts of missing values. This makes sense, as games can end quicker than 25 minutes. We will resolve the missing data in the imputation step later.

| Column Name | Number of Missing Values |
| --- | --- |
|goldat10   |     18920|
|xpat10     |     18920|
|csat10     |     18920|
|goldat15   |     18920|
|xpat15     |     18920|
|csat15     |     18920|
|goldat20   |     19300|
|xpat20     |     19300|
|csat20     |     19300|
|goldat25   |     25610|
|xpat25     |     25610|
|csat25     |     25610|

#### Univariate
 <iframe
 src="assets/goldat10_hist.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

 Gold has a huge impact on the game, as it what determines what items you can buy. From the observed graph, we can see that there two distributions of gold at 10 minutes, which suggests that gold distribution is effected by other factors. 


#### Bivariate
 <iframe
 src="assets/goldat10vsChamp.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

 <iframe
 src="assets/goldat25vsChamp.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

 As we can see from both of the graphs aboves, typical support champions, such as Leona, earn less gold. Even as the game progresses (at 10 minutes vs at 25), it seems as though supports still lag behind in gold. 


#### Aggragate 
Looking at a small subset of the champions, we see the following.

| position   |       Rell |    Darius |    Ekko |
|-----------|-----------|----------|--------|
| bot        | nan        |  13       | 6       |
| jng        | nan        |   5       | 3.77778 |
| mid        | nan        |   7       | 4.13333 |
| sup        |   0.746702 | nan       | 5.5     |
| top        | nan        |   4.74725 | 2.66667 |

Some champions are played in multiple roles. It would be interesting to see if there are ways to find 'off meta' picks for certain roles that might give teams an edge. Values that are whole numbers, are likely due to a champion played once in that role. Nan values are because no one has played that champion for that roll. Rell, for example, is only played support. This table also gives a window on how deadly certain champs are. Darius has on average, 13 kills in the top lane, which is very high!

#### Imputation
In order to know get a better understanding of which condition to inpute the data, it is helpful to graph the data we are working with.

 <iframe
 src="assets/goldat10nosup_dist.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

This graph gives a good indication that the gold income is indeed dependent on position. 

 <iframe
 src="assets/imputation_compare.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

First, I tried figuring out what condition would be the best, which I think would come down to either the champion chosen, or the position. Thus, I compared the goldat stat across time for various champions. I found the distribution to vary more than that of the goldat stat across time for various positions.
A notible point is that many of the goldat stats across time, are bimodel. This is likely due to the fact that the support position recieves less gold than other roles, creating a separate bump in the distribution. Interestingly enough as well, looking at the xpat stat, you can see a trimodel distribution, with sup have the least, jng and bot tied, and top having the most xp.

After exploring imputation on position, I came to find that conditional probability on position to most closely follow the data before imputation. In fact, it is difficult to see the difference without closely zooming in on the graph to see the difference.

## Framing a Prediction Problem
The problem that I pose is a classification model. I want to see if it is possible to classify a team into two categories, a Win or a Lost state. The response variable is the match outcome, which is binary: either a Win or a Loss. I chose this because it is the most important final result of a game and can be used to evaluate team performance or strategy effectiveness. I am using the Accuracy metric since it measures the overall percentage of correct predictions (both wins and losses). It’s useful when classes are balanced (i.e., about the same number of wins and losses).

Through the game, each player has access to information on how much gold they collect, the amount of xp, and cs farmed. This is by definition of playing the game, and by access to these metrics through the player user interface. Thus, we would have access to this information to predict the outcome of the game. 

## Baseline Model


## Final Model