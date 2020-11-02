# MOVIE DATABASE
## SUMMARY
  Using data from three sources, this project combines the data sources, cleans them up and then adds it to a PostgreSQL datagbase to be available for future analysis
### BACKGROUND
Using a combination of Pandas, Python and the ETL process, we were able to create a function that cleaned Wikipedia and Kaggle data about movies.  Once these databases were cleaned, we added them to an SQL database which now has two tables with a primary common key so the inforamtion ca be combined.  Since this process was successful, this new project is now going to add in a third database from MovieLens which will make the analytical process more robust.
### DATA AVAILABLE
  JSON data from Wikipedia for movies
  Kaggle Data from Movies
  MovieLens data with Ratings of Movies
### ANALYSIS
1.  Create an ETL function function to read in three data files
![](https://github.com/xactuary/movies-ETL/blob/main/Resources/Function_1.PNG)
2. Cleaning the Wikipedia Data
  
This part is extensive in edits due to the varying nature of the Json data that comes from Wikipedia.  The first step is to review the data.  There are 193 variables and 7,311 records.  This is too many records and variables to individually inspect so I have written a function that will clean it up before I put it in the SQL database.  
 
 Cleaning Steps
 1.  The first step is to remove the TV shows.  There is a variable called "No. of episodes" which shows a digit greater than 1 for serialized programs that can be used to remove the TV shows from the data.  Using the following list comprehension code, I identify 6 cases of TV shows in the data and remove them.  The resulting record count is 7,305.
   >  wiki_movies = [movie for movie in wiki_movies_raw
      if 'No. of episodes' in movie]
