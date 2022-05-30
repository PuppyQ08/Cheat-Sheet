# Notes

Switching sigmoid activation function in ML to ReLu function enable the gradient descent method faster since the gradient for sigmoid gradually shrink to 0 while ReLu has 0 gradient for left area and constant gradient for the right.

Loss function of $L = \frac{1}{2} (\hat{y} - y)$ is not good for gradient descent. It may find a local minimum since it is not convex. 
