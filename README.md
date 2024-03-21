# League of Legends -analysis
A data science project at UCSD that performs Exploratory Data Analysis, Hypothesis test, creating Baseline Models and fiannly performing fairness analysis on real-life gaming data from League of Legends.

Authors: Jingxiao Qiu, Sirui Zhang

## Introduction
### General Introduction
League of Legends (LOL) is a popular multiplayer online battle arena (MOBA) game developed by Riot Games. With millions of players worldwide, it has become one of the most influential and widely played esports in the gaming industry. The data set we will be working with is a professional data set that’s developed by Oracle's Elixir. The file records match data from professional LOL esports gaming matches throughout 2022. 

This dataset captures key gameplay statistics and outcomes from a collection of LOL matches, offering a rich source of information for understanding player behavior, team dynamics, and match outcomes. It includes a variety of features such as individual player performance, team strategies, in-game statistics, and overall match dynamics.

In the realm of League of Legends (LOL), the concept of **"first blood"** holds significant weight and serves as an important trajectory of a match. First blood refers to the initial first kill secured by a team during the early stages of a game. Beyond its immediate impact on the scoreboard, first blood sets the tone for the ensuing gameplay, often shaping the general dynamics, strategies, and outcomes of the match.

The central question we are interested in is **Does the occurrence of the first blood influence the probability of winning a League of Legends match?** We want to use data analysis techniques to testify the impact of first blood on gaming statistics,  including individual player performance, team strategies, in-game metrics, and ultimately, match outcomes. 

### Introduction of Columns
The dataset introduces a comprehensive array of columns featuring gameplay metrics and match outcomes from professional League of Legends esports matches. Here's an introduction to some of the key columns:
In the dataset provided, we encounter various columns that encapsulate essential gameplay statistics and match outcomes from professional League of Legends (LoL) esports matches. Here's a brief introduction to each of these columns:

- **gameid**: This column represents a unique identifier for each individual match played. It allows us to distinguish between different matches in the dataset.

- **side**: The 'side' column denotes the team affiliation of a particular player or team. It typically distinguishes between 'blue' and 'red' teams, providing insights into the team dynamics and matchups within a match.

- **result**: This column indicates the outcome of a match for a specific team or player. It may denote whether the team won, lost, or if the match ended in a draw.

- **kills**: The 'kills' column quantifies the number of enemy champions a player or team successfully eliminated during the match. 

- **deaths**: Conversely, the 'deaths' column records the number of times a player or team was eliminated by enemy champions. 

- **assists**: The 'assists' column records the number of assists credited to a player or team, indicating instances where they contributed to eliminating an enemy champion without securing the kill themselves.

- **firstblood**: This binary column indicates whether the occurrence of the first blood event took place in the match. First blood refers to the first instance of a player or team securing a kill in the game.

- **firstbloodkill**: Similar to 'firstblood', this binary column specifically denotes whether a player or team secured the first kill of the match, thereby earning the distinction of 'first blood.'

- **team kpm**: 'Team kpm' stands for 'kills per minute' and represents the average rate at which a team secures kills over the duration of the match. 

- **position**: The 'position' column specifies the role or position played by an individual player within their team composition. Common positions include 'top,' 'jungle,' 'mid,' 'bot,' and 'support.'

- **minionkills**: This column records the number of minions or neutral monsters slain by a player or team during the match. It reflects their ability to efficiently farm gold and experience points, crucial for character progression and itemization.

- **league**: The 'league' column denotes the specific league tournament in which the match took place.

## Data Cleaning and Exploratory Data Analysis
## Assessment of Missingness
## Hypothesis Testing
## Framing a Prediction Problem
## Baseline Model
## Final Model
## Fairness Analysis
