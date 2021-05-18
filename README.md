# Recommender system for Books
## Background
A recommender system, or a recommendation system , is a subclass of information filtering system that aims to predict the "rating" a user would give to a particular item or product. Recommendation engine algorithms are usually categorized in two types -  Collaborative filtering models and Content-based models.   
1. **Collaborative filtering**: In this, user ratings are used in order to determine user or item similarities. The key emphasis therefore, is to predict the user's rating on the basis of information on users or item SIMILAR to the user or item in question by using the ratings given by user to items. It can therefore be achieved by either User-based or Item-based filtering.    
&nbsp;  
Consider user-item matrix with #rows=#user and #columns=#items
Given user X and item i, we have to predict rating given by user x to item i = Rxi.
&nbsp;  
a. **User-based**: Similarity between users(on the basis of user-item ratings) is the basis to predict the rating.  
![\Large Rxi = \frac{\sum_{y=1}^{N} SxyRyi}{\sum_{{y=1}^{N}}{Sxy}}](https://latex.codecogs.com/svg.latex?Rxi%20%3D%20%5Cfrac%7B%5Csum_%7By%3D1%7D%5E%7BN%7D%20SxyRyi%7D%7B%5Csum_%7B%7By%3D1%7D%5E%7BN%7D%7D%7BSxy%7D%7D)  
where  
N = set of K users most similar to user X; who have also rated item i  
Sxy = sim(user X, user Y)  
Ryi = Rating for item i by user Y  
&nbsp;  
b. **Item-based**: Similarity between items(on the basis of user-item ratings) is the basis to predict the rating.    
![\Large Rxi = \frac{\sum_{\substack{j\in{N}}} SijRxj}{\sum_{\substack{j\in{N}}}{Sij}}](https://latex.codecogs.com/svg.latex?Rxi%20%3D%20%5Cfrac%7B%5Csum_%7B%5Csubstack%7Bj%5Cin%7BN%7D%7D%7D%20SijRxj%7D%7B%5Csum_%7B%5Csubstack%7Bj%5Cin%7BN%7D%7D%7D%7BSij%7D%7D)  
where  
N = set of K items most similar to item i; that have also been rated by user X    
Sij = sim(item i, item j)  
Rxj = Rating for item j by user X 
&nbsp;  
**Notion of similarity: How to establish similarity?**  
Various methods are available for this like Jaccard Similarity, Cosine Similarity, Centered cosine etc.  
 
* Cosine similarity:   
E.g. similarity bewtween user A and user B = sim(A,B) = cos(rA,rB)  
where rA, rB are ratings vector for respective users.  
*Missing ratings problem*: This gives only a marginally correct answer, because it treats missing ratings as negative(not mathematically but the missing ratings are assigned 0 to calculate cosine thus assigning the worst possible value to missing ratings but that may not be true!)  
* Centered cosine: In this, we normalize the ratings by subtracting the mean of corresponding row. In doing so, the ratings of each user will be centered to '0'. So, '0' becomes the average rating for every user.  
=> +ve rating indicates that user liked it more than avg  
and -ve rating indicates that user liked it less than avg    
This solves the 'Missing ratings problem' as the missing ratings is although still considered 0, '0' here means avg rating and not the worst possibe rating.    
*Centered cosine or Pearson Correlation is used in this project.*
&nbsp;  

2. **Content-based**: In this method, items are recommended by predicting the item rating using the similarity of the said items. These algorithms try to recommend items that are similar to those that a user liked in the past (or is examining in the present). In particular, various candidate items are compared with items previously rated by the user and the best-matching items are recommended.
&nbsp;  
*User buys item A. We find an item B similar to A and recommend that to the user.*
&nbsp;  
Difference between item-based collabortaive fitering and content-based filtering. In both of these, we observe the similarity of user but in collaborative it is completely based on the user's ratings while in content-based, it depends on the actual similarity between two items, not on what the user has rated the two items in question.  
&nbsp;

## Dataset used:  
Book-Crossing Dataset collected by Cai-Nicolas Ziegler in a 4-week crawl (August / September 2004) from the Book-Crossing community is used in this project. 
&nbsp;  

### Format
*source: http://www2.informatik.uni-freiburg.de/~cziegler/BX/*
The Book-Crossing dataset comprises 3 tables.
* BX-Users
Contains the users. Note that user IDs (`User-ID`) have been anonymized and map to integers. Demographic data is provided (`Location`, `Age`) if available. Otherwise, these fields contain NULL-values.

* BX-Books
Books are identified by their respective ISBN. Invalid ISBNs have already been removed from the dataset. Moreover, some content-based information is given (`Book-Title`, `Book-Author`, `Year-Of-Publication`, `Publisher`), obtained from Amazon Web Services. Note that in case of several authors, only the first is provided. URLs linking to cover images are also given, appearing in three different flavours (`Image-URL-S`, `Image-URL-M`, `Image-URL-L`), i.e., small, medium, large. These URLs point to the Amazon web site.

* BX-Book-Ratings
**Contains the book rating information. Ratings (`Book-Rating`) are either explicit, expressed on a scale from 1-10 (higher values denoting higher appreciation), or implicit, expressed by 0.**  
&nbsp;  

## Model:
* Baseline model: The baseline model in this project is that of a simple Popularity-based recommender system i.e. based on the top or most popular books (by highest user ratings)
* Collaborative filtering: Both user-based and item-based collaborative filtering are implemented in this project. 


