# Wrangling details

In this document we will illustrate the details of our wrangling process including mostly ( Access and Cleaning ) for each of three files:
* `twitter-archive-enhanced.csv`.
* `tweet-json.txt`.
* `image-predictions.tsv`.
***
## Access

### Twitter Archive Enhanced.

#### Quality Issues.

* Those columns referes to IDs that should be object instead of fload and int data types [`tweet_id`,`in_reply_to_status_id`,`in_reply_to_user_id`,`retweeted_status_id`,`retweeted_status_user_id`].
* `None` values should be replaced with `NaN` (this may help us in cleaning and merging and save us some few lines of code).
* [`timestamp`,`retweeted_status_timestamp`] should be conferted to datatime data type.
* There are some missing `expanded_urls` values they should be filled.
* `None` needs to be replaced with `Nan` in `name` column.
* there was also invalid numerator and denominator ratings which were cleaned and corrected while performing some analysis which are in row index 313 with wrong value of 960/10 the right ones are 13/10 extracted from text it was detected while performing the analysis.

#### Tidiness Issues

* There should be another table (*Retweet Table*) that contains info about the retweets, doing so will save us storage and there won't be `NaN` values.
* There should be another table dedicated for the users who replied to the tweets.

there are new files created 
* `Retweet_Table_new.csv`
* `Tweets_Replies.csv`
* `twitter_archive_master.csv`

***
### Image prediction.

This table doesn't have so many issues at least from my little investigation.
```
In [12]: 
image_prediction.info()

Out [12]: 
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 2075 entries, 0 to 2074
Data columns (total 12 columns):
 #   Column    Non-Null Count  Dtype  
---  ------    --------------  -----  
 0   tweet_id  2075 non-null   int64  
 1   jpg_url   2075 non-null   object 
 2   img_num   2075 non-null   int64  
 3   p1        2075 non-null   object 
 4   p1_conf   2075 non-null   float64
 5   p1_dog    2075 non-null   bool   
 6   p2        2075 non-null   object 
 7   p2_conf   2075 non-null   float64
 8   p2_dog    2075 non-null   bool   
 9   p3        2075 non-null   object 
 10  p3_conf   2075 non-null   float64
 11  p3_dog    2075 non-null   bool   
dtypes: bool(3), float64(3), int64(2), object(4)
memory usage: 152.1+ KB
```
as we can see there is no issues like missing values or wrong Dtypes and the data is pretty much tidy.

#### Qulaity issues 

* `tweet_id` should be converted to `object` data type.

***
### Twitter Json.
#### Qualtiy issues

* [`id`,`in_reply_to_status_id`,`in_reply_to_user_id`,`quoted_status_id`] should be `object` data type.

#### Tidiness issues 

* there are columns that doesn't contain any data and will be dropped [`user`,`geo`,`coordinates`,`contributors`].
* [`id_str`,`in_reply_to_status_id_str`,`in_reply_to_user_id_str`,`quoted_status_id_str`] should be removed because they are duplicates.
***

