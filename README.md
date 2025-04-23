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

(5, 162)
|    Aatrox |      Ahri |     Akali |    Akshan |    Alistar |      Amumu |    Anivia |     Annie |   Aphelios |      Ashe |   Aurelion Sol |      Azir |      Bard |   Bel'Veth |   Blitzcrank |   Brand |      Braum |   Caitlyn |   Camille |   Cassiopeia |   Cho'Gath |     Corki |    Darius |     Diana |   Dr. Mundo |    Draven |    Ekko |     Elise |   Evelynn |    Ezreal |   Fiddlesticks |   Fiora |   Fizz |     Galio |   Gangplank |     Garen |      Gnar |   Gragas |    Graves |      Gwen |   Hecarim |   Heimerdinger |   Illaoi |    Irelia |    Ivern |      Janna |   Jarvan IV |       Jax |     Jayce |      Jhin |      Jinx |   K'Sante |    Kai'Sa |   Kalista |    Karma |   Karthus |   Kassadin |   Katarina |     Kayle |      Kayn |    Kennen |   Kha'Zix |   Kindred |      Kled |   Kog'Maw |   LeBlanc |   Lee Sin |      Leona |    Lillia |   Lissandra |    Lucian |     Lulu |     Lux |   Malphite |   Malzahar |    Maokai |   Master Yi |   Miss Fortune |   Mordekaiser |   Morgana |      Nami |      Nasus |   Nautilus |   Neeko |   Nidalee |     Nilah |   Nocturne |   Nunu & Willump |      Olaf |   Orianna |    Ornn |   Pantheon |   Poppy |      Pyke |    Qiyana |     Quinn |      Rakan |   Rammus |   Rek'Sai |       Rell |   Renata Glasc |   Renekton |    Rengar |     Riven |    Rumble |      Ryze |    Samira |   Sejuani |     Senna |   Seraphine |    Sett |     Shaco |       Shen |   Shyvana |    Singed |      Sion |     Sivir |   Skarner |       Sona |     Soraka |     Swain |   Sylas |    Syndra |   Tahm Kench |   Taliyah |     Talon |      Taric |   Teemo |     Thresh |   Tristana |    Trundle |   Tryndamere |   Twisted Fate |    Twitch |      Udyr |     Urgot |     Varus |   Vayne |    Veigar |   Vel'Koz |       Vex |        Vi |     Viego |    Viktor |   Vladimir |   Volibear |   Warwick |   Wukong |     Xayah |    Xerath |   Xin Zhao |     Yasuo |      Yone |    Yorick |      Yuumi |       Zac |       Zed |      Zeri |      Ziggs |     Zilean |      Zoe |     Zyra |
|----------:|----------:|----------:|----------:|-----------:|-----------:|----------:|----------:|-----------:|----------:|---------------:|----------:|----------:|-----------:|-------------:|--------:|-----------:|----------:|----------:|-------------:|-----------:|----------:|----------:|----------:|------------:|----------:|--------:|----------:|----------:|----------:|---------------:|--------:|-------:|----------:|------------:|----------:|----------:|---------:|----------:|----------:|----------:|---------------:|---------:|----------:|---------:|-----------:|------------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|---------:|----------:|-----------:|-----------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|-----------:|----------:|------------:|----------:|---------:|--------:|-----------:|-----------:|----------:|------------:|---------------:|--------------:|----------:|----------:|-----------:|-----------:|--------:|----------:|----------:|-----------:|-----------------:|----------:|----------:|--------:|-----------:|--------:|----------:|----------:|----------:|-----------:|---------:|----------:|-----------:|---------------:|-----------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|------------:|--------:|----------:|-----------:|----------:|----------:|----------:|----------:|----------:|-----------:|-----------:|----------:|--------:|----------:|-------------:|----------:|----------:|-----------:|--------:|-----------:|-----------:|-----------:|-------------:|---------------:|----------:|----------:|----------:|----------:|--------:|----------:|----------:|----------:|----------:|----------:|----------:|-----------:|-----------:|----------:|---------:|----------:|----------:|-----------:|----------:|----------:|----------:|-----------:|----------:|----------:|----------:|-----------:|-----------:|---------:|---------:|
|   0       |   2       |   8       | nan       | nan        | nan        | nan       | nan       |    4.16773 |   3.12052 |      nan       |   4.66667 | nan       |  nan       |      2       |   8     |   2        |   4.74827 | nan       |      5       |    2.125   |   0       |  13       | nan       |     1       |   4.93967 | 6       | nan       |  nan      |   3.62478 |        nan     |     2   |    nan |   3       |   nan       | nan       | nan       | 0        |   3       | nan       |   7       |        1.93333 |  nan     |   8       | 0.333333 | nan        |    3        | nan       | nan       |   4.07779 |   4.38336 | nan       |   5.26383 |   4.8437  | 1.07692  |   3.4     |  nan       |  nan       | nan       | nan       | nan       | nan       |   6.66667 | nan       |   3.80925 |  nan      |   4.5     |   0.5      | nan       |   nan       |   4.9554  | 1.5      | 3.4     |    1       |  nan       | nan       |      nan    |        4.38657 |     nan       |   4       |   1       |   1.5      |   1        | 1       | nan       |   4.25641 |  nan       |        nan       |   2       | nan       | 2.5     |   nan      | 4       | nan       | nan       | nan       | nan        |   nan    |  nan      | nan        |       0.5      |    1.5     |   4       | nan       | nan       |   9       |   5.22807 |  0.666667 |   2.73188 |     2.22156 | 1.66667 | nan       | nan        | nan       | nan       |   2.09091 |   4.16545 | nan       |   6        |   0.730769 |   2.27586 | 6.66667 |   3.04    |     1.88462  |   4.875   | nan       | nan        |     nan | nan        |    4.29412 | nan        |    nan       |        0       |   5.00907 | nan       | nan       |   4.21626 | 4.63636 |   3.69697 |       1   | nan       | nan       |   1       |   3.25    |    2       |  nan       |       nan |  3.33333 |   4.03059 |   4.22222 |     5.5    |   3.67857 | nan       | nan       |   1        | nan       |   5.33333 |   4.59615 |   2.8      |   1        | nan      | nan      |
| nan       |   3       | nan       | nan       | nan        |   1.75     | nan       | nan       |  nan       | nan       |      nan       | nan       | nan       |    4.14348 |      2.25    | nan     | nan        |  13       | nan       |    nan       |  nan       | nan       |   5       |   3.30363 |     1.25    | nan       | 3.77778 |   3.74194 |    5.2963 |   8       |          1.875 |     2   |    nan | nan       |     3       | nan       | nan       | 2.77922  |   4.19438 |   3.77824 |   3.09524 |      nan       |    3     |   6       | 0.866667 |   2        |    2.25784  |   3       | nan       |  10       | nan       | nan       | nan       | nan       | 3.66667  |   4.43919 |  nan       |  nan       | nan       |   4.02439 | nan       |   4.16854 |   4.64474 | nan       | nan       |  nan      |   3.21508 | nan        |   3.2375  |   nan       | nan       | 3        | 2.5     |    1       |  nan       |   1.88235 |        6.25 |        2       |       2.8     |   2.33333 | nan       | nan        | nan        | 7       |   4.32787 | nan       |    2.86392 |          2.17647 |   3.432   | nan       | 1       |     3.9322 | 1.88823 | nan       |   4.15517 | nan       | nan        |     2.75 |    4.1358 | nan        |     nan        |  nan       |   5.22857 |   8       |   4.78947 | nan       | nan       |  2.0687   | nan       |     2       | 0.5     |   3.71429 |   0        |   3.53704 |   1       | nan       | nan       |   1.35714 | nan        | nan        | nan       | 4.75    | nan       |   nan        |   4.20408 |   3.90385 |   1.5      |       3 | nan        |   14       |   2.40708  |      2.5     |      nan       | nan       |   2.37812 |   2.5     | nan       | 0       | nan       |       1   |   5       |   2.59236 |   3.68004 | nan       |  nan       |    2.40994 |       nan |  3.25393 | nan       | nan       |     2.6307 | nan       | nan       | nan       | nan        |   2.57143 |   4.4     |   4.5     | nan        | nan        | nan      | nan      |
|   5.28    |   3.64047 |   4.86403 |   4.37143 | nan        | nan        |   3.40426 |   4.07692 |    3.5     | nan       |        4.16667 |   3.17752 | nan       |  nan       |    nan       |   3.125 | nan        |   7       |   4.25    |      4.27027 |    3.5     |   3.77832 |   7       |   3.7     |     1.66667 |   4.5     | 4.13333 | nan       |  nan      |   3.92308 |        nan     |     3.5 |      3 |   2.56189 |     4.73333 | nan       |   1       | 2.33333  |   3.47368 |   4.91667 |   6       |        3.44444 |    4     |   4.25806 | 1.22727  |   0        |    4        | nan       |   3.77778 |   2       | nan       | nan       |   5.17391 |   4.33333 | 1.62019  |   4.63636 |    4.64103 |    5.14286 |   3.33333 |   5       |   3       | nan       | nan       |   3.4     |   3.39286 |    3.8247 |   2.5     | nan        |   6.6     |     2.26816 |   4.35965 | 0.538462 | 3       |    4       |    3.14286 | nan       |      nan    |      nan       |       4.5     |   3       | nan       |   4.44444  | nan        | 3.78947 | nan       | nan       |    2.625   |        nan       |   8       |   2.93387 | 1.29787 |     3.25   | 6       | nan       |   4.43478 |   1       |   0        |   nan    |  nan      | nan        |     nan        |    2.72263 | nan       |   3.5     |   4.21212 |   3.10563 | nan       |  1.66667  |   5       |     2.47603 | 2.70588 | nan       | nan        |   2       |   2.85714 |   2.13793 |   5.66667 | nan       |   0        |   0.458333 |   2.8694  | 4.02266 |   3.43284 |   nan        |   3.53219 |   5.06667 | nan        |       3 | nan        |    3.77011 |   1        |      4.23239 |        2.50677 | nan       |   9       |   4.5     |   4.15    | 5.33333 |   4.11832 |       3.7 |   3.77426 |   5       |   3.5     |   3.55048 |    4.33333 |    4       |       nan |  7       |   6       |   3.71667 |     3      |   3.49245 |   3.54449 | nan       |   3        |   1.5     |   5.26    |   4.46341 |   3.73913  |   1.62992  |   3.4661 | nan      |
| nan       | nan       | nan       | nan       |   0.643885 |   0.918067 | nan       | nan       |  nan       |   1.1     |      nan       |   4.33333 |   1.20122 |  nan       |      1.07273 |   6     |   0.533972 |   1       |   2.33333 |    nan       |    3.33333 | nan       | nan       | nan       |     1.5     | nan       | 5.5     | nan       |  nan      |   6       |        nan     |   nan   |    nan |   1.17347 |   nan       | nan       | nan       | 0.901961 | nan       | nan       | nan       |        1.55224 |  nan     | nan       | 1        |   0.446602 |    0.555556 |   2       | nan       | nan       | nan       | nan       | nan       | nan       | 0.926223 | nan       |  nan       |  nan       | nan       | nan       |   3       | nan       | nan       | nan       | nan       |  nan      |   4       |   0.737004 | nan       |   nan       |   1.5     | 0.644205 | 1.65528 |  nan       |  nan       |   1.04918 |      nan    |        2       |       4       |   1.08434 |   1.00727 |   0.846154 |   0.761435 | 1.66667 | nan       | nan       |  nan       |        nan       | nan       | nan       | 2.11111 |     2.2    | 1.2     |   3.33221 | nan       | nan       |   0.778568 |   nan    |  nan      |   0.746702 |       0.862745 |  nan       | nan       | nan       |   2.2     | nan       | nan       |  1.04762  |   2.27354 |     1.34272 | 1.47937 |   4       |   0.666667 | nan       |   0.5625  |   1.3913  |   4.5     | nan       |   0.826531 |   0.453125 |   2.5     | 2.42857 |   1.5     |     0.903129 |   1.5     | nan       |   0.605769 |     nan |   0.736006 |  nan       |   0.714286 |    nan       |      nan       |   8       | nan       | nan       |   3       | 3       |   2.5     |     nan   |   2       |   1.33333 | nan       |   4       |    2.5     |  nan       |       nan |  3.3125  | nan       |   3.6     |   nan      |   2.73333 |   5       | nan       |   0.872102 |   2.2     | nan       | nan       |   0.666667 |   0.639344 |   4.5    |   1.4375 |
|   2.99509 |   2.28571 |   4.49414 |   3.75188 | nan        | nan        |   0       |   4       |    7       | nan       |      nan       |   1.375   |   1.75    |    6       |    nan       | nan     | nan        | nan       |   3.38394 |      2.77778 |    2.74576 |   3.66667 |   4.74725 | nan       |     1.9375  |   2.75    | 2.66667 |   5       |  nan      | nan       |        nan     |     3.4 |    nan |   2       |     3.33383 |   3.66667 |   2.38078 | 1.63115  |   2.67831 |   3.17462 | nan       |        3.66667 |    4.625 |   3.89905 | 1        |   0.4      |    1.71429  |   3.15428 |   3.438   | nan       | nan       |   2.93333 |   0       |   8       | 0.979381 |   4.75    |  nan       |  nan       |   3.0814  |   1       |   2.69928 | nan       |   2       |   3.16667 | nan       |    6      |   3.14815 |   1        |   3.19672 |     3       |   4.59459 | 0.625    | 1       |    1.91176 |  nan       |   1.51485 |      nan    |      nan       |       3.48469 | nan       |   0       |   2.92683  |   2        | 4.14286 |   5       |  25       |    4       |        nan       |   4.14483 |   5       | 1.5516  |     3.5    | 2       | nan       |   9.5     |   4.14286 |   0        |     0.5  |  nan      | nan        |     nan        |    2.38095 |   1.83333 |   3.83516 |   3.82418 |   2.21429 |   2       |  1.95632  | nan       |     1       | 2.66552 |   3       |   1.93023  |   2.70732 |   2.83333 |   1.75813 | nan       | nan       | nan        |   0        |   2.51429 | 3.51887 | nan       |     1.58333  | nan       | nan       |   0.5      |       4 | nan        |    4.75    |   2.47619  |      3.87778 |      nan       | nan       |   2.84615 |   3.47368 |   4       | 4.55882 |   4.5     |     nan   |   0       |   5       |   3       |   2.84615 |    3.23288 |    2.61818 |         6 |  2.96732 | nan       | nan       |     2.6    |   3.3913  |   3.43478 |   1.61538 | nan        |   1.88889 | nan       |   4.85    |   6        |   1.05556  | nan      | nan      |

#### Imputation


## Framing a Prediction Problem


## Baseline Model


## Final Model