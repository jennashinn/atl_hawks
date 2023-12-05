# *The Pick is In* - Predicting NBA Draft Value

With only two rounds, making the correct pick for an NBA team is paramount to the future success of the franchise. 

## Data Processing & Understanding
The dataset used for this project was the [NBA Draft Basketball Player Data 1989-2021](https://www.kaggle.com/datasets/mattop/nba-draft-basketball-player-data-19892021/data). As with most data, this was very messy, with quite a view missing values and inconsistenly labeled team names. 

- **Missing Schools:** In 2005, the NBA began to require potential draftees to be removed at least one year from high school and be at least 19 years old. This prevented high school athletes going straight to the NBA. More recently, instead of going to college, many elite players have opted to play for one year in the G League. Because of these two exeptions, and players coming from another country, any player a null value in `college` would now have 'No College' listed.

- **Combining Teams:** Since some franchises have changed names and moved cities, I changed all of the team names to the current name of that franchise.
    - Ex. Seattle Sonics is now the Oklahoma City Thunder
 
**Handling Outliers**

- **Minutes Played:** To prevent a rookie with just a few minutes of playing time from creating too much variance, a minutes played limit was set. 

- **LeBron Ruins the Model:** Since LeBron James is quite literally in a tier of his own, he was removed from the dataset, as well as a few other extreme outliers (the complete duds) on both ends of the spectrum.To determine which players to remove, the z-score of 'value_over_replacement', 'box_plus_minus', and 'win_shares_per_48_minutes' was used. 

## Process and Results 
To create a method for valuing each draft slot in the NBA Draft, I used VORP. Since the graph appears to follow an exponential trend, I'm going use curve_fit from scipy.optimize to fit a line to the plot, and get a corresponding equation. This equation will only require overall_pick as a variable. The rest will be constants. The equation will allow us to enter the overall_pick and get the expected value_over_replacement.

## Future Work
To increase the accuracy of expected VORP, it would be ideal to have season-by-season data for the first four to six years of each player's career. It would also be helpful to have any draft trade data to know where a team is expected to draft.
