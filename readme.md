
# Music Sharing on Reddit

This is the official Github for our paper "Imagine All the People: Characterizing Social Music Sharing on Reddit". This repository will link the materials necessary to recreate our analysis. This includes both the music sharing dataset and the Python files for generating visuals. 



## Introduction to the dataset

### How did we create the dataset? 
To create the dataset we found all instances of musicians shared through their YouTube videos or Spotify links. A full explanation is available in the "data" section of our paper. The final dataset can be at `/data/Reddit_Sub_Com_f_genre.csv' and this 
consists of all artists shared more than 20 times alongside their respective *social genres* (discussed below). 

## Reddit embedding
To study artists we relied on the Reddit embedding designed in previous work [1]. The embedding we used has not been released yet, but can be remade using a method similar to that in the previous work.. 
The vectors consist of the 150-dimension Reddit embedding and the metadata provides some statistics about each subreddit. 

## Embedding artists into Reddit space to create *social genres*
The file `src/artist_genre/social_genres.ipynb` takes in the raw music sharing dataset, embeds musicians into the Reddit embedding and then clusters the artists into *social genres*

Once the social genres are defined we run the file `src/artist_genre/naming_genres.ipynb` to generate visuals explaining each *social genre*. This method provides a broad overview of the social genres, but some social genres require deeper analysis. 

After `src/artist_genre/cosine_similarity.ipynb` can be used to calculate the cosine similarity between either the artists or social genres. The cosine similarity files `artist_cosine_similarity.csv` and `genre_cosine_similarity.csv` generated in this file are later used in the file `heatmap.ipynb` which generates the heatmap seen here <INCLUDE VISUAL OF THE HEATMAP>.

Note that when we create the heatmaps we require artist release date information to create the colourbars on the sides of the heatmap. This is created in the file `src/artist_genre/release_date.ipynb` 


### Word comparison
We also compare the *social genres* to words embedded into the same Reddit space.  We use the file `src/artist_genre/wordclouds.ipynb` to generate word clouds for each of the *social genres*. 


## Social dimensions
Brief introduction: Similar to how word embeddings are capable of encoding semantic relationships, the Reddit embedding is capable of capturing underlying connections between Reddit communities. In particular, this has encouraged the creation of social dimensions in the Reddit embedding which can be found in existing literature [2]. Each community is weighed on several social dimensions like gender, age, and political leanings, these weights are found in `data/scores_z.csv`. Using this method we can augment our understanding of musicians. 

### Projected artists and cultures onto the social dimensions.
We begin by studying how the Reddit community as a whole differs from the music-sharing subset of Reddit. For this we create a many density plot using the file `src/social_dimensions/many_density_plot.ipynb`. 

After we provide a more local analysis of how different artists and *social genres* differ on the social dimensions. The main plot is the is a scatter plot featuring how the various social genres differ on the social dimensions. This plot is created in file `src/social_dimensions/social_stripplot.ipynb`. 


## Extra-musical sharing
To measure extra-musical sharing we develop two metrics, based on two different observations. First, extra-musical sharing is more likely to occur in a wide range of contexts. Second, extra-musical sharing can be associated with a joke. 

### GS Score
To capture the first observation we created the GS Score. To create the GS Score we run`src/extra_musicality/gs_score`. In the end we'll have a dataset that sorts artists by how widely shared they are. 

### Meme Score
To create the meme score
we first need to calculate the z-score between artists and subreddits in which they are shared in. This is done in `src/extra_musicality/artist_subreddit_proportions.ipynb`.  After we run the file `src/extra_musicality/vectorize_dimensions.ipynb` to vectorize the z-scores into the embedding. Finally `meme_score.ipynb` is run to calculate the cosine similarity between the "meme vector" and the artists in our embedding. 


Related work:
To better grasp some of the ideas outlined here, we recommend you look over
[1] Waller, I., & Anderson, A. (2019, May). Generalists and specialists: Using community embeddings to quantify activity diversity in online platforms. In The World Wide Web Conference (pp. 1954-1964).
[2] Waller, I., & Anderson, A. (2020). Community embeddings reveal large-scale cultural organization of online platforms. arXiv preprint arXiv:2010.00590.

