# graph_matching_for_data_dictionary_harmonization
Provide methods to automatically match entries in a data dictionary based on structure between items

## Task

Given are two data dictionaries A, and B, and example data for both. We are looking for a match between the items in the two data dictionaries so that compatible items are grouped together. 

For example let data dictionary A be the data dictionary from the HCP project and data dictionary B be the data dictionary from the ABCD study. Create an item to item mapping for each item in A to an item in B.

### Trivial

Of course we can match by data type (continuous or factor level). Of course we could match on feature of the marginal distributions (similar moments or entrophy).

### Idea

Let us assume that the above is not sufficient because the individual items are too numerous - or the above approach is not fun enough. There is more information that we can use if we have access to sample data from each project. We can describe an item 'a' in the data dictionary A by its relationship with other items in A. For example we can predict a_x based on other variables a_y in A (decision trees for regression). If the item information is sufficiently large this can be done multiple times by removing previously used a_y and repeating the estimation of a_x from A without the a_y used up already. Thus this process can create a number N of graph g_a (decision trees) that all predict one item a_x. Repeating the process with all a we will create a database of small graphs labelled by the items. These graphs can be enriched by adding node label from the marginal features of each item.

We can therefore create a database G_A of graphs g_a (decision trees) that are labelled by the item a_x. The same can be performed for G_B.

An algorithm that can do a classification on graph databases is DGCNN. We can use it to query if a g_b can be classified into a label a. The corresponding match will identify for an item from project B what item from project A most closely represent it.

The cool thing about this stratety of matching data dictionary items is that both the label type, the marginal distribution and the relationship of the item with other items in its project is used for the match. We are explicitly not need a match on the variable name. The method should in principle be able to discover matches of latent variables.

Here an example tutorial about DGCNN: https://medium.com/crim/deep-learning-applied-to-graphs-586ce63bb28e.