# Graph matching for data dictionary harmonization

Provide a method to match entries in a data dictionary based on data features.

## Task

Given are two data dictionaries A, and B, and example data for both with non-overlapping participants. We are looking for a ranking of items in B given any choice of item in A. Such ranking should rank item by similarity or compatiblity.

For example let data dictionary A be the data dictionary from the HCP project and data dictionary B be the data dictionary from the ABCD study. Create an item to item mapping for each HCP item to an item in ABCD.

We do not want to rely on participant data that are in both projects. We don't want rely on item names. The method should work with pseudonymized and anonymized data.

### Trivial

Of course we can match by data type (continuous or factor level). Of course we could match on feature of the marginal distributions (similar moments or entrophy).

### Idea

Let us assume that the above is not sufficient because the individual items are too numerous, or the coding of variables is different such as in age specified in month or age specified in years. There is more information that we can use if we have access to sample data from each project. We can describe an item 'a' in the data dictionary A by its relationship with other items in A. For example we can predict a<sub>x</sub> based on other variables a<sub>y</sub> in A (decision trees for regression). If the item information is sufficiently large this can be done multiple times by removing previously used a<sub>y</sub> and repeating the estimation of a<sub>x</sub> from A without the a<sub>y</sub> used up already. Thus this process can create a number N of graph g<sub>a</sub> (decision trees) that all predict one item a<sub>x</sub>. Repeating the process with all a we will create a database of small graphs labelled by the items. These graphs can be enriched by adding node label from the marginal features of each item.

We can therefore create a database G<sub>A</sub> of graphs g<sub>a</sub> (decision trees) that are labelled by the item a<sub>x</sub>. The same can be performed for G<sub>B</sub>.

An algorithm that can do a classification on graph databases is DGCNN. We can use it to query if a g<sub>b</sub> can be classified into a label a. The corresponding match will identify for an item from project B what item from project A most closely represent it.

The cool thing about this stratety of matching data dictionary items is that both the label type, the marginal distribution and the relationship of the item with other items in its project is used for the match. We are explicitly not need a match on the variable name. The method should in principle be able to discover matches of latent variables.

Here an example tutorial about DGCNN: https://medium.com/crim/deep-learning-applied-to-graphs-586ce63bb28e.

### References
 - canonical correlation analysis
 - distance correlation
 - Open Refine
 - reproschema