# Notes

Switching sigmoid activation function in ML to ReLu function enable the gradient descent method faster since the gradient for sigmoid gradually shrink to 0 while ReLu has 0 gradient for left area and constant gradient for the right.

Loss function of $L = \frac{1}{2} (\hat{y} - y)$ is not good for gradient descent. It may find a local minimum since it is not convex. 

From [Karphathy's video](https://www.youtube.com/watch?v=VMj-3S1tku0),
it says there common bugs you may have:

1. you didn't try to overfit a single batch first.
2. you forgot to toggle train/eval mode for the net.
3. you forgot to .zero_grad() (in pytorch) before .backward().
4. you passed softmaxed outputs to a loss that expects raw logits
5. you didn't use bias = false for you linear/conv2d layer when using batchnorm, or conversely forget to include it for the output layer.
6. thinking view() and permute() are the same thing.
7. 
