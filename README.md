# Adversarial Attack

Executing non-targeted attacks using the [Fast Gradient Sign Method (FGSM)](https://arxiv.org/abs/1412.6572) and [Iterative Fast Gradient Sign Method (I-FGSM)](https://arxiv.org/abs/1607.02533) attack algorithms on proxy networks resulted in the attacked model achieving an accuracy of **0.00%**.

## Attack Algorithm
### FGSM
FGSM stands out for its simplicity and efficiency, showcasing the susceptibility of machine learning models to subtle, meticulously crafted perturbations in input data. This underscores the importance of enhancing the robustness and security of machine learning systems, motivating researchers to develop more resilient models and defenses against adversarial attacks like FGSM.

1. Given an input sample $x$ and a trained machine learning model $f$, FGSM computes the gradient of the model's loss function $J(f(x), y)$ with respect to the input $x$, where $y$ represents the true label of $x$.
   
2. Rather than adjusting the model's parameters, FGSM directly alters the input data $x$ in the direction of the gradient of the loss function with respect to $x$, while restricting the perturbation to a small step (scaled by a small epsilon value) to prevent excessive distortion.

3. The perturbed input, denoted as $x'$, is calculated using the formula:

$$x' = x + \epsilon \cdot \text{sign}(\nabla_x J(f(x), y))$$

Here, $\epsilon$ denotes a small constant indicating the magnitude of the perturbation, and $\text{sign}(\cdot)$ returns the sign of its argument.

4. Finally, the adversarial example $x'$ is fed into the model, which is likely to misclassify it due to the minor perturbation aimed at maximizing the loss.

### I-FGSM
1. Initialize $x'$ with the original benign image $x$.
2. Construct a loop corresponding to the number of iterations for iterative processing.
3. In each iteration, apply FGSM with $\epsilon = \alpha$ to obtain a new $x'$, then constrain the new $x'$ within the range $[x-\epsilon, x+\epsilon]$, where $\alpha$ represents the step size.

## Attack Technique
1. Simultaneously target multiple proxy models.
2. Aggregate the variance and bias of models ([Delving into Transferable Adversarial Examples and Black-box Attacks](https://arxiv.org/abs/1611.02770)).
3. Employ Ensemble Attack ([Query-Free Adversarial Transfer via Undertrained Surrogates](https://arxiv.org/abs/2007.00806)).

## Dataset
The [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) dataset serves as the primary data source for this project, accessible [here](https://drive.google.com/file/d/19E0B_Cj2gCWSHiqI6wkFaHYXXXGVA0WR/view?usp=sharing).

For detailed implementation and usage instructions, please refer to the provided [code](https://github.com/Dawson-ma/Adversarial-Attack/blob/main/Adversarial_Attack.ipynb).
