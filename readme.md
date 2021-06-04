
# Music Sharing on Reddit

This is the official repository for the paper ["Imagine All the People: Characterizing Social Music Sharing on Reddit"](http://www.cs.toronto.edu/~ashton/pubs/music-on-reddit-icwsm21.pdf). It contains RedditMusic, our dataset of 1.3 million instances of music sharing on Reddit, and all the materials necessary to replicate our analyses. 

## The RedditMusic Dataset

To create RedditMusic, we extracted all instances of songs being shared via YouTube videos or Spotify links. A full explanation is available in the "Data" section of the [paper](http://www.cs.toronto.edu/~ashton/pubs/music-on-reddit-icwsm21.pdf). The final dataset of 1.3 million instances of music sharing on Reddit is located at `/data/Reddit_Sub_Com_f_genre.csv` and consists of all shares of artists who were shared more than 20 times, along with their respective *social genres* (discussed below). 

## Embedding artists into Reddit space to create *social genres*
To study artists we used the Reddit embedding designed in previous work [[1]](http://www.cs.toronto.edu/~ashton/pubs/actdiv-www2019.pdf). The file `src/artist_genre/social_genres.ipynb` takes in the raw music sharing dataset, embeds musicians into the Reddit embedding and then clusters the artists into *social genres*.

Once the social genres are defined we run the file `src/artist_genre/naming_genres.ipynb` to generate visuals explaining each *social genre*. This method provides a broad overview of the social genres, but some social genres require deeper analysis. 

Then, `src/artist_genre/cosine_similarity.ipynb` can be used to calculate the cosine similarity between both the artists and the social genres. The cosine similarity files `artist_cosine_similarity.csv` and `genre_cosine_similarity.csv` generated in this file are later used in the file `heatmap.ipynb` which generates the heatmaps in the paper.

Note that when we create the heatmaps we require artist release date information to create the colourbars on the sides of the heatmap. This is created in the file `src/artist_genre/release_date.ipynb`.

We also compare the *social genres* to words embedded into the same Reddit space.  We use the file `src/artist_genre/wordclouds.ipynb` to generate word clouds for each of the *social genres*. 

## Social dimensions
Similar to how word embeddings are capable of encoding semantic relationships, the Reddit community embedding is capable of capturing semantic relationships between Reddit communities. In particular, this enabled the creation of social dimensions in the Reddit embedding that capture salient social constructs [[2]](http://www.cs.toronto.edu/~ashton/pubs/cultural-dims2020.pdf). Each community is weighed on several social dimensions like gender, age, and political leanings. Using this method we can augment our understanding of musicians. 

### Projecting artists and *social genres* onto the social dimensions.
We begin by studying how the Reddit community as a whole differs from the music-sharing subset of Reddit. For this we create a many density plot using the file `src/social_dimensions/many_density_plot.ipynb`. 

After we provide a more local analysis of how different artists and *social genres* differ on the social dimensions. The main plot is the is a scatter plot featuring how the various social genres differ on the social dimensions. This plot is created in file `src/social_dimensions/social_stripplot.ipynb`. 

## Extra-musical sharing
To measure extra-musical sharing we develop two metrics, based on two different observations. First, extra-musical sharing is more likely to occur in a wide range of contexts. Second, extra-musical sharing is often meme-driven. 

### Generalist-Specialist score
To capture the first observation we adapted the [GS-score](http://www.cs.toronto.edu/~ashton/pubs/actdiv-www2019.pdf) to measure the diversity of contexts a song is shared in. The code to do this is in `src/extra_musicality/gs_score`. It outputs a dataset that sorts artists by how widely shared they are. 

### Meme score
To quantify the second observation, we first calculate the z-score between artists and subreddits in which they are shared in. This is done in `src/extra_musicality/artist_subreddit_proportions.ipynb`.  Then we run the file `src/extra_musicality/vectorize_dimensions.ipynb` to vectorize the z-scores into the embedding. Finally `meme_score.ipynb` calculates the cosine similarity between the "meme vector" and the artists in our embedding. 


Related work:
[1] Waller, I., & Anderson, A. (2019, May). [Generalists and specialists: Using community embeddings to quantify activity diversity in online platforms](http://www.cs.toronto.edu/~ashton/pubs/actdiv-www2019.pdf). In The World Wide Web Conference (pp. 1954-1964).

[2] Waller, I., & Anderson, A. (2020). [Community embeddings reveal large-scale cultural organization of online platforms](http://www.cs.toronto.edu/~ashton/pubs/cultural-dims2020.pdf). arXiv preprint arXiv:2010.00590.

