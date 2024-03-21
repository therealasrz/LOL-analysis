# League of Legends FirstBlood Statistical Analysis

League of Legends FirstBlood Statistical Analysis is a comprehensive data science project conducted at UCSD. The project encompasses various stages of analysis, starting from exploratory data analysis to hypothesis testing, creation of baseline models, and concluding with fairness analysis. The primary focus of the project is to investigate the significance of the "first blood" event in League of Legends matches and its impact on match statistics and outcomes.

Authors: Sirui Zhang, Jingxiao Qiu

## Introduction
### General Introduction
League of Legends (LOL) is a popular multiplayer online battle arena (MOBA) game developed by Riot Games. With millions of players worldwide, it has become one of the most influential and widely played esports in the gaming industry. The data set we will be working with is a professional data set that’s developed by Oracle's Elixir. The file records match data from professional LOL esports gaming matches throughout 2022. 

This dataset captures key gameplay statistics and outcomes from a collection of LOL matches, offering a rich source of information for understanding player behavior, team dynamics, and match outcomes. It includes a variety of features such as individual player performance, team strategies, in-game statistics, and overall match dynamics.

In the realm of League of Legends (LOL), the concept of **"first blood"** holds significant weight and serves as an important trajectory of a match. First blood refers to the initial first kill secured by a team during the early stages of a game. Beyond its immediate impact on the scoreboard, first blood sets the tone for the ensuing gameplay, often shaping the general dynamics, strategies, and outcomes of the match.

The central question we are interested in is **Does the occurrence of the first blood influence the probability of winning a League of Legends match?** We want to use data analysis techniques to testify the impact of first blood on gaming statistics,  including individual player performance, team strategies, in-game metrics, and ultimately, match outcomes. 

### Introduction of Columns
The dataset introduces a comprehensive array of columns featuring gameplay metrics and match outcomes from professional League of Legends esports matches. Here's an introduction to some of the key columns:
In the dataset provided, we encounter various columns that encapsulate essential gameplay statistics and match outcomes from professional League of Legends (LoL) esports matches. Here's a brief introduction to each of these columns:

- `gameid`: This column represents a unique identifier for each individual match played. It allows us to distinguish between different matches in the dataset.

- `side`: The 'side' column denotes the team affiliation of a particular player or team. It typically distinguishes between 'blue' and 'red' teams.

- `result`: This column indicates the outcome of a match for a specific team or player. It may denote whether the team won, lost, or if the match ended in a draw.

- `kills`: The 'kills' column quantifies the number of enemy champions a player or team successfully eliminated during the match. 

- `deaths`: Conversely, the 'deaths' column records the number of times a player or team was eliminated by enemy champions. 

- `assists`: The 'assists' column records the number of assists credited to a player or team, indicating instances where they contributed to eliminating an enemy champion without securing the kill themselves.

- `firstblood`: This binary column indicates whether the occurrence of the first blood event took place in the match. First blood refers to the first instance of a player or team securing a kill in the game.

- `firstbloodkill`: Similar to 'firstblood', this binary column specifically denotes whether a player or team secured the first kill of the match, thereby earning the distinction of 'first blood.'

- `monsterkills`: the number of monsters or neutral objectives slain by a team or player during a game. These monsters can include jungle camps, epic monsters like Baron Nashor or the Dragon, as well as other neutral objectives such as Rift Herald or elemental drakes. The number of monster kills can be indicative of a team's control over the map, their ability to secure key objectives, and their overall dominance in the game.

- `position`: The 'position' column specifies the role or position played by an individual player within their team composition. Common positions include 'top,' 'jungle,' 'mid,' 'bot,' and 'support.'

- `minionkills`: This column records the number of minions or neutral monsters slain by a player or team during the match. It reflects their ability to efficiently farm gold and experience points, crucial for character progression and itemization.

- `league`: The 'league' column denotes the specific league tournament in which the match took place.

## Data Cleaning and Exploratory Data Analysis
### Data Cleaning
To save time in the further data cleaning steps, we first only keep the relevant columns: `gameid`, `side`, `result`, `kills`, `deaths`, `assists`, `firstblood`, `firstbloodkill`, `monsterkills`, `position`, `minionkills`, `league`. In this dataset, each game has 12 rows, with 10 rows representing each of the players (i.e. player rows), and 2 rows for summarizing the overall team performance and result (i.e. team rows). We decide to keep all these rows, as they will be both utilized in the further analysis.

Furthermore, among these columns, we find out that the column `minionkills` have some missing values, and specifically there is one game that has all `minionkills` entries as missing. Since there are still many other games in the dataset, we decide to simply drop this specific game. Moreover, the rest of the missing values in `minionkills` are all coming from team rows. We write a helper function to impute these missing values by the total number of minions killed in that team in order to make it consistent with other non-missing values. 

Below is the head of our league_clean dataframe.

| gameid                | side   |   result |   kills |   deaths |   assists |   firstblood |   firstbloodkill |   monsterkills | position   |   minionkills | league   |
|:----------------------|:-------|---------:|--------:|---------:|----------:|-------------:|-----------------:|---------------:|:-----------|--------------:|:---------|
| ESPORTSTMNT01_2690210 | Blue   |        0 |       2 |        3 |         2 |            0 |                0 |             11 | top        |           220 | LCKC     |
| ESPORTSTMNT01_2690210 | Blue   |        0 |       2 |        5 |         6 |            1 |                0 |            115 | jng        |            33 | LCKC     |
| ESPORTSTMNT01_2690210 | Blue   |        0 |       2 |        2 |         3 |            0 |                0 |             16 | mid        |           177 | LCKC     |
| ESPORTSTMNT01_2690210 | Blue   |        0 |       2 |        4 |         2 |            1 |                0 |             18 | bot        |           208 | LCKC     |
| ESPORTSTMNT01_2690210 | Blue   |        0 |       1 |        5 |         6 |            1 |                1 |              0 | sup        |            42 | LCKC     |

*Note: The cleaned dataset here consists of all the columns we will need for both **hypothesis testing** and **prediction model**. When we get into each of the specific parts above, we will adjust this DataFrame further to make it compliant to our necessary steps.

### Univariate Analysis
We permformed univariate analysis on the kill statistics in the dataset

<iframe
  src="assets/TotalTeamKills.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The histogram shows that the distribution of team kills is nearly normal, slightly right skewed. This suggests that the data is well-behaved, with team kills being distributed in a manner that is relatively balanced and typical for such gaming scenarios.

We also plot a graph for the dirstribution of monsterkills in the data set.

<iframe
  src="assets/MonHist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The histogram shows that the distribution of monsterkills is nearly normal. This suggests that the data is well-behaved, with monsterkills being distributed in a manner that is relatively balanced and serves as good statistics for analysing player behavior.

### Bivariate Analysis
We permformed bivariate analysis on the first blood and result statistics in the dataset to visualize the distribution of teams that wins with the first kill.

<iframe
  src="assets/PieChart.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

According to the plot, teams with first blood has a win rate about 60%. A 60% win rate implies that the majority of teams that secure the first blood end up winning the match, indicating that securing the first kill provides a strategic advantage that contributes to overall success.

### Interesting Aggregates
Here are some intersting aggregates to invest within the data set. 

|   firstblood |   result |   kills |   deaths |   assists |   team kpm |   minionkills |
|-------------:|---------:|--------:|---------:|----------:|-----------:|--------------:|
|            0 |     4873 |  159125 |   201307 |    360525 |    5032.85 |   1.84307e+07 |
|            1 |     7540 |  200452 |   158989 |    441953 |    6531.28 |   1.85042e+07 |

We first groupby the cleaned data set with firstblood status and then calculate the sum of all statistics. By comparing the gaming statistics with and without first blood. We had a better visualization about the difference in statistics for teams with and without firstblood. The team with first blood has a better statistics: more winning, kills assist, team damages, minionkills and less deaths.

## Assessment of Missingness
In this part, we are going to test if the missingness of `firstblood` column depends on other columns. The two other columns that we used are `league` and `result`. The significance level we choose for both permutation tests is 0.5, and the test statistic is Total Variance Distance (TVD).

First, we perform the permutation test on **firstblood** and **league**, and the missingness of **firstblood** does depend on **league**. 

Null Hypothesis: Distribution of **league** when **firstblood** is missing is the same as the distribution of **league** when **firstblood** is not missing.
Alternative Hypothesis: Distribution of **league** when **firstblood** is missing is NOT same as the distribution of **league** when **firstblood** is not missing.

Below is the observed distribution of **league** when **firstblood** is missing and not missing.

| league     |   fb_missing = False |   fb_missing = True |
|:-----------|---------------------:|--------------------:|
| CBLOL      |           0.0222936  |          0          |
| CBLOLA     |           0.0198165  |          0          |
| CDF        |           0.00669725 |          0          |
| CT         |           0.00238532 |          0          |
| DCup       |           0.00117737 |          0.0423542  |
| DDH        |           0.0191743  |          0          |
| EBL        |           0.0169725  |          0          |
| EL         |           0.0123853  |          0          |
| ESLOL      |           0.0222018  |          0          |
| EUM        |           0.0244954  |          0          |
| GL         |           0.0159633  |          0          |
| GLL        |           0.0186239  |          0          |
| HC         |           0.0148624  |          0          |
| HM         |           0.0140367  |          0          |
| IC         |           0.00688073 |          0          |
| LAS        |           0.0208257  |          0          |
| LCK        |           0.042844   |          0          |
| LCKC       |           0.0361468  |          0          |
| LCL        |           0.00146789 |          0          |
| LCO        |           0.0194495  |          0          |
| LCS        |           0.0280734  |          0          |
| LCSA       |           0.0495413  |          0          |
| LDL        |           0.0143884  |          0.517602   |
| LEC        |           0.0222936  |          0          |
| LFL        |           0.0226606  |          0          |
| LFL2       |           0.0221101  |          0          |
| LHE        |           0.0222936  |          0          |
| LJL        |           0.019633   |          0          |
| LJLA       |           0.00348624 |          0          |
| LLA        |           0.017156   |          0          |
| LMF        |           0.0292661  |          0          |
| LPL        |           0.0120183  |          0.432343   |
| LPLOL      |           0.0191743  |          0          |
| LVP SL     |           0.0224771  |          0          |
| MSI        |           0.00733945 |          0          |
| NEXO       |           0.0177064  |          0          |
| NLC        |           0.0351376  |          0          |
| PCS        |           0.0248624  |          0          |
| PGC        |           0.0515596  |          0          |
| PGN        |           0.0136697  |          0          |
| PRM        |           0.0336697  |          0          |
| SL (LATAM) |           0.0151376  |          0          |
| TAL        |           0.0188073  |          0          |
| TCL        |           0.0202752  |          0          |
| UL         |           0.0223853  |          0          |
| UPL        |           0.0377982  |          0          |
| VCS        |           0.029633   |          0          |
| VL         |           0.0155963  |          0          |
| WLDs       |           0.0131498  |          0.00770077 |

After we performed permutation tests, we found that the **observed statistic** for this permutation test is: 0.9647151320636651, and the **p-value** is 0. The plot below shows the empirical distribution of the TVD for the test.

<iframe
  src="assets/PerHist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Since the p-value is less than the 0.5 significance level, we reject the null hypothesis. Thus, the missingness of **firstblood** depends on the **league** column. 

The second permutation test that we are performing is on **firstblood** and **result**, and the missingness of **firstblood** does not depend on **result**. 

Null Hypothesis: Distribution of**result** when **firstblood** is missing is the same as the distribution of **result** when **firstblood** is not missing.
Alternative Hypothesis: Distribution of **result** when **firstblood** is missing is NOT same as the distribution of **result** when **firstblood** is not missing.

Below is the observed distribution of `result` when `firstblood` is missing and not missing.

|   result |   fb_missing = False |   fb_missing = True |
|---------:|---------------------:|--------------------:|
|        0 |             0.500092 |                 0.5 |
|        1 |             0.499908 |                 0.5 |

After we performed permutation tests, we found that the **observed statistic** for this permutation test is: 9.174311926607448e-05, and the **p-value** is 0.99
. The plot below shows the empirical distribution of the TVD for the test.

<iframe
  src="assets/FigNot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Since the p-value is greater than the 0.5 significance level, we fail to reject the null hypothesis. Thus, the missingness of **firstblood** does not depend on the **result** column. 

## Hypothesis Testing
In the hypothesis test, we aim to assess whether there is a significant difference in the distribution of kills for winning games between the team that secures the first blood and the team that does not. This investigation is crucial for understanding the relationship between securing the first blood in a League of Legends match and the subsequent gameplay dynamics, particularly in terms of kill distribution among winning teams.

**Null**: The distribution of kills for winning games for the team that gets the first blood is the same as the team that does not get the first blood. 

**Alternative**: The distribution of kills for winning games for the team that gets the first blood is NOT the same as the team that does not get the first blood.

**Test Statistics**: Absolute mean difference between teams in kills with and without first kills,

**Significance Level**: 5%

Here is a histogram containing the distribution of our test statistics during the hypothesis test:

<iframe
  src="assets/HypoHist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Based on the hypothesis test performed, with a **p-value** of **0.0009990**, we **reject** the null hypothesis. This suggests that the distribution of kills for winning games for the team that secures the first blood is NOT the same as the team that does not get the first blood. This finding indicates that securing the first blood may indeed have a significant impact on the gameplay dynamics and overall success of the team in League of Legends matches.

## Framing a Prediction Problem
The model that we built are based on the following **prediction problem**: Are we able to predict if a player’s position is jungle or not based on their other game statistics? 

In this part, we will need to one hot encode the original **position** column, and this will give us 5 binary columns representing each position: **position_top**, **position_jng**, **position_mid**, **position_bot**, **position_sup**.  Since we are predicting based on individual performance, we decide to drop all the team rows, and keep only the player rows. Thus, this is a **binary classfication model**, and our responsive variable is **position_jng**. Since we are only predicting if the given player is jungle or not, we can drop all other binary columns for position. The below is the head of DataFrame we are using in this section: 

|   index |   kills |   deaths |   assists |   firstbloodkill |   team kpm |   minionkills |   position_jng |
|--------:|--------:|---------:|----------:|-----------------:|-----------:|--------------:|---------------:|
|       0 |       2 |        3 |         2 |                0 |     0.3152 |           220 |              0 |
|       1 |       2 |        5 |         6 |                0 |     0.3152 |            33 |              1 |
|       2 |       2 |        2 |         3 |                0 |     0.3152 |           177 |              0 |
|       3 |       2 |        4 |         2 |                0 |     0.3152 |           208 |              0 |
|       4 |       1 |        5 |         6 |                1 |     0.3152 |            42 |              0 |

To prevent overfitting, the data will be split into two parts: 75% training data, and 25% test data. In terms of model’evaluation, we will use both accuracy and F1-score. The reason we are using F1-score on top of accuracy is because the data we are working on is unbalanced. In the DataFrame, 20% of the player’s positions are jungle, and 80% of players are some other positions; the accuracy score alone won’t give us a representative evaluation of the model. 

At the time of prediction, we only know the following information for each player: ‘kills',  'deaths', 'assists', 'firstbloodkill', 'monsterkills', and  'minionkills'. These are all the statistics collected during the game. We will train our model based on the above features.

## Baseline Model
For the baseline model, we used a Random Forest Classifier, with the following three features: kills, deaths, assists, and firstbloodkill. Among these four features, kills, deaths, and assists are quantitative, and we utilized StandardScaler Transformer to transform them into standard scale. The firstbloodkill is a nominal categorical variable, and it is already in binary form, thus we do not need to perform more encodings.

After fitting the model, our accuracy score on the training data is **0.79454**. This means that our model is able to correctly predict **79.454%** of data. This accuracy score may sound really high, but it is quite misleading since our data is unbalanced. The F-1 score of this model is **7.913%** which is extremely low. Such a low F-1 score is due to a small Recall of 0.044336, as our model has many false negatives. Our model still has large improvement space, and we will improve it through adding more features, and tuning hyperparameters in the next section. 

Here is our confuse matrix from the baseline model.
<iframe
  src="assets/Matrix.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Final Model
In our final model, we added two more features: **monsterkills** and **minionkills**. We are adding these two features into our model because we believe in the LOL game, the champions in jungle positions usually have higher damage, so they are able to kill more minions compared to other positions at the same amount of time. Moreover, the main job of the jungle position in the game is to kill the monsters, so we believe jungle positions should have a relatively high **monsterkills** number. Additionally, **minion kills** reflect a player's ability to efficiently farm gold and experience, which are crucial for scaling and gaining advantages in the game. Therefore, we expect that both monster kills and minion kills will provide valuable predictive power in our final model, allowing us to better understand the factors influencing victory in League of Legends matches.

Our final model also uses a random forest classifier in alignment with the baseline model. The two additional features we added (**monsterkills** and **minionkills**) are both quantitative features, so we used StandardScaler Transformer to perform encodings of these two columns. In terms of tuning hyperparameters, the two hyperparameters we chose are: max depth and the number of estimators for the random forest classifier. We are testing max depth of 2 through 200, with each of 20 steps. For the number of estimators, we are testing from 2 to 100, with each of 10 steps. Using the technique of grid search to find the best hyperparameters, we found out that the best max depth is 22 and the best number of estimators is also 22. 

The accuracy score is now 0.9993, meaning our model is able to correctly predict 99.93% of our data. This score is super high! If we now take a look into the F-1 score, it is 99.83%, meaning both of our precision and recall are close to 1. We have achieved huge improvement in both evaluation metrics, and this improvement suggests that our adjustment to the model is effective in terms of prediction power.

## Fairness Analysis
In this section, we are going to assess if our model is fair among different groups. The question we are trying to answer here is: “ does my model perform worse for individuals who have monsterkills less than or equal to 100 than it does for individuals who have monster kills greater than 100? 

The group X represents the players who have monsterkills less than or equal to 100, and group Y represents those who have monster kills greater than 100. Our evaluation metric is accuracy, and the significance level is 0.05. 

The followings are our hypothesis:
Null hypothesis: Our model’s accuracy for individuals who have less than or equal to 100 monsterkills is same as the accuracy for individuals who have greater than 100 monsterkills.
Alternative hypothesis: Our model’s accuracy for individuals who have less than or equal to 100 monsterkills is NOT same as the accuracy for individuals who have greater than 100 monsterkills.

After performing the permutation test, the result p-value we got is 0.798, which is larger than the 0.05 significance level, and we fail to reject the null hypothesis. Thus our model predicts players from two groups with the same accuracy, and our model is fair. 

