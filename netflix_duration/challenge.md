**Netflix**! What started in 1997 as a DVD rental service has since exploded into one of the largest entertainment and media companies.

Given the large number of movies and series available on the platform, it is a perfect opportunity to flex your exploratory data analysis skills and dive into the entertainment industry. Our friend has also been brushing up on their Python skills and has taken a first crack at a CSV file containing Netflix data. They believe that the average duration of movies has been declining. Using your friends initial research, you'll delve into the Netflix data to see if you can determine whether movie lengths are actually getting shorter and explain some of the contributing factors, if any.

You have been supplied with the dataset `netflix_data.csv` , along with the following table detailing the column names and descriptions:

## The data
### **netflix_data.csv**
| Column | Description |
|--------|-------------|
| `show_id` | The ID of the show |
| `type` | Type of show |
| `title` | Title of the show |
| `director` | Director of the show |
| `cast` | Cast of the show |
| `country` | Country of origin |
| `date_added` | Date added to Netflix |
| `release_year` | Year of Netflix release |
| `duration` | Duration of the show in minutes |
| `description` | Description of the show |
| `genre` | Show genre |


# Importing pandas and matplotlib
import pandas as pd
import matplotlib.pyplot as plt

# Start coding!

filename = 'netflix_data.csv'
netflix_df = pd.read_csv(filename)
netflix_df.head(5)

netflix_subset = netflix_df[netflix_df['type'] == 'Movie']
netflix_subset.head(5)

netflix_movies = netflix_subset[['title', 'country','genre', 'release_year', 'duration' ]]
netflix_movies.head(5)

short_movies = netflix_movies[netflix_movies['duration'] < 60]
short_movies.head(20)

colors = []

for index, row in netflix_movies.iterrows():
    genre = row['genre']
    
    if 'Children' in genre:
        colors.append('blue')
    elif 'Documentaries' in genre:
        colors.append('green')
    elif 'Stand-Up' in genre:
        colors.append('yellow')
    else:
        colors.append('red')
        
print(colors[:5])

import matplotlib.pyplot as plt

colors = colors[:len(netflix_movies)]

fig, ax = plt.subplots(figsize=(12, 8))

scatter_plot = ax.scatter(
    x=netflix_movies['release_year'],
    y=netflix_movies['duration'],
    c=colors,  
    alpha=0.5 
)


ax.set_xlabel('Release Year')
ax.set_ylabel('Duration (min)')
ax.set_title('Movie Duration by Year of Release')
handles = [plt.Line2D([0], [0], marker='o', color='w', markerfacecolor=color, markersize=10) for color in set(colors)]
labels = ['Children', 'Documentaries', 'Stand-Up', 'Other']
ax.legend(handles, labels, title='Genres', loc='upper left')
plt.show()


"Are we certain that movies are getting shorter?"

Maybe!
There's an increase of short movies after 2000, but we still have the same quantite of long movies same as last century.
The average, median and standard deviation are lower now, fore sure, we still have a good quantity of long movies.

