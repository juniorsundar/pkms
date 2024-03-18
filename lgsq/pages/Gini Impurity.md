# Definition
	- It is a metric used primarily in decision tree algorithm (like CART) to determine how well a specific feature can split data within a node into more homogeneous groups.
	- In context of classification, it measures:
		- **Heterogeneity** - Probability of incorrectly classifying a randomly selected data point if it were labeled randomly according to the distribution of classes in that dataset or node.
		- **"Pure" nodes** - The value is '0' when a node contains only instances of one class (completely homogeneous).
		- **"Impure" nodes** - It reaches maximum value of 0.5 when classes are evenly distributed within a node.
	- ## Formula
		- $G = \sum_{i=1}^{C} p(i)*(1-p(i))$
		- Where:
			- $C$ is the number of classes.
			- $p(i)$ is the probability or relative frequency of a data point belonging to a class $i$.
- # Use in Decision Trees
	- *Calculating Initial Impurity* - At the beginning, Gini impurity of the root node of the tree is calculated based on the initial distribution of classes in your dataset.
	  logseq.order-list-type:: number
	- *Evaluating Splits* - For each potential split (based on a feature), the Gini impurities of a resulting child node is calculated.
	  logseq.order-list-type:: number
	- *Selecting Best Split* - Feature that leads to the greatest reduction in the weighted average Gini impurity across the child nodes is chosen as the split for that node.
	  logseq.order-list-type:: number
	- *Iterative Process* - Process repeats recursively, creating progressively smaller and more homogeneous nodes until certain stopping criteria are met (e.g. maximum tree depth, minimum impurity reduction).
	  logseq.order-list-type:: number
- # Why Gini Impurity is Favoured
	- *Less computationally expensive* - Compared to other impurity measures like
	  entropy, Gini impurity is generally less intensive for calculations.
	- *Handles imbalanced classes* - Is somewhat robust to imbalanced class
	  distributions.
	- *Intuitive interpretation* - Many find probabilistic interpretation of Gini
	  impurity easier to grasp.
- # TL;DR
  
  Gini impurity measures how mixed-up the different classes are within a group
  of data points. If all data points belong to the same class (perfect order)
  then the Gini impurity is 0. If classes are perfectly evenly distributed
  (maximum disorder), Gini impurity is 0.5.
  
  Decision trees love low impurity. When building a decision tree, the goal is
  to find splits that generate groups with lower Gini impurity, meaning those
  groups are closer to having just one class.
  
  * Example: Predicting Ball Colour
  
  Imagine that there are 6 blue and 4 red balls in a bag.
  
  ** Overall Impurity:
  
   Probability of picking blue ball: 6/10 = 0.6
   Probability of picking red ball: 4/10 = 0.4
   Gini impurity from {** Formula}[formula]: 1 - (0.6)^2 - (0.4)^2 = 0.48
  
  ** Testing a Split
  
  Let's split the balls based on whether they are heavier or lighter than a
  certain weight.
	- Group 1: 5 blue balls, 1 red ball
	- Group 2: 1 blue ball, 3 red balls
	  
	  ** Impurity After Split
	  
	  *In Group 1*:
	  Probability of picking blue ball: 5/6
	  Probability of picking red ball: 1/6
	  Gini impurity: 1 - (5/6)^2 - (1/6)^2 = 0.278
	  
	  *In Group 2*:
	  Probability of picking blue ball: 1/4
	  Probability of picking red ball: 3/4
	  Gini impurity: 1 - (1/4)^2 - (3/4)^2 = 0.438
	  
	  *Weighted Average Impurity*:
	  Weight of Group 1: 6/10 (6 out of 10 balls)
	  Weight of Group 2: 4/10
	  Weighted Average Impurity:
	  (Weight of Group 1 * Impurity of Group 1) + (Weight if Group 2 * Impurity of Group 2)
	  = (6/10 * 0.278) + (4/10 * 0.438)
	  = ~0.342
	  
	  ** Analysis
	  
	  Weighted impurity after split is lower than the original impurity of the
	  bag. This indicates that out split based on weight did a decent job of
	  separating the balls, making the groups more "pure" in terms of their colour
	  distribution.
	  
	  The decision tree algorithm would repeat this process for different features
	  and potential splits, comparing the weighted average impurities. The split
	  leading to the greatest reduction in impurity would be selected at each
	  node.