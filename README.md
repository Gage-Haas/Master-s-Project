# Master-s-Project
Master's Project


The data files ending in Region_Data.txt contain SNP values that have been matched with the other corresponding data files.

The SNPs were cleaned by eliminating any SNP that had a missing value of 9 for all individuals, even if that SNP wasn't missing for the other populations.

Then a T1 statistic is calculated. This takes a long time to compute, so you can also just load the results of that calculation directly with the T1_matrix.csv file. 

A distance matrix is calculated as every element being 1 - T1 for each row/columns corresponding T1 statistic

The dissimilarity matrix is then calculated as the variance of the distances between points in thie distance matrix.

Then a GA is utilized to try to optimize the Sum of Squares Among Populations SSAP which is defined as the Sum of Squares of the Dissimilarity matrix - the Sum of Squares of each population.

I create a random populaiton of clusters and then I calculate the SSAP for each cluster guess by taking the corresponding data from the original data based on the clustering guesses. I then compute the sum of squares within populations for each population and then add these togethere. The sum of these within population sum of squares is  then subtracted from the Sum of Squares of the dissimilarity matrix, which gives the SSAP value which is what we want to maximize with the genetic algorithm. 

I then take the n best solutions from the random guesses by taking the n highest ssap scores.

I then make offspring from these solutions at random, every guess will mate but their mating partner will be random.

I then mutate the offspring at random. I provide a perecentage of chance for a mutation to occur, and then also a random number of individuals will get assigned a new cluster, which is also determined at random.

I then keep track of what guess has given me the best ssap score. 

After every iteration the mutated offspring are then introduced into the next population along with an additional rnumber of random guesses.

