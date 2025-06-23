# Intro
## Machine Learning
- Subset of Artificial Intelligence
- Computer can 'learn' from data

## Deep Learning
- Subset of machine learning
- Multilayered neural networks

## Neural Network
- Inspired by the human brain
- Consists of network of artificial **neurons** which are connected by **edges**, forming a **neural network**
- Each neuron receives **signals**, which is just a number
- Neuron applies an **activation function** to put those signals which are modified by a set of **parameters** applied to each input (parameters change during learning)
- Output of the activation function will usually be the input to another neuron, forming **layers**
- Depending on how many neurons in a layer and what their activation functions are, layers can perform different functions

![](Pasted%20image%2020250521132612.png)

### For Machine Learning
- Different hidden layers can be used to find **features** in the inputs (Basically mimicking the human process of abstraction)
- Human can look at something on a screen and not see pixels but instead see 'A cat' or 'eyes and a mouth'
- Performing this abstraction and feature discovery is difficult for computers, although some algorithms exist
- Advantage of neural networks is instead of programming specific features, they can instead be **trained**
- Even though the model can train parameters on it's own, human engineers are still needed to decide the layout of the neural network
- Many different ways to structure a neural network to make it useful for different purposes
- **Credit assignment path** (CAP) - chain of transformations from input to input
- CAP of two layers is enough to approximate any math function but deep learning networks can go a lot deeper

## Types of Machine Learning
### Supervised Learning
- Model exposed to a bunch of correct data, it learns the connections between elements

#### Regression
- Predicts numerical value

#### Classification
- Predicts likelihood that something belongs to a category (Ex. Is this a picture of a cat or a dog?)

#### Data
- Often the hardest thing to require
- Dataset will contain **examples** and **labels**
- Ex. If you have a bunch of pictures, and label which ones are cats and which ones are dogs
- The bigger and more diverse the dataset the better result

#### Model
- Choose the structure of your neural network
- Some structures are already well known to be good a certain tasks
- Often you'll have to fine-tune the structure to get the results you want

#### Training
- Once you have your data, you have to **train** it
- Typically you start off with some random parameters to make predictions on examples, and then compare the predictions to the labels
- Based on the difference between the result and the label, you compute the **loss** and use that to figure out what direction the weights need to go in
- Choosing how you compute loss is important to decide
- Typically done in **epochs**

#### Evaluation
- Similar to training
- Give it examples, ask it to make predictions
- Model uses correct answers to update it's weights
- **human being** uses the correct answers to evaluate the model and determine if more training is needed

#### Inference
- Making predictions/classifications
- Difference from evaluation is that here we don't know the correct answer and are using the model to get them

### Unsupervised Learning
- Doesn't provide the model any correct answers, model has to identify meaningful patterns in the data

### Reinforcement Learning
- Models trained on getting rewards or penalties for actions performed, tries to get the most rewards

### Generative
- Creates content from user input

## Linear Regression
- Given a set of data, find the equation of best fit for that line of the data
- Finding a relationship between one or more independent variables and a dependent variable
- Since you have a bunch of data that consists of inputs (independent variables) and outputs (dependent variables) problem is easy to approach with a **supervised** model
- Don't need machine learning for this but it's a good problem for our first neural network

### Temperature Conversion
- Take a formula we already know - $F = C * \frac {9} {5} + 32$
- Assume we have a list of values - Celsius Temperatures and the Fahrenheit values
- Should **normalize** the data by making every values from 0 - 1

#### Layers
- Model will have two layers
- Input layer for Celsius
- Output layer for Fahrenheit
- Forward function and it's parameters transform the signal from the input to the output
- In our case, the parameters will be **weight** and **bias**

#### Minibatch Stochastic Gradient Descent
- Picking some weights, trying them out, computing the loss and moving towards better weights is **Gradient Descent** (Trying to minimize the loss)
- There are other variations (Ex. do we adjust the weight after every item or after we've done all the data?)
- The method we will use is **stochasticly** is random

##### Calculating the Gradient
- Need to determine where the loss is going and how fast in order to adjust the weights
- Once we know the loss rate over time we have the slope of a line
- Gets more complicated if you have more than one independent variable

##### Backpropagation
- Used for calculating gradients
- When we go *forward* through the neural network we are calculating the loss function
- When we go *backwards* we get the gradients of the loss function
- Backpropagation is the process of gathering the gradients for all parameters by summing the contributions to the current batch
- We can use the gradients to update our parameters

##### Calculating Gradient with PyTorch
- First object we will use is a **Tensor** - a multi-dimensional matrix that's got specific functions to transform it in specific ways
- Tensors are optimized for ML and using them on GPUs
- Makes it easy to calculate the gradient with the **`backward`** function
