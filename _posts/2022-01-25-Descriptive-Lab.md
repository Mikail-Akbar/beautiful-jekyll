# Welcome to my descriptive lab!

The dataset I worked with entails the statistics regarding the football teams in Europe’s top 5 leagues (Serie A, Bundesliga, Ligue 1, La Liga, Premier League).  The top 5 leagues in Europe are determined by the [UEFA league coefficients](https://www.uefa.com/nationalassociations/uefarankings/country/). In this data, each club corresponds to information about its league, goals scored, shots attempted per game, yellow cards, red cards, possession %, passing accuracy (in %), the # of aerial duels won, and the team rating. I’m interested in most of these categories (besides red cards and team rating), and all I wanted to do is to try to find some correlations between the data. I also wanted to find some centers in the data to see how teams in Europe generally perform. As a result, I can better understand the tactics of the game and whether certain aspects lead to more goals, etc. 

The [dataset](https://www.kaggle.com/varpit94/football-teams-rankings-stats) was created by Arpit Verma on Kaggle.

### Center and variability in my data (98 teams)
|       | Goals | Shots per game | Pass accuracy (%) | Aerial duals won |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| Mean | 52.18 | 11.85 | 80.44 | 16.00| 
| Standard Deviation | 16.45 | 2.150 | 4.690 | 3.079 | 
| Min | 20.00 | 7.100 | 66.50 | 9.500 |
| 25% | 40.25 | 10.33 | 78.03 | 14.03 |
| 50% | 50.00 | 11.45 | 80.80 | 16.10 |
| 75% | 61.75 | 13.35 | 83.45 | 17.85 |
| Max | 99.00 | 17.10 | 89.70 | 26.80 |

### Some notes about the center and variability of the selected 4 categories
- The data for the goals scored is somewhat dispersed, compared to the data for the other 3 columns. The range is a whopping 79 goals, and the standard deviation is 16.45 goals. I visualized this data in a box plot below.
- The data in all 4 columns are not skewed in any direction, as the means and medians are very close to each other. 

![boxplot](https://github.com/Mikail-Akbar/mikail/blob/Mikail-Akbar-patch-1/assets/img/boxplot.png?raw=true)

## What I found:

#### 1. In terms of goals scored, some leagues are more lop-sided than others.

The IQR gives a good idea about where the middle 50% of the data lies. In terms of the goals scored across all 5 leagues, some leagues have teams that score very few goals and other teams that score many goals; this creates a lop-sided league. I calculated how many teams in each league scored an amount of goals that was lower than the 25% mark:

- Bundesliga: 6 (Mainz, Augsburg, Arminia Bielefeld, Werder Bremen, FC Koln, Schalke 04)
- La Liga: 0
- Serie A: 2 (Parma, Benevento)
- Ligue 1: 3 (Angers, Nimes, Dijon)
- Premier League: 6 (Wolves, Brighton, Burnley, Fulham, West Brom, Sheffield United)

I also calculated how many teams scored an amount of goals that are higher than the 75% mark:

- Bundesliga: 4 (Bayern Munich, Borrusia Dortmund, Eintracht Frankfurt, Borrusia Monchengladbach)
- La Liga: 0
- Serie A: 7 (Juventus, Roma, AC Milan, Inter Milan, Atalanta, Napoli, Sassuolo)
- Ligue 1: 4 (PSG, Monaco, Lyon, Lille) 
- Premier League: 7 (Man City, Man United, Tottenham, Leeds, West Ham, Leicester, Liverpool)

This means that, in terms of goals scored, some leagues are more balanced than others. The most balanced league in that regard is clearly La Liga, as all 20 teams fall in the IQR. On the other hand, the Premier League is the most lop-sided league, with 13 out of 20 teams falling outside the IQR of the goals scored within Europe's top 5 leagues.

#### 2. There is a direct relationship between possession and goals scored. 

![possgoals]({{baseurl}}/assets/img/possgoals.png)

##### Value of correlation: 0.718

We can conclude that teams that have more possession score more goals, which is supported by our value of correlation of 0.718, a number that is close to 1. Based on this graph, I wonder why coaches deploy the counter-attack tactic, where the defense sits deep on the pitch and allows the other side to have possession so that when they win back possession, they can speed down the pitch to get an open, goal-scoring opportunity. 

#### 3. Serie A teams score the most goals, while La Liga teams score the least amount of goals. 

![goalbargraph]({{site.baseurl}}/assets/img/goalsbar.png)

We can conclude that Serie A teams have the most attacking tactics (leading to the most goals), while La Liga teams have the most defensive tactics. In the future, I can  analyze the attacking vs. defensive tactics of a team by looking at the average field position of the 10 outfield players, as well as the formation each manager employs (3-4-3, 4-3-3, 4-4-2, etc.)

#### 4. La Liga teams win the most aerial duels, while Serie A teams win the least aerial duels.

![aerialswonbar](https://github.com/Mikail-Akbar/mikail/blob/Mikail-Akbar-patch-1/assets/img/aerialsbar.png?raw=true)

Since La Liga teams score the least goals, this can mean that they use more defensive tactics and hence win more aerial duels (a defensive statistic.) On the other hand, while Serie A scores the most goals, that can mean that they deploy more attacking attacks and thus win the least aerial duels.

#### 5. The information above is further corroborated by a scatter plot between goals and aerials won:

![aerialgoalsscatter](https://github.com/Mikail-Akbar/mikail/blob/Mikail-Akbar-patch-1/assets/img/aerialsgoals.png?raw=true)

##### Value of correlation: -0.496

Although the value of correlation is not entirely convincing, we can somewhat conclude that the more goals a team scores, the less aerial duels they win. This is a reasonable conclusion considering that teams either favor attacking or defensive tactics (a famous example is Chelsea FC’s “Park the Bus” tactic), so teams sacrifice defensive prowess to focus on scoring more goals. 

#### 6. There is an inverse relationship between aerial duels won and possession.

![aerialsposs](https://github.com/Mikail-Akbar/mikail/blob/Mikail-Akbar-patch-1/assets/img/aerialsposs.png?raw=true)

##### Value of correlation: -0.544

This is a surprising relationship, since winning more aerial duels means to win possession. So, it’s interesting to find that teams that win less aerial duels have a bigger hold on possession. Although the value of correlation here is also not entirely convincing, there is still some relationship between the two variables.

#### 7. There is a direct relationship between a team’s shots per game and passing accuracy.

![shotspass](https://github.com/Mikail-Akbar/mikail/blob/Mikail-Akbar-patch-1/assets/img/shotspass.png?raw=true)

##### Value of correlation: 0.684

We can conclude that the more shots a team takes per game, the higher their passing accuracy. This is supported by a value of correlation of 0.684. It’s possible that this relationship exists due to the technical quality of the team; if a team can find a way to create more shots per game, their passing accuracy would also reflect the technical excellence on the pitch. 

#### 8. There is no correlation between yellow cards and goals scored. 

![yellowcards](https://github.com/Mikail-Akbar/mikail/blob/Mikail-Akbar-patch-1/assets/img/yellowcards.png?raw=true)

##### Value of correlation: -0.189

I wanted to look at this statistic because I wanted to see whether teams that have more yellow cards (which means that they are more agressive on the pitch) correlates to more goals scored. However, according to the scatter plot, there is not correlation between the two variables. This conclusion is further corroborated by a value of correlation of -0.189, which is close to 0, or no correlation at all. 

## Limitations
I wish this dataset included information about the teams’ record. This way I can analyze whether these various statistics (shots per game, possession, aerial duels, etc) has an effect on the success of the team. While it is interesting to correlate these statistics to the goals scored per game, scoring goals does not mean that a team is successful. Furthermore, all of the data that is presented in the dataset is from teams that play in one league. In other words, data from interleague play is not represented in this dataset. That can affect our data because teams may score a certain number of goals against teams in their own league, but that number can increase or decrease against teams from other leagues. 
