---
author: Ayman DAMOUN
title: Machine learning basics
date: 2021-03-08
description: My notes I took while taking Machine Learning taught by Andrew Ng on Coursera.
math: true
---
In the following post I will present my notes of the course  Machine Learning by Andrew Ng.
The course can be found at coursera [Link](https://www.coursera.org/learn/machine-learning). In addition the material and my assignment solutions are on my github repository [Link](https://www.coursera.org/learn/machine-learning).
{{< math.inline >}}
{{ if or .Page.Params.math .Site.Params.math }}
<!-- KaTeX -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.css" integrity="sha384-zB1R0rpPzHqg7Kpt0Aljp8JPLqbXI3bhnPWROx27a9N0Ll6ZP/+DiW/UqRcLbRjq" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.js" integrity="sha384-y23I5Q6l+B6vatafAwxRu/0oK/79VlbSz7Q9aiSZUvyWYIYsd+qj+o24G5ZU2zJz" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
{{ end }}
{{</ math.inline >}}

# Vocabulary

- **Machine Learning**: Field of study that gives computers the ability to learn
     without being explicitly programmed.
- **Supervised Learning**: In supervised learning, we are given a data set and already know what our correct output should look like, having the idea that there is a relationship between the input and the output. Supervised learning problems are categorized into "regression" and "classification" problems. In a regression problem, we are trying to predict results within a continuous output, meaning that we are trying to map input variables to some continuous function. In a classification problem, we are instead trying to predict results in a discrete output.
- **Unsupervised Learning**: Unsupervised learning allows us to approach problems with little or no idea what our results should look like. We can derive structure from data where we don't necessarily know the effect of the variables. We can derive this structure by clustering the data based on relationships among the variables in the data.

# Linear regression

- n: number of features
- m: number of training set
- {{< math.inline >}}\(\alpha\):{{</ math.inline >}} Learning Rate

![your_img](https://i.ibb.co/d23xpZM/Linear-regression.png#center)

- **Hypothesis**: {{< math.inline >}}\(h_\theta(x)=\theta^Tx\) with \(x_0=1\){{</ math.inline >}}.
- **Parameters**: {{< math.inline >}}\(\theta_0,\theta_1,...,\theta_n\){{</ math.inline >}}.
- **Cost function**:
$$
J(\theta)=\frac{1}{2m}\sum_{i=1}^{m} (h_\theta(x^{(i)})-y^{(i)})^2
$$
- **Gradient descent**: Repeat
$$
\theta_j:=\theta_j-\alpha \frac{\partial}{\partial \theta_j} J(\theta)
$$
 simultaneously update for every j=\{0,...,n\}
- **Feature Scaling**: for fast convergence, Get every feature into approximately a {{< math.inline >}}\(-1\leq x_i\leq 1\){{</ math.inline >}} range

# Normal Equation
$$
\theta=(X^TX)^{-1}X^Ty
$$
There is no need to do feature scaling with the normal equation.
### Comparaison between Normal Equation and Gradient descent
| Gradient Descent           | Normal Equation         |
|----------------------------|-------------------------|
| Need to choose α           | No need to choose α     |
| Needs many iterations      | No need to iterate      |
| {{< math.inline >}}\(O(kn^2)\){{</ math.inline >}}   | {{< math.inline >}}\(O(n^3) for X^TX\){{</ math.inline >}}     |
| Works well when n is large | Slow if n is very large |

# Classification
- Sigmoid function:
$$h_\theta(x)=p(y=1/x;\theta)=\frac{1}{1+\exp{-\theta^Tx}}$$
- Decision Boundar:
$$h_\theta(x)\ge 0.5\Rightarrow y=1\quad h_\theta(x)<0.5\Rightarrow y=0$$
- Logistic regression cost fonction:
$$J(\theta)=\frac{1}{m}\sum_{i=1}^{m}\mathrm{Cost}(h_\theta(x^{(i)}),y^{(i)})$$

$$
\mathrm{Cost}(h_\theta(x),y) = -\log(h_\theta(x)) \quad \quad \text{if y = 1} \newline
\mathrm{Cost}(h_\theta(x),y) = -\log(1-h_\theta(x)) \quad \text{if y = 0}
$$

$$
\mathrm{Cost}(h_\theta(x),y) = 0 \quad \text{ if } h_\theta(x) = y \newline
\mathrm{Cost}(h_\theta(x),y) \rightarrow \infty \quad \text{ if } y = 0\; \mathrm{and} \; h_\theta(x) \rightarrow 1\newline
\mathrm{Cost}(h_\theta(x),y) \rightarrow \infty \quad \text{ if } y = 1 \; \mathrm{and} \; h_\theta(x) \rightarrow 0
$$

$$J(\theta)=\frac{1}{m}\left[\sum_{i=1}^{m}y_{i}\log h_\theta(x_{i})+(1-y_{i})\log(1-h_\theta(x_i))\right]$$

### Gradient Descent
Repeat
$$
\theta_j:=\theta_j-\alpha \sum_{i=1}^{m}(h_\theta(x^{(i)})-y^{(i)})x^{(i)}_j
$$
 simultaneously update for every j=\{0,...,n\}
- Advanced Optimization Matlab

**Function**
```matlab
function [jVal, gradient] = costFunction(theta)
  jVal = [...code to compute J(theta)...];
  gradient = [...code to compute derivative of J(theta)...];
end
```
**Fminunc**
```matlab
options = optimset('GradObj', 'on', 'MaxIter', 100);
initialTheta = zeros(2,1);
   [optTheta, functionVal, exitFlag] = fminunc(@costFunction, initialTheta, options);
```
### Multiclass Classification

**One-vs-all**
 Train a logistic regression classifier {{< math.inline >}}\(h_\theta(x)\){{</ math.inline >}}  for each class i to predict the probability that {{< math.inline >}}\(y = i\){{</ math.inline >}} .
$$
h^i(\theta)=P(y=i/x;\theta)
$$
To make a prediction on a new x, pick the class i that maximizes {{< math.inline >}}\(h_\theta(x)\){{</ math.inline >}}.

# Overfitting

Underfit ==> high bias

Overfit ==> high variance

There are two main options to address the issue of overfitting:
- Reduce the number of features.
- Regularization: Keep all the features, but reduce the magnitude of parameters  {{< math.inline >}}\(h_\theta(x)\){{</ math.inline >}}.

- **Regularization Cost Function**
$$
J(\theta)=\frac{1}{2m}\sum_{i=1}^{m}(h_\theta(x^{(i)}-y^{(i)})^2+\lambda \sum_{j=1}^{n} \theta_j^2
$$
- **Gradient Descent**
$$
 \text{Repeat}\ \lbrace \newline \ \ \ \ \theta_0 := \theta_0 - \alpha\ \frac{1}{m}\ \sum_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)})x_0^{(i)} $$
$$\\ \ \ \ \ \theta_j := \theta_j - \alpha\ \left[ \left( \frac{1}{m}\ \sum_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)})x_j^{(i)} \right) + \frac{\lambda}{m}\theta_j \right] $$ $$\ \ \ \ \ \ \ \ \ \ j \in \lbrace 1,2...n\rbrace\newline  \rbrace 
$$

- **Normal Equation**
$$
\theta = \left( X^TX + \lambda \cdot L \right)^{-1} X^Ty
$$ 

$$
 \text{where} \;L = \begin{bmatrix} 0 & & & & \\\\ & & 1 & & \\\\ & & & \ddots & \\\\ & & & & 1 \newline\end{bmatrix}
$$

If m < n, then $X^TX$ is non-invertible. However, when we add the term  {{< math.inline >}}\(\lambda L\){{</ math.inline >}}, then {{< math.inline >}}\(X^TX+\lambda L\){{</ math.inline >}} becomes invertible.