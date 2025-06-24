[Back to overveiw](Readme.md)

# Machine Learning

## Learning
Learning is about improving an agent’s performance on future tasks after making observations about the world.

Reasons for learning:
- The designer can't come up with all possible situations.
- The designer can't handle all changes over time.
- The designer may have no idea about the solution.

## Types of Learning

### Supervised Learning
- Agent observes input-output pairs.
- Learns a function that maps inputs to outputs.

### Unsupervised Learning
- Agent learns patterns in the input even without explicit feedback.

### Reinforcement Learning
- Agent learns from a series of reinforcements (rewards or punishments).
- Trial-and-error learning (like how children learn).

## Hypothesis Space
- A set of possible functions (e.g., linear functions).
- Each function is a candidate solution.

## Hypothesis
- A function selected from the hypothesis space.

## Ockham’s Razor Principle
- When multiple hypotheses are consistent with the data, prefer the simplest one.

## Types of Tasks

### Classification
- Output values are from a finite set (e.g., {sunny, cloudy, rainy}).

### Regression
- Output values are continuous/numeric (e.g., temperature).

## Decision Trees
A simple and successful form of learned function:
- Input: vector of attribute values
- Output: decision (True/False)

Tree structure:
- Root and internal nodes: attributes
- Leaves: output decision

### Learning Process
- Divide-and-conquer strategy.
- Select the most informative attribute (based on information gain).
- Generate branches for each value.

### Entropy
- Measures uncertainty of a random variable (in bits).
- Used to quantify information gained from a split.

### Information Gain
- Expected reduction in entropy from an attribute test.
- Select attribute with highest information gain for splitting.

## Learning Logical Models

### False Negatives
- Hypothesis says “no”, but the true answer is “yes”.

### False Positives
- Hypothesis says “yes”, but the true answer is “no”.

### Current-Best-Hypothesis
- Maintain a single hypothesis that best fits the data.
- Modified iteratively based on new data.

### Version-Space Learning
- Maintain a set of all hypotheses consistent with the data.
- Represented by:
  - S-set: most specific consistent hypotheses
  - G-set: most general consistent hypotheses

## Linear Regression
- Learns a linear function to approximate real-valued outputs.
- Uses gradient descent to minimize the error.

## Linear Classification
- Divides data into two classes using a linear decision boundary.

### Linearly Separable Examples
- Classes can be perfectly separated by a line (or hyperplane).

- XOR example: Not linearly separable.

## Artificial Neural Networks
- Composed of layers of nodes (neurons).
- Uses backpropagation to update weights based on error.

### Backpropagation
- Computes gradient of the loss function.
- Updates weights using gradient descent.

## Parametric Models
- Fixed number of parameters.
- Model complexity doesn't grow with data size (e.g., linear regression).

## Non-Parametric Models
- Number of parameters can grow with data size.
- More flexible (e.g., k-nearest neighbors).

## k-Nearest Neighbors (k-NN)
- Instance-based learning.
- Predicts output based on the majority label of k closest examples.

## Support Vector Machines (SVM)
- Combines non-parametric methods with linear classification.
- Finds the maximum-margin separator.
- Uses kernel trick to map input into higher dimensions when data is not linearly separable.

[Back to overveiw](Readme.md)

