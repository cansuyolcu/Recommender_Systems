## Recommender_Systems
In this project I focus on providing a basic recommendation system by suggesting movies.
# Importing Libraries

```python
import numpy as np
import pandas as pd
```
# Getting the Data

```python
column_names = ['user_id', 'item_id', 'rating', 'timestamp']
df = pd.read_csv('u.data', sep='\t', names=column_names)
df.head()
```

<img src= "https://user-images.githubusercontent.com/66487971/89820347-8cd9ab80-db55-11ea-9114-d19eb791a448.png" width = 250>

```python
movie_titles = pd.read_csv("Movie_Id_Titles")
movie_titles.head()
```

<img src= "https://user-images.githubusercontent.com/66487971/89820484-be527700-db55-11ea-9164-a10f5a8f0b88.png" width = 200>

```python
df = pd.merge(df,movie_titles,on='item_id')
df.head()
```

<img src= "https://user-images.githubusercontent.com/66487971/89820573-e9d56180-db55-11ea-9189-12b2e65abfc7.png" width = 350>

## EDA

```python
import matplotlib.pyplot as plt
import seaborn as sns
sns.set_style('white')
%matplotlib inline
```

```python
df.groupby('title')['rating'].mean().sort_values(ascending=False).head()
```

<img src= "https://user-images.githubusercontent.com/66487971/89820974-81d34b00-db56-11ea-8615-80438ce2f109.png" width = 350>


```python

df.groupby('title')['rating'].count().sort_values(ascending=False).head()
```

<img src= "https://user-images.githubusercontent.com/66487971/89821073-b0e9bc80-db56-11ea-86e5-f201ebbc1c6f.png" width = 250>

```python

ratings = pd.DataFrame(df.groupby('title')['rating'].mean())
ratings.head()

```

<img src= "https://user-images.githubusercontent.com/66487971/89821146-d676c600-db56-11ea-9e1c-bf322fddbdbf.png" width = 250>

```python
ratings['num of ratings'] = pd.DataFrame(df.groupby('title')['rating'].count())
ratings.head()
```

<img src= "https://user-images.githubusercontent.com/66487971/89821241-f8704880-db56-11ea-8646-acd986be74b8.png" width = 350>

```python

plt.figure(figsize=(10,4))
ratings['num of ratings'].hist(bins=70)

```

<img src= "https://user-images.githubusercontent.com/66487971/89821339-19d13480-db57-11ea-95dd-ecf58b678c21.png" width = 700>

```python

plt.figure(figsize=(10,4))
ratings['rating'].hist(bins=70)

```

<img src= "https://user-images.githubusercontent.com/66487971/89821523-6157c080-db57-11ea-8fb3-941f2f0f2d8b.png" width = 700>

```python
sns.jointplot(x='rating',y='num of ratings',data=ratings,alpha=0.5)
```

<img src= "https://user-images.githubusercontent.com/66487971/89821699-b0055a80-db57-11ea-9fd3-296246b077cd.png" width = 550>

# Recommending Similar Movies

```python

moviemat = df.pivot_table(index='user_id',columns='title',values='rating')
moviemat.head()

```

<img src= "https://user-images.githubusercontent.com/66487971/89870407-7582d880-dbbe-11ea-80d2-c2857cee44d0.png" width = 1000>


```python
ratings.sort_values('num of ratings',ascending=False).head(10)
```

<img src= "https://user-images.githubusercontent.com/66487971/89870611-c8f52680-dbbe-11ea-9662-856ec432d239.png" width = 300>

I choose Star Wars, a sci-fi movie. And Liar Liar, a comedy.

```python

starwars_user_ratings = moviemat['Star Wars (1977)']
liarliar_user_ratings = moviemat['Liar Liar (1997)']

```

# Cleaning Nan values and getting correlations


```python
corr_starwars = pd.DataFrame(similar_to_starwars,columns=['Correlation'])
corr_starwars.dropna(inplace=True)
corr_starwars.head()
```

<img src= "https://user-images.githubusercontent.com/66487971/89871119-8bdd6400-dbbf-11ea-9d54-0b0951f07029.png" width = 200>


Now if I sort the dataframe by correlation, I get the most similar movies, however I get some results that don't really make sense. This is because there are a lot of movies only watched once by users who also watched Star Wars.

```python

corr_starwars.sort_values('Correlation',ascending=False).head(10)
```


<img src= "https://user-images.githubusercontent.com/66487971/89871274-d52db380-dbbf-11ea-90fc-dc78c54c626c.png" width = 500>





























