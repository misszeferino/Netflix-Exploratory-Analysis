# Netflix Exploratory Data Analysis



## Introduction

This is Exploratory Data Analysis using Python of the "Netflix Movies & TV Shows" dataset. The purpose of this project is to find out and visualize the data's main characteristics and trends using statistical methods and data visualization techniques.



# Phase 1: Ask


## About the data

The Netflix Movies & TV Shows dataset can be found on [Kaggle](https://www.kaggle.com/shivamb/netflix-shows). It contains all TV Shows and Movies metadata available on Netflix. The dataset is updated every month. It contains 8807 records and 12 columns.

[Netflix](http://en.wikipedia.org/wiki/Netflix) was founded on August 29, 1997, as a mail-based rental business. In January 2007, the company launched a streaming media service, introducing video on demand via the Internet.


## Objective

The purpose of this analysis is to answer the following questions:

* Number of movies/tv-shows added to the streaming platform by year
* Which month has the most added movies/tv-shows?
* Which day has the most added movies/tv-shows?
* How many Movies vs. TV-Shows?
* Which year has the most releases Movies/TV-Shows?
* Which is the oldest movie/tv-show on streaming?
* Which countries produce the most movies/tv-shows?
* Cast members with the most content


# Phase 2: Data Preparation


### Importing Libraries


```python
import pandas as pd 
import plotly.express as px
```


```python
import plotly.io as pio
pio.renderers.default = "svg"
```

### Loading the dataset with Pandas¶


```python
netflix = pd.read_csv('C:/Users/Luciana/Desktop/Portfolio/CaseStudy5_Netflix/netflix_titles.csv')
netflix
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>show_id</th>
      <th>type</th>
      <th>title</th>
      <th>director</th>
      <th>cast</th>
      <th>country</th>
      <th>date_added</th>
      <th>release_year</th>
      <th>rating</th>
      <th>duration</th>
      <th>listed_in</th>
      <th>description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>s1</td>
      <td>Movie</td>
      <td>Dick Johnson Is Dead</td>
      <td>Kirsten Johnson</td>
      <td>NaN</td>
      <td>United States</td>
      <td>September 25, 2021</td>
      <td>2020</td>
      <td>PG-13</td>
      <td>90 min</td>
      <td>Documentaries</td>
      <td>As her father nears the end of his life, filmm...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>s2</td>
      <td>TV Show</td>
      <td>Blood &amp; Water</td>
      <td>NaN</td>
      <td>Ama Qamata, Khosi Ngema, Gail Mabalane, Thaban...</td>
      <td>South Africa</td>
      <td>September 24, 2021</td>
      <td>2021</td>
      <td>TV-MA</td>
      <td>2 Seasons</td>
      <td>International TV Shows, TV Dramas, TV Mysteries</td>
      <td>After crossing paths at a party, a Cape Town t...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>s3</td>
      <td>TV Show</td>
      <td>Ganglands</td>
      <td>Julien Leclercq</td>
      <td>Sami Bouajila, Tracy Gotoas, Samuel Jouy, Nabi...</td>
      <td>NaN</td>
      <td>September 24, 2021</td>
      <td>2021</td>
      <td>TV-MA</td>
      <td>1 Season</td>
      <td>Crime TV Shows, International TV Shows, TV Act...</td>
      <td>To protect his family from a powerful drug lor...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>s4</td>
      <td>TV Show</td>
      <td>Jailbirds New Orleans</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>September 24, 2021</td>
      <td>2021</td>
      <td>TV-MA</td>
      <td>1 Season</td>
      <td>Docuseries, Reality TV</td>
      <td>Feuds, flirtations and toilet talk go down amo...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>s5</td>
      <td>TV Show</td>
      <td>Kota Factory</td>
      <td>NaN</td>
      <td>Mayur More, Jitendra Kumar, Ranjan Raj, Alam K...</td>
      <td>India</td>
      <td>September 24, 2021</td>
      <td>2021</td>
      <td>TV-MA</td>
      <td>2 Seasons</td>
      <td>International TV Shows, Romantic TV Shows, TV ...</td>
      <td>In a city of coaching centers known to train I...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>8802</th>
      <td>s8803</td>
      <td>Movie</td>
      <td>Zodiac</td>
      <td>David Fincher</td>
      <td>Mark Ruffalo, Jake Gyllenhaal, Robert Downey J...</td>
      <td>United States</td>
      <td>November 20, 2019</td>
      <td>2007</td>
      <td>R</td>
      <td>158 min</td>
      <td>Cult Movies, Dramas, Thrillers</td>
      <td>A political cartoonist, a crime reporter and a...</td>
    </tr>
    <tr>
      <th>8803</th>
      <td>s8804</td>
      <td>TV Show</td>
      <td>Zombie Dumb</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>July 1, 2019</td>
      <td>2018</td>
      <td>TV-Y7</td>
      <td>2 Seasons</td>
      <td>Kids' TV, Korean TV Shows, TV Comedies</td>
      <td>While living alone in a spooky town, a young g...</td>
    </tr>
    <tr>
      <th>8804</th>
      <td>s8805</td>
      <td>Movie</td>
      <td>Zombieland</td>
      <td>Ruben Fleischer</td>
      <td>Jesse Eisenberg, Woody Harrelson, Emma Stone, ...</td>
      <td>United States</td>
      <td>November 1, 2019</td>
      <td>2009</td>
      <td>R</td>
      <td>88 min</td>
      <td>Comedies, Horror Movies</td>
      <td>Looking to survive in a world taken over by zo...</td>
    </tr>
    <tr>
      <th>8805</th>
      <td>s8806</td>
      <td>Movie</td>
      <td>Zoom</td>
      <td>Peter Hewitt</td>
      <td>Tim Allen, Courteney Cox, Chevy Chase, Kate Ma...</td>
      <td>United States</td>
      <td>January 11, 2020</td>
      <td>2006</td>
      <td>PG</td>
      <td>88 min</td>
      <td>Children &amp; Family Movies, Comedies</td>
      <td>Dragged from civilian life, a former superhero...</td>
    </tr>
    <tr>
      <th>8806</th>
      <td>s8807</td>
      <td>Movie</td>
      <td>Zubaan</td>
      <td>Mozez Singh</td>
      <td>Vicky Kaushal, Sarah-Jane Dias, Raaghav Chanan...</td>
      <td>India</td>
      <td>March 2, 2019</td>
      <td>2015</td>
      <td>TV-14</td>
      <td>111 min</td>
      <td>Dramas, International Movies, Music &amp; Musicals</td>
      <td>A scrappy but poor boy worms his way into a ty...</td>
    </tr>
  </tbody>
</table>
<p>8807 rows × 12 columns</p>
</div>



### Column names and types


```python
netflix.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 8807 entries, 0 to 8806
    Data columns (total 12 columns):
     #   Column        Non-Null Count  Dtype 
    ---  ------        --------------  ----- 
     0   show_id       8807 non-null   object
     1   type          8807 non-null   object
     2   title         8807 non-null   object
     3   director      6173 non-null   object
     4   cast          7982 non-null   object
     5   country       7976 non-null   object
     6   date_added    8797 non-null   object
     7   release_year  8807 non-null   int64 
     8   rating        8803 non-null   object
     9   duration      8804 non-null   object
     10  listed_in     8807 non-null   object
     11  description   8807 non-null   object
    dtypes: int64(1), object(11)
    memory usage: 825.8+ KB
    

### Numerical column 'describe'


```python
netflix.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>release_year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>8807.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2014.180198</td>
    </tr>
    <tr>
      <th>std</th>
      <td>8.819312</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1925.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>2013.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>2017.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2019.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2021.000000</td>
    </tr>
  </tbody>
</table>
</div>



# Phase 3: Process


### Checking for missing data


```python
missing_data = netflix.isna().sum().sort_values(ascending=False)
missing_data
```




    director        2634
    country          831
    cast             825
    date_added        10
    rating             4
    duration           3
    show_id            0
    type               0
    title              0
    release_year       0
    listed_in          0
    description        0
    dtype: int64




```python
netflix_isna = pd.isna(netflix['director'])
netflix[netflix_isna]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>show_id</th>
      <th>type</th>
      <th>title</th>
      <th>director</th>
      <th>cast</th>
      <th>country</th>
      <th>date_added</th>
      <th>release_year</th>
      <th>rating</th>
      <th>duration</th>
      <th>listed_in</th>
      <th>description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>s2</td>
      <td>TV Show</td>
      <td>Blood &amp; Water</td>
      <td>NaN</td>
      <td>Ama Qamata, Khosi Ngema, Gail Mabalane, Thaban...</td>
      <td>South Africa</td>
      <td>September 24, 2021</td>
      <td>2021</td>
      <td>TV-MA</td>
      <td>2 Seasons</td>
      <td>International TV Shows, TV Dramas, TV Mysteries</td>
      <td>After crossing paths at a party, a Cape Town t...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>s4</td>
      <td>TV Show</td>
      <td>Jailbirds New Orleans</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>September 24, 2021</td>
      <td>2021</td>
      <td>TV-MA</td>
      <td>1 Season</td>
      <td>Docuseries, Reality TV</td>
      <td>Feuds, flirtations and toilet talk go down amo...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>s5</td>
      <td>TV Show</td>
      <td>Kota Factory</td>
      <td>NaN</td>
      <td>Mayur More, Jitendra Kumar, Ranjan Raj, Alam K...</td>
      <td>India</td>
      <td>September 24, 2021</td>
      <td>2021</td>
      <td>TV-MA</td>
      <td>2 Seasons</td>
      <td>International TV Shows, Romantic TV Shows, TV ...</td>
      <td>In a city of coaching centers known to train I...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>s11</td>
      <td>TV Show</td>
      <td>Vendetta: Truth, Lies and The Mafia</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>September 24, 2021</td>
      <td>2021</td>
      <td>TV-MA</td>
      <td>1 Season</td>
      <td>Crime TV Shows, Docuseries, International TV S...</td>
      <td>Sicily boasts a bold "Anti-Mafia" coalition. B...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>s15</td>
      <td>TV Show</td>
      <td>Crime Stories: India Detectives</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>September 22, 2021</td>
      <td>2021</td>
      <td>TV-MA</td>
      <td>1 Season</td>
      <td>British TV Shows, Crime TV Shows, Docuseries</td>
      <td>Cameras following Bengaluru police on the job ...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>8795</th>
      <td>s8796</td>
      <td>TV Show</td>
      <td>Yu-Gi-Oh! Arc-V</td>
      <td>NaN</td>
      <td>Mike Liscio, Emily Bauer, Billy Bob Thompson, ...</td>
      <td>Japan, Canada</td>
      <td>May 1, 2018</td>
      <td>2015</td>
      <td>TV-Y7</td>
      <td>2 Seasons</td>
      <td>Anime Series, Kids' TV</td>
      <td>Now that he's discovered the Pendulum Summonin...</td>
    </tr>
    <tr>
      <th>8796</th>
      <td>s8797</td>
      <td>TV Show</td>
      <td>Yunus Emre</td>
      <td>NaN</td>
      <td>Gökhan Atalay, Payidar Tüfekçioglu, Baran Akbu...</td>
      <td>Turkey</td>
      <td>January 17, 2017</td>
      <td>2016</td>
      <td>TV-PG</td>
      <td>2 Seasons</td>
      <td>International TV Shows, TV Dramas</td>
      <td>During the Mongol invasions, Yunus Emre leaves...</td>
    </tr>
    <tr>
      <th>8797</th>
      <td>s8798</td>
      <td>TV Show</td>
      <td>Zak Storm</td>
      <td>NaN</td>
      <td>Michael Johnston, Jessica Gee-George, Christin...</td>
      <td>United States, France, South Korea, Indonesia</td>
      <td>September 13, 2018</td>
      <td>2016</td>
      <td>TV-Y7</td>
      <td>3 Seasons</td>
      <td>Kids' TV</td>
      <td>Teen surfer Zak Storm is mysteriously transpor...</td>
    </tr>
    <tr>
      <th>8800</th>
      <td>s8801</td>
      <td>TV Show</td>
      <td>Zindagi Gulzar Hai</td>
      <td>NaN</td>
      <td>Sanam Saeed, Fawad Khan, Ayesha Omer, Mehreen ...</td>
      <td>Pakistan</td>
      <td>December 15, 2016</td>
      <td>2012</td>
      <td>TV-PG</td>
      <td>1 Season</td>
      <td>International TV Shows, Romantic TV Shows, TV ...</td>
      <td>Strong-willed, middle-class Kashaf and carefre...</td>
    </tr>
    <tr>
      <th>8803</th>
      <td>s8804</td>
      <td>TV Show</td>
      <td>Zombie Dumb</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>July 1, 2019</td>
      <td>2018</td>
      <td>TV-Y7</td>
      <td>2 Seasons</td>
      <td>Kids' TV, Korean TV Shows, TV Comedies</td>
      <td>While living alone in a spooky town, a young g...</td>
    </tr>
  </tbody>
</table>
<p>2634 rows × 12 columns</p>
</div>



### Checking for duplicates


```python
netflix['show_id'].duplicated().any()
```




    False



### Changing the date format of the column 'date_added' to 'datetime'



```python
netflix['date_added']= pd.to_datetime(netflix['date_added'].str.strip(), format= "%B %d, %Y") 
netflix
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>show_id</th>
      <th>type</th>
      <th>title</th>
      <th>director</th>
      <th>cast</th>
      <th>country</th>
      <th>date_added</th>
      <th>release_year</th>
      <th>rating</th>
      <th>duration</th>
      <th>listed_in</th>
      <th>description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>s1</td>
      <td>Movie</td>
      <td>Dick Johnson Is Dead</td>
      <td>Kirsten Johnson</td>
      <td>NaN</td>
      <td>United States</td>
      <td>2021-09-25</td>
      <td>2020</td>
      <td>PG-13</td>
      <td>90 min</td>
      <td>Documentaries</td>
      <td>As her father nears the end of his life, filmm...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>s2</td>
      <td>TV Show</td>
      <td>Blood &amp; Water</td>
      <td>NaN</td>
      <td>Ama Qamata, Khosi Ngema, Gail Mabalane, Thaban...</td>
      <td>South Africa</td>
      <td>2021-09-24</td>
      <td>2021</td>
      <td>TV-MA</td>
      <td>2 Seasons</td>
      <td>International TV Shows, TV Dramas, TV Mysteries</td>
      <td>After crossing paths at a party, a Cape Town t...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>s3</td>
      <td>TV Show</td>
      <td>Ganglands</td>
      <td>Julien Leclercq</td>
      <td>Sami Bouajila, Tracy Gotoas, Samuel Jouy, Nabi...</td>
      <td>NaN</td>
      <td>2021-09-24</td>
      <td>2021</td>
      <td>TV-MA</td>
      <td>1 Season</td>
      <td>Crime TV Shows, International TV Shows, TV Act...</td>
      <td>To protect his family from a powerful drug lor...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>s4</td>
      <td>TV Show</td>
      <td>Jailbirds New Orleans</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021-09-24</td>
      <td>2021</td>
      <td>TV-MA</td>
      <td>1 Season</td>
      <td>Docuseries, Reality TV</td>
      <td>Feuds, flirtations and toilet talk go down amo...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>s5</td>
      <td>TV Show</td>
      <td>Kota Factory</td>
      <td>NaN</td>
      <td>Mayur More, Jitendra Kumar, Ranjan Raj, Alam K...</td>
      <td>India</td>
      <td>2021-09-24</td>
      <td>2021</td>
      <td>TV-MA</td>
      <td>2 Seasons</td>
      <td>International TV Shows, Romantic TV Shows, TV ...</td>
      <td>In a city of coaching centers known to train I...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>8802</th>
      <td>s8803</td>
      <td>Movie</td>
      <td>Zodiac</td>
      <td>David Fincher</td>
      <td>Mark Ruffalo, Jake Gyllenhaal, Robert Downey J...</td>
      <td>United States</td>
      <td>2019-11-20</td>
      <td>2007</td>
      <td>R</td>
      <td>158 min</td>
      <td>Cult Movies, Dramas, Thrillers</td>
      <td>A political cartoonist, a crime reporter and a...</td>
    </tr>
    <tr>
      <th>8803</th>
      <td>s8804</td>
      <td>TV Show</td>
      <td>Zombie Dumb</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2019-07-01</td>
      <td>2018</td>
      <td>TV-Y7</td>
      <td>2 Seasons</td>
      <td>Kids' TV, Korean TV Shows, TV Comedies</td>
      <td>While living alone in a spooky town, a young g...</td>
    </tr>
    <tr>
      <th>8804</th>
      <td>s8805</td>
      <td>Movie</td>
      <td>Zombieland</td>
      <td>Ruben Fleischer</td>
      <td>Jesse Eisenberg, Woody Harrelson, Emma Stone, ...</td>
      <td>United States</td>
      <td>2019-11-01</td>
      <td>2009</td>
      <td>R</td>
      <td>88 min</td>
      <td>Comedies, Horror Movies</td>
      <td>Looking to survive in a world taken over by zo...</td>
    </tr>
    <tr>
      <th>8805</th>
      <td>s8806</td>
      <td>Movie</td>
      <td>Zoom</td>
      <td>Peter Hewitt</td>
      <td>Tim Allen, Courteney Cox, Chevy Chase, Kate Ma...</td>
      <td>United States</td>
      <td>2020-01-11</td>
      <td>2006</td>
      <td>PG</td>
      <td>88 min</td>
      <td>Children &amp; Family Movies, Comedies</td>
      <td>Dragged from civilian life, a former superhero...</td>
    </tr>
    <tr>
      <th>8806</th>
      <td>s8807</td>
      <td>Movie</td>
      <td>Zubaan</td>
      <td>Mozez Singh</td>
      <td>Vicky Kaushal, Sarah-Jane Dias, Raaghav Chanan...</td>
      <td>India</td>
      <td>2019-03-02</td>
      <td>2015</td>
      <td>TV-14</td>
      <td>111 min</td>
      <td>Dramas, International Movies, Music &amp; Musicals</td>
      <td>A scrappy but poor boy worms his way into a ty...</td>
    </tr>
  </tbody>
</table>
<p>8807 rows × 12 columns</p>
</div>



### Checking unique type of data of the column 'Type'

There are only two types of data: Movie and TV Show


```python
type_data = netflix.type.unique()
type_data
```




    array(['Movie', 'TV Show'], dtype=object)




# Phase 4 Exploratory Data Analysis


## About Netflix streaming platform



#### Number of movies/tv-shows added to the streaming platform by Year


```python
# year with the most added movies/tv-shows
netflix_release_year = netflix.date_added.dt.year.astype('Int64').value_counts()
netflix_release_year
```




    2019    2016
    2020    1879
    2018    1649
    2021    1498
    2017    1188
    2016     429
    2015      82
    2014      24
    2011      13
    2013      11
    2012       3
    2008       2
    2009       2
    2010       1
    Name: date_added, dtype: Int64



#### The month with the most added movies/tv-shows


```python
netflix_release_month = netflix.date_added.dt.month.astype('Int64').value_counts()
netflix_release_month
```




    7     827
    12    813
    9     770
    4     764
    10    760
    8     755
    3     742
    1     738
    6     728
    11    705
    5     632
    2     563
    Name: date_added, dtype: Int64



#### Day with the most added movies/tv-shows



```python
netflix_release_day = netflix.date_added.dt.day.astype('Int64').value_counts()
netflix_release_day
```




    1     2212
    15     687
    2      325
    16     289
    31     274
    20     249
    19     243
    5      231
    22     230
    10     214
    30     210
    6      210
    18     207
    26     206
    8      201
    14     198
    25     197
    27     195
    7      194
    21     193
    28     190
    23     184
    12     181
    17     180
    13     175
    4      175
    24     159
    3      151
    11     149
    9      147
    29     141
    Name: date_added, dtype: Int64



#### Number of Movies vs. TV-Shows


```python
netflix_type = netflix.type.value_counts()
netflix_type
```




    Movie      6131
    TV Show    2676
    Name: type, dtype: int64



## About the Movies/TV-Shows


#### The year with the most releases movies/tv-shows


```python
movietv_release_year = netflix.release_year.value_counts()
movietv_release_year
```




    2018    1147
    2017    1032
    2019    1030
    2020     953
    2016     902
            ... 
    1966       1
    1925       1
    1947       1
    1959       1
    1961       1
    Name: release_year, Length: 74, dtype: int64



#### The oldest movie/tv-show on streaming


```python
netflix[netflix['release_year']== 1925]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>show_id</th>
      <th>type</th>
      <th>title</th>
      <th>director</th>
      <th>cast</th>
      <th>country</th>
      <th>date_added</th>
      <th>release_year</th>
      <th>rating</th>
      <th>duration</th>
      <th>listed_in</th>
      <th>description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4250</th>
      <td>s4251</td>
      <td>TV Show</td>
      <td>Pioneers: First Women Filmmakers*</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2018-12-30</td>
      <td>1925</td>
      <td>TV-14</td>
      <td>1 Season</td>
      <td>TV Shows</td>
      <td>This collection restores films from women who ...</td>
    </tr>
  </tbody>
</table>
</div>



#### Top 30 Countries producing the most movies/tv-shows


```python
# country unique
#netflix['country'].unique()
```


```python
# new dataset for the country count
country_count = netflix.copy()
country_count = pd.concat([country_count, netflix['country'].str.split(",", expand=True)], axis=1)
country_count = country_count.melt(id_vars=["type","title"], value_vars=range(12), value_name="Country")
country_count = country_count[country_count["Country"].notna()]
country_count["Country"] = country_count["Country"].str.strip()
country_count
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>type</th>
      <th>title</th>
      <th>variable</th>
      <th>Country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Movie</td>
      <td>Dick Johnson Is Dead</td>
      <td>0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>1</th>
      <td>TV Show</td>
      <td>Blood &amp; Water</td>
      <td>0</td>
      <td>South Africa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>TV Show</td>
      <td>Kota Factory</td>
      <td>0</td>
      <td>India</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Movie</td>
      <td>Sankofa</td>
      <td>0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>8</th>
      <td>TV Show</td>
      <td>The Great British Baking Show</td>
      <td>0</td>
      <td>United Kingdom</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>78859</th>
      <td>Movie</td>
      <td>The Look of Silence</td>
      <td>8</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>85496</th>
      <td>Movie</td>
      <td>Barbecue</td>
      <td>9</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <th>87666</th>
      <td>Movie</td>
      <td>The Look of Silence</td>
      <td>9</td>
      <td>Netherlands</td>
    </tr>
    <tr>
      <th>94303</th>
      <td>Movie</td>
      <td>Barbecue</td>
      <td>10</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>103110</th>
      <td>Movie</td>
      <td>Barbecue</td>
      <td>11</td>
      <td>Uruguay</td>
    </tr>
  </tbody>
</table>
<p>10019 rows × 4 columns</p>
</div>




```python
# countries unique
#country_count.Country.unique()
```


```python
# countries with the most number of content streaming
country_count.Country.value_counts()
```




    United States     3690
    India             1046
    United Kingdom     806
    Canada             445
    France             393
                      ... 
    Malawi               1
    Slovakia             1
    Armenia              1
    Panama               1
    Mongolia             1
    Name: Country, Length: 123, dtype: int64



#### Top 30 Cast members with the most content


```python
#New dataset for the cast count
cast_count = netflix.copy()
cast_count = pd.concat([cast_count, netflix['cast'].str.split(",", expand=True)], axis=1)
cast_count = cast_count.melt(id_vars=["type","title"], value_vars=range(44), value_name="Cast_name")
cast_count = cast_count[cast_count["Cast_name"].notna()]
cast_count["Cast_name"] = cast_count["Cast_name"].str.strip()
cast_count
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>type</th>
      <th>title</th>
      <th>variable</th>
      <th>Cast_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>TV Show</td>
      <td>Blood &amp; Water</td>
      <td>0</td>
      <td>Ama Qamata</td>
    </tr>
    <tr>
      <th>2</th>
      <td>TV Show</td>
      <td>Ganglands</td>
      <td>0</td>
      <td>Sami Bouajila</td>
    </tr>
    <tr>
      <th>4</th>
      <td>TV Show</td>
      <td>Kota Factory</td>
      <td>0</td>
      <td>Mayur More</td>
    </tr>
    <tr>
      <th>5</th>
      <td>TV Show</td>
      <td>Midnight Mass</td>
      <td>0</td>
      <td>Kate Siegel</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Movie</td>
      <td>My Little Pony: A New Generation</td>
      <td>0</td>
      <td>Vanessa Hudgens</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>380555</th>
      <td>TV Show</td>
      <td>Social Distance</td>
      <td>43</td>
      <td>Niles Fitch</td>
    </tr>
    <tr>
      <th>382150</th>
      <td>TV Show</td>
      <td>Creeped Out</td>
      <td>43</td>
      <td>Andonis Anthony</td>
    </tr>
    <tr>
      <th>382475</th>
      <td>TV Show</td>
      <td>Black Mirror</td>
      <td>43</td>
      <td>Michael Smiley</td>
    </tr>
    <tr>
      <th>382921</th>
      <td>TV Show</td>
      <td>COMEDIANS of the world</td>
      <td>43</td>
      <td>Adib Alkhalidey</td>
    </tr>
    <tr>
      <th>384887</th>
      <td>Movie</td>
      <td>Arthur Christmas</td>
      <td>43</td>
      <td>Brian Cummings</td>
    </tr>
  </tbody>
</table>
<p>64105 rows × 4 columns</p>
</div>




```python
cast_count.Cast_name.value_counts()[:30]
```




    Anupam Kher            43
    Shah Rukh Khan         35
    Julie Tejwani          33
    Takahiro Sakurai       32
    Naseeruddin Shah       32
    Rupa Bhimani           31
    Om Puri                30
    Akshay Kumar           30
    Yuki Kaji              29
    Paresh Rawal           28
    Amitabh Bachchan       28
    Boman Irani            27
    Vincent Tong           26
    Rajesh Kava            26
    Andrea Libman          25
    Kareena Kapoor         25
    John Cleese            24
    Samuel L. Jackson      24
    Tara Strong            23
    Jigna Bhardwaj         23
    Fred Tatasciore        23
    Daisuke Ono            22
    Kay Kay Menon          21
    Nawazuddin Siddiqui    21
    Ajay Devgn             21
    Ashleigh Ball          21
    Nicolas Cage           21
    Junichi Suwabe         21
    David Attenborough     20
    Salman Khan            20
    Name: Cast_name, dtype: int64



# Phase 5: Visualization

### Movies vs. TV-Shows


```python
fig=px.histogram(netflix, x= 'type', color= 'type',
             title="Movies vs. TV-Shows",
             color_discrete_sequence= px.colors.sequential.Sunsetdark)
fig.show()

```


    
![svg](output_40_0.svg)
    


### Number of Movies/TV-Shows added by Year


```python
fig=px.histogram(netflix, x= netflix['date_added'].dt.year, color= netflix['type'],
             title="Netflix number of Movie/TV Show by year",
             color_discrete_sequence= px.colors.sequential.Sunsetdark,  
              labels=dict(x="Year", color= "Type")                     
                   )
fig.show()
```


    
![svg](output_42_0.svg)
    


### Number of Movies/TV-Shows added by Month

#### Dropping 'NA' records from the column 'date_added'

Dropping 10 records from the column 'date_added' that contain 'NA' values


```python
#counting the number of 'NA' on the column 'date_added'
netflix['date_added'].isna().sum()
```




    10




```python
#dropping 'NA'
netflix = netflix.dropna(subset=['date_added'])
```


```python
fig=px.histogram(netflix, x= netflix['date_added'].dt.month, color= netflix['type'],
             color_discrete_sequence= px.colors.sequential.Sunsetdark,
             title="Movies/TV Shows added by Month",
             labels=dict(x="Month")) 
fig.show()
```


    
![svg](output_47_0.svg)
    


### Number of Movies/TV-Shows added by Day


```python
fig=px.histogram(netflix, x= netflix['date_added'].dt.day,color= netflix['type'],
             color_discrete_sequence= px.colors.sequential.Sunsetdark,            
             title="Movies/TV Shows added by Day",
             labels=dict(x="Day")) 
fig.show()
```


    
![svg](output_49_0.svg)
    


## About the content

### Number of Movies/TV-Shows by year of release


```python
fig=px.histogram(netflix, x= 'release_year', color= 'type',
             title="Number of Movies/TV-Shows by year of release",
             color_discrete_sequence= px.colors.sequential.Sunsetdark,  
             labels={'release_year':'Year of release'}                     
                   )
fig.show()
```


    
![svg](output_51_0.svg)
    


### Top 30 Countries with the most streaming content


```python
fig=px.histogram(country_count, x= 'Country', color= 'type',
        title="Top 30 Countries with the most streaming content",
        color_discrete_sequence= px.colors.sequential.Sunsetdark).update_xaxes(
        categoryorder="total descending",range=(0, 30))
fig.show()
```


    
![svg](output_53_0.svg)
    





# Findings


### About Netflix

* There are more Movies than TV-Shows available on streaming. 6131 movies and 2676 tv-shows.
* 2019 is the year with the most content addition on the streaming platform, 2016 movie/tv-shows added, followed by 2020 with 1879, and 2018 with 1649 total.
* July and December are the months with the most content addition, 827 and 813 movie/tv-shows added.
* Netflix adds content on the first day of the month more than any other day.

### About the content available

* Among the contents available 1147 of them were originally released in 2018 followed by 2017 with 1032, and 2019 with 1030 total.
* Pioneers: First Women Filmmakers is the oldest content available on streaming. It's a collection of restored films dating from 1925.
* The United States is the country that produces the most of the content with 3690 titles, followed by India 1046 titles and the United Kingdom 806 titles.
* Anupam Kher is the actor with the higher number of titles, 43 films. [Anupam Kher](http://en.wikipedia.org/wiki/Anupam_Kher)  is an Indian actor, director, and producer that has appeared in over 500 films.




