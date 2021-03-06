---
layout: post
title: Different types of probability sampling methods?
subtitle: Handy techniques in data science to create sample population
---

Basically sampling method refers to the way where observations are selected from the large population to create a sample for a sample survey or experiment. While solving some problems in a data science, we might be in dilemma regarding which data to pickup from the population to train your model. 
Therefore following methods can be handy to decide which sampling techniques to use based on your problem.

- Stratified sampling
- Cluster sampling
- Systematic sampling
- Convenience sampling
- Multistage sampling

### Stratified sampling
In stratified sampling, population is divided into multiple groups and individuals from each groups are selected randomly.
Eg. Assume you have data about population from 50 different states in USA and if you need to take a sample of population, then you can select 3(or more) people from each state.

### Cluster sampling
Population is divided into separate groups of units called clusters. Randomly select some of the groups or clusters and 
your sample population is everyone in those selected groups. Eg. Among 50 different states in USA, randomly select 3 states
and your sample is everyone in these 3 states.

### Systematic sampling
It is operated on ordered data. Using systematic sampling, you can select a starting point and select every k-th data. 
Eg. Assume you have list of contact information in a phone book, start with 5th person and select every 5-th person in 
the list for your sample data i.e your samples are 5-th, 10-th, 15-th, 20-th … person.

### Convenience sampling
It means using the data which is readily available to use. A convenience sample is made up of people who are easy to reach.
Eg. If you want to survey your neighbour, sampling information about your best friend might be a good sample for the
experiment. Consider a pollster interviews shoppers at a mall. The mall was chosen because it was a convenient 
site for pollster or because it was close to the pollster’s home or business, this would be a convenience sample.

### Multistage sampling
In multistage sampling, we can select samples by combining different types of sampling methods as mentioned above.

