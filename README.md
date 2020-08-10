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

<img src= "https://user-images.githubusercontent.com/66487971/89820484-be527700-db55-11ea-9164-a10f5a8f0b88.png" width = 250>

```python
df = pd.merge(df,movie_titles,on='item_id')
df.head()
```

<img src= "https://user-images.githubusercontent.com/66487971/89820573-e9d56180-db55-11ea-9189-12b2e65abfc7.png" width = 250>

## EDA


