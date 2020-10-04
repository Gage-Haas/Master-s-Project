# Master-s-Project
Master's Project

This project is an attempt at finding a way to accurately cluster populations that are very similar to each other along with populations that are very different. 
For examle Greek & Albanians are very genetically similiar, and so are Koreans & Japanese. Because of this when all four of these populations are clustered together, a K-means algorithm will want to cluster these individuals into two populations even though they are really four. Also due to the gentic variance of individuals being greatest within individuals of the same populaiton, when you attempt to just cluster these two similar populations together it results in the outlier point becoming it's own cluster. So a large percentage of individuals will belong to one cluster, and outlier points will result in the other cluster. This gets worse the more genetically similar the populations are. For a cluster between japanes and korean I had one singular point belonging to it's own cluster. With albanians and greeks it clustered more accurately when just looking at this population. 

PCA is a dimensionality reduction technique that can help differentiate the genetic data some, so the clustering between two similar populations was improved.
However, even when utilizing PCA this did not help differentiate two similar groups when all four groups were looked at, as the two sets are very genetically different. 

The data files ending in Region_Data.txt contain SNP values that have been matched with the other corresponding data files.
The SNPs were cleaned by eliminating any SNP that had a missing value of 9 for all individuals, even if that SNP wasn't missing for the other populations.

You can find all necessary files needed to run these codes in the Matched_Datasets.zip folder.

https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1003480

The paper in the above link provides a method of reducing the genetic variation within populations while maximizing the genetic varitation between popultaions.

First a T1 statistic is calculated. This takes a long time to compute, so you can also just load the results of that calculation directly with the T1_matrix.csv file. 

A distance matrix is then calculated as every element being 1 - T1 for each row/columns corresponding T1 statistic

The dissimilarity matrix is then calculated as the variance of the distances between points in thie distance matrix.

In order to confirm that this dissimilarity matrix was really able to reduce the genetic variation within populations. I PCA reduced the dissimilarity matrix into 3 principal components, and then I clustered these principal components with K -Means. I then generated two plots of the principal components, one with the true class assignments over the components and the other with the K- Means class assignments. You can see from these graphs that this matrix transformation provides some differentiation between like populations when the dissimilar populations are also included.

Although the K - Means gave better results using the dissimilarity matrix, I tried to explore an improvement of this clustering by utilizing a genetic algorithm to maximize the between, or among populations, sum of squares. This will conversely minimize the genetic variance within populations as well. 

The Sum of Squares Among Populations SSAP is defined as the Sum of Squares of the Dissimilarity matrix - the Sum of Squares of each population.

I create a random populaiton of clusters and then I calculate the SSAP for each cluster guess by taking the corresponding data from the original data based on the clustering guesses. I then compute the sum of squares within populations for each population and then add these togethere. The sum of these within population sum of squares is  then subtracted from the Sum of Squares of the dissimilarity matrix, which gives the SSAP value which is what we want to maximize with the genetic algorithm. 

I then take the n best solutions from the random guesses by taking the n highest ssap scores.

I then make offspring from these solutions at random, every guess will mate but their mating partner will be random.

I then mutate the offspring at random. I provide a perecentage of chance for a mutation to occur, and then also a random number of individuals will get assigned a new cluster, which is also determined at random.

I then keep track of what guess has given me the best ssap score. 

After every iteration the mutated offspring are then introduced into the next population along with an additional rnumber of random guesses.

