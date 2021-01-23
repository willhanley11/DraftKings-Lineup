# Creating the Optimal Daily Fantasy Lineup: 

### Using past NBA game-logs to forcast upcoming statistics 

The goal of this data science project is to create a model to forecast NBA player statistics. Using game-logs dating back to 2016, I will try to predict the statistics of each player for an upcoming game and use the predictions to create an optimal lineup to be played in DraftKings daily fantasy.

DraftKings daily fantasy is a daily contest hosted on DraftKings.com. Participants are given a list of NBA players that will be playing that night, and a salary attached to each of those players. The goal of the contest is to choose 8 players that the participant thinks will have the highest "DraftKings score" while remaining under the $50,000 salary cap. For example, LeBron James may cost $12,000 on a given night, while Joe Schmo may only cost $3,000. Further, the lineup must include one player from each basketball position (Point Guard, Shooting Guard, Small Forward, Power Forward, Center), as well as 3 wildcards (a guard of anykind, a forward of anykind, and any position). Choose the lineup with a high cumulative DraftKings score, and win money! 

According to DraftKings.com, the percentage of participants who are profitable in the last 30 days is just 19%. So it looks like we will have our work cut out for us.

### DraftKings Scoring System

<a href="url"><img src="./images/Screen%20Shot%202021-01-22%20at%204.17.01%20PM.png" height="300" width="700" ></a>

### Data Collection and Processing

The data for this project came in 3 parts. First, the game log data was collected from stats.nba.com. I used Selenium to webscrape the games dating back to 2016, collecting over 100,000 game logs. Second, I needed an up to date list of the current players that would be playing that night. To get that information, I webscraped from www.sportsline.com. Finally, I scraped from www.fantasypros.com to collect the positions of the players, as well as their DraftKings salaries. All of this data can be scraped on a daily basis to get up to date information for the current days games. 

The preprocessing of the data involved feature enginerring. Obviously, the game logs did not have a DraftKings score in them. Using the formula for the DraftKings score (and creating a few other columns, double-double, etc.), I attached a total score to each game in the game logs. 

### Model and Projection Data

Using a VAR model with certain restrictions and a whole lot of "pd.merge", I was able create DraftKings score projections for each player playing in a game that day. The dataframe consists of the Player, Position, Points Projection, Actual Salary, Points Projection Rank, Actual Salary Rank, and an Eligable column as a way of finding outliers. A sample of 10 players can be seen below. 

<a href="url"><img src="./images/Screen%20Shot%202021-01-22%20at%204.01.46%20PM.png" height="350" width="600" ></a>

### Optimizing the lineup

Given the salary and position restrictions, our goal is to find the most projected points from the player pool. Using an optimizer that I modifed from fantasy football (optimizer written by Branko Blagojevic), we are able to find the players with the highest values and from that, find our optimal lineup.





