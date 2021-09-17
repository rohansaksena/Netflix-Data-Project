# Netflix Dataset 

This is a basic data analysis projects containing some data analysis and visualisation . Here , a dataset of Netflix Movies and TV Shows is present which contain fields of "Show_Id", "Category", "Title", "Director", "Cast", "Country", "Release_Date", "Rating", "Duration",        "Type", "Description"  . This Dataset is present in a csv file which we will read using the pandas dataframe.

## Data Source : - Kaggle


## Project Outcomes:
#### By the time we finish this project we would have successfully answered a few questions:

### Previewing the first 5 entries of our dataset
```
netflix_df.head()
```
### Previewing the last 5 entries of our dataset
```
netflix_df.tail()
```
### Finding the rows and columns in our Dataset
```
netflix_df.shape
```
### Finding out any null values if they exist and represent them through a heatmap
```
netflix_df.isnull().sum()
sns.heatmap(netflix_df.isnull())
```
### Finding out the data type for each variable
```
netflix_df.dtypes
```
### Replacing all 'Directors' with Null Values to 'unknown'
```
netflix_df["Director"] = netflix_df["Director"].fillna('Unknown')
netflix_df["Cast"] = netflix_df["Director"].fillna('Unknown')
netflix_df.head()
```
### Finding out the data from our dataset which have the 'Type' equal to "International TV Shows, TV Dramas" or "International TV Shows", "TV Dramas"
```
netflix_df[netflix_df['Type'].isin(["International TV Shows, TV Dramas","International TV Shows", "TV Dramas"])]
```
### Finding Duplicate data from our dataset
```
netflix_df[netflix_df.duplicated()]
```
### Removing Duplicate Data from our Dataset
```
netflix_df.drop_duplicates(inplace=True)
netflix_df.shape #To check our changes
```
### What is the show Id for House of cards and who directed it ?
```
netflix_df[netflix_df['Title'] =='House of Cards'] #Method 1
netflix_df[netflix_df['Title'].isin(['House of Cards'])] #Method 2
netflix_df[netflix_df['Title'].str.contains('House of Cards')] #Method 3
```
### convert object data type to datetime
```
netflix_df['Release_Date'] = pd.to_datetime(netflix_df['Release_Date'])
netflix_df.dtypes
```
### In which year were the maximum number of shows and series were released ? show with Bargraph
```
netflix_df['Release_Date'].dt.year.value_counts()
netflix_df['Release_Date'].dt.year.value_counts().plot(kind='bar')#Method 1

netflix_df['Release_Years'] = netflix_df['Release_Date'].dt.year
plt.xticks(rotation=45)
sns.countplot(x='Release_Years',data=netflix_df)#Method 2
```
### Number of Movies and TV Shows Present in this Dataset , represent it via Bargraph
```
netflix_df['Category'].value_counts()#Unique Movie and Tv Shows
sns.countplot(x='Category',data=netflix_df,palette='Set2',lw=3,ec='black',hatch='/')#Method 1
netflix_df['Category'].value_counts().plot(kind='bar')#Method 2
```
### Show all the movies that were released in the year 2016
```
netflix_df[(netflix_df['Category']=='Movie')&(netflix_df['Release_Years']== 2016)]
```
### Show only the Titles of all TV Shows that were released in India only
```
netflix_df[(netflix_df['Category']=='TV Show')&(netflix_df['Country']=='India')]['Title']
```
### Show top 10 Directors who gave most number of movies and TV Shows to netflix
```
netflix_df['Director'].value_counts().head(10)
```
### Show all records where category is movies and Type is comedies or country is United Kingdom
```
netflix_df[(netflix_df['Category']=='Movies') & (netflix_df['Type']== 'Comedies') | (netflix_df['Country']=='United Kingdom')]
```
### Name the movies that "Tom Cruise" was a part of
```
netflix_new = netflix_df.dropna()
netflix_new[netflix_new['Cast'].str.contains('Tom Cruise')]
```
### Different Ratings given in Netflix
```
netflix_df["Rating"].nunique()
netflix_df["Rating"].unique()
```
### Number of Tv Shows with 'R' rating after 2018
```
netflix_df[(netflix_df["Rating"] =='R') & (netflix_df['Release_Years']>2018)].shape
```
### Number of Tv Shows with 'TV-14' rating in 'Canada'
```
netflix_df[(netflix_df["Rating"] =='TV-14') & (netflix_df['Country']=='Canada')].shape
```
### Maximum Duration of a TV Show or Movie
```
netflix_df[["Duration_no","temp"]]=netflix_df['Duration'].str.split(' ',expand=True)
netflix_df.drop(columns='temp')
netflix_df[netflix_df['Category']=='Movie']['Duration_no'].max() #Maximum Duration for a movie
netflix_df[netflix_df['Category']=='TV Show']['Duration_no'].max()
```
### Sorting Database on the basis of Years
```
netflix_df.sort_values(by='Release_Years')
```
### Find all the instances where Category is 'Movie' and Type is 'Drama' or Category is 'TV Shows' and Type is 'Kids TV'
```
netflix_df[(netflix_df['Category']=="Movie") & (netflix_df['Type']=="Dramas") | (netflix_df['Category']=="TV Show") & (netflix_df['Type'].isin(["Kids' TV"]))]

```

## Project Setup:
To clone this repository you need to have Python compiler installed on your system alongside pandas and seaborn libraries. I would rather suggest that you download jupyter notebook if you've not already.

To access all of the files I recommend you fork this repo and then clone it locally. Instructions on how to do this can be found here: https://help.github.com/en/github/getting-started-with-github/fork-a-repo

The other option is to click the green "clone or download" button and then click "Download ZIP". You then should extract all of the files to the location you want to edit your code.

Installing Jupyter Notebook: https://jupyter.readthedocs.io/en/latest/install.html<br>
Installing Pandas library: https://pandas.pydata.org/pandas-docs/stable/install.html
