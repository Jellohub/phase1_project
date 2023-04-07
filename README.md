# FLATIRON SCHOOL PHASE 1 PROJECT
*Angelo Turri*

##### Goals
Microsoft stakeholders are looking to get into the movie business. They are likely trying to make basic high level decisions such as where to allocate resources for advertising. This project is designed to inform such basic decisions.

##### Areas of Focus and Measures of Success
I focused on making recommendations for selecting genre, areas of advertising, and cast & crew members. My measures of success were ROI (return on investment), which is calculated by dividing the total gross of movie by its budget, and whether or not the movie was profitable. These measures of success are closely linked by not exactly the same.

# Advertising

##### Data prep & cleaning
For my analysis on advertising, I used a dataset from TheNumbers, which is a website that tracks box office revenue. This dataset contains 5,782 sample entries of their data. It contained data on the production budget, domestic, and worldwide gross for movies. I re-formatted each of the monetary columns, which were initially formatted as strings, to integer types, so I could perform statistical analyses on the data. I then used the monetary data to create columns for a movie's ROI, profitable status, and foreign gross. The columns were calculated as follows.

- ROI (denoted in percent): (worldwide gross / budget) * 100
- Profitable: **True** if ROI > 100%, **False** if ROI <= 100%.
- Foreign gross: Worldwide gross - domestic gross

I also created another ROI column, but instead of being a continuous variable, this column was a categorical column, with values such as "142%–214%".

In addition to creating new columns for more in-depth analysis, I eliminated outliers from the data. There were many extreme ones; the presence of such outliers is bound to skew results. Not wanting to make an unwarranted recommendation for stakeholders, I eliminated outliers from the ROI, budget, and worldwide gross columns using the same method that box-plots use to locate outliers:

- It was greater than the 75th percentile of its column by more than the IQR.
- It was less than the 25th percentile of its column by more than the IQR.

Each of these values was turned into a null value and then dropped from the dataset.

##### Analyses
I conducted three analyses and made three corresponding visualizations in this section. First, I analyzed the percentage of total earnings for domestic and total movie gross for movies of all different ROI levels. Second, I analyzed the same percentages for unprofitable movies. Finally, I analyzed the same percentages for profitable movies. These analyses showed a consistent dominance of domestic over foreign advertising, but a decreasing dominance as movie success or budget went up. Finally, it showed that unprofitable movies neglected foreign advertising even as their budget increased, whereas profitable movies did not neglect foreign advertising as much.

# Genre

##### Data prep and cleaning

For my analysis on genre, I used the dataset formed in the Advertising section, as well as a dataset from IMDB, which is a website that collects data on films, tv shows, video games, and more types of content. This dataset was one of eight tables in a larger SQLite database. It contained data on the genres of movies. To create a single dataframe out of the two datasets I had, I used a SQL query.

Once I had my dataframe, I eliminated any duplicates there were, which were entries that had the same name and genre but conflicting monetary data.

##### Analyses

I conducted three analyses and made three corresponding visualizations in this section. First, I analyzed the correlations between all different genres and profitability status (a Boolean variable indicating whether a movie is profitable or not), which yielded no clear results. Second, I analyzed the ROI for each genre. Third, I analyzed the average profitability status for each genre. The last two analyses yielded a list of very reliable genres, very unreliable genres, and a longer list of genres with no apparent defects or superiorities.

# Cast

##### Data prep and cleaning

For my analysis on cast, I used the dataset formed in the Genre section, as well as two more datasets from IMDB which contained the names and professions of people, as well as the movies they played in. I used a SQL query to join all three tables into one.

##### Analyses
I perform a single analysis in this section. This analysis is far more complex than any any other in this project. The question is: which cast members are more influential in a movie's success? To answer, we must determine the correlation between actor success and movie success. This means following these steps for each profession:

- Selecting groups of people of different levels of success in a certain time
- Selecting movies that involve those people in a later time
- Determining the correlation between actor success and the subsequent success of movies that hired them
- Repeating the process for different measures of success and different times
- Aggregating the data to get single success scores for each profession

This analysis yielded a clear superiority of off-screen crew to on-screen crew.