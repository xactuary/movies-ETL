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
2.  The xxt step is to clean up the imdb_id using regex code.  Imdb strings in the wiki look this this usually https://www.imdb.com/title/tt1234567/," with "tt1234567.  So the Regex code to standardize this is:
> wiki_movies_df['imdb_id'] = wiki_movies_df['imdb_link'].str.extract(r'(tt\d{7})')  
  
Although the project requested a try/except, the code did not find any exceptions.
3.  For step 3, columns that contained blanks for more than 90% of the occurrences were dropped.  
> wiki_columns_to_keep = [column for column in wiki_movies_df.columns if wiki_movies_df[column].isnull().sum() < len(wiki_movies_df) * 0.9]  
4.  Using similar Regex expressions, the next 2 cleaning steps changed what should be numeric data to numeric.  These variables include Box_office receipts and budget which are dollar amounts.  Most of the cases fit in these two categories:
> form_one = form_one = r'\$\s*\d+\.?\d*\s*[mb]illi?on' 
> form_two = r'\$\s*\d{1,3}(?:[,\.]\d{3})+(?!\s[mb]illion)'  

4.  the release date variable was cleaned up using Regex and parsing. There are 4 basic forms for this date: 
>  date_form_one = r'(?:January|February|March|April|May|June|July|August|September|October|November|December)\s[123]\d,\s\d{4}'  
>  date_form_two = r'\d{4}.[01]\d.[123]\d'  
>  date_form_three = r'(?:January|February|March|April|May|June|July|August|September|October|November|December)\s\d{4}'  
>  date_form_four = r'\d{4}'  





