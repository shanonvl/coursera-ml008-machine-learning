# Week 2

## Multiple Features

* x<sub>1</sub> ... x<sub>n</sub> are parameters.
* y is target
* n = number of features
* x<sup>(i)</sup> = input (features) of i<sup>th</sup> training example.
* x<sub>j</sub><sup>(i)</sup> = value of feature <i>j</i> in <i>i<sup>th</sup></i> training example.

```
[ 
  1416 
  291 
  321 
]
```

x<sup>(2)</sup> = 291


Old Hypothesis: h<sub>theta</sub>(x) = theta<sub>0</sub>*x<sub>0</sub> + theta<sub>1</sub>*x<sub>1</sub>

Multiple variable form adds a theta multiplier for each parameter:

h<sub>theta</sub>(x) = theta<sub>0</sub>*x<sub>0</sub> + theta<sub>1</sub>*x<sub>1</sub> + ... + theta<sub>n</sub>*x<sub>n</sub>

For convenience of notation, define x<sub>0</sub> = 1 ( x<sub>0</sub><sup>(i)</sup> = 1).

Think of parameters AND thetas as vectors/matrices.

theta<sub>0</sub>*x<sub>0</sub> + theta<sub>1</sub>*x<sub>1</sub> + ... + theta<sub>n</sub>*x<sub>n</sub>

is the same as theta<sup>T</sup> * x

Therefore this can be simplified to h<sub>theta</sub>(x) = theta<sup>T</sup>x.

## Feature Scaling

Normalize feature values to make gradient descent more efficient.  If values are vastly different, cost function will be skewed toward the largest value and gradient descent will require more iterations to find the minimum.

Goal is to get every feature into approximately a -1 <= x<sub>i</sub> <= 1 range.  If it's close e.g. -2 <= x<sub>2</sub> <= .5 is okay.

NO:  -100 <= x <= 100 
NO:  -0.0001 <= x <= 0.0001 

Rule of thumb:  Don't worry too much, but as long as they're close and have some variance.

### Mean normalization

Replace x<sub>i</sub> with ( x<sub>i</sub> - mu<sub>i</sub> ) / (max-min OR std deviation)

## Learning Rate (alpha)

* Debugging gradient descent 
* How to choose alpha

Purpose of gradient descent is to minimize cost function, J(theta).  To debug, is helpful to graph X: # iterations, Y: J(theta) and ensure that there is a downward slope as X increases.  Looking at this figure can also suggest # of iterations necessary to effectively converge.

The # of iterations is completely dependent on values e.g. could be 30, 30,000, 3,000,000.

Typically create an "automatic convergence test" which effectively creates a minimum delta of J(theta) which equates to convergence.

If J(theta) is increasing, use smaller alpha.  Typically too large of alpha will continually overshoot the minimum.

For sufficiently small alpha, J(theta) should **always** decrease per iteration. however too small alpha will require unnecessary iterations to converge.

Choosing alpha:

1. Try e.g. 0.001, 0.003, 0.01, 0.03, 0.1, 0.3, 1 (eacb ~3x as large as previous)

2. Plot (# iterations,J(theta))

## Features and Polynomial Regression

For a given housing problem, assume features (a) frontage and (b) depth.  Instead of using separately, create a new feature, area, which is frontage x depth.  

## Normal Equation

Method of solving for theta analytically vs. iterative algorithm ( like gradient descent ).  Some advantages / disadvantages... 

Intuition: 

J(theta) = a * theta^2 + b * theta + c 

theta = (X<sup>T</sup> * X)<sup>-1</sup> * X<sup>T</sup> * y

octave: pinv function -> matrix inverse

octave: theta = pinv(X' * X) * X' * y

When to use gradient descent vs. normal equation:

GD:
* Need to choose alpha
* Need many iterations
* Works well even when number of features (n) is large.

Normal Equation:
* No need to choose alpha
* Don't need to iterate
* Need to compute (X<sup>T</sup>*X)<sup>-1</sup>
	* O(n^3) time to compute.
* Slow if <i>n</i> is very large

What is small vs. large: n <= 10k range, probably normal equation, but larger prob gradient descent.

## Normal Equation Noninvertibility (Optional material)

Sometimes X<sup>T</sup> * X is non-invertible:

* Redundant / linearly dependent features 

e.g. x1 = size in feet^2, x2 = size in meters^2

In this case, x1 = 3.28^2 * x2. 

* Too many features, specifically if m <= n.

For the first case, remove redundancy.
For the second case, delete some features, or use regularization ( future lesson ).













