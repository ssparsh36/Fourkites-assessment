# Loss Landscape Geometry and Optimization Dynamics  
An empirical study using two neural network architectures

This repository presents an experimental investigation into the relationship between neural network architecture, loss landscape geometry, optimization behavior and generalization performance. The work examines how simple architectural changes influence both the training dynamics and the shape of the regions in which models converge. The focus is on practical and intuitive analysis rather than formal mathematical treatment.

## Overview

The study is built around four central questions:

1. Why does stochastic gradient descent reach solutions that generalize well despite the non convex nature of neural network loss surfaces  
2. How does architecture influence the geometry of the loss landscape  
3. Which geometric properties appear to correlate with ease of training and generalization quality  
4. Can we identify signs of optimization difficulty through simple landscape observations  

To explore these questions, two models are trained on the Fashion MNIST dataset under identical training conditions.

Model A is a basic multilayer perceptron with no normalization or regularization.  
Model B is a small convolutional network with batch normalization and dropout.

Their behavior is compared using a series of lightweight diagnostic tools.

## Methods

Four empirical probes are used throughout the study. Each of these is inexpensive to compute and does not require higher order derivatives or complex analysis.

1. Learning curves. Training and validation loss and accuracy are recorded over the course of optimization in order to observe convergence speed and stability.  

2. Generalization gap. The difference between training accuracy and validation accuracy is monitored. Larger gaps suggest overfitting or sensitivity to training data, while small or near zero gaps indicate more robust solutions.  

3. Robustness to parameter noise. Small random perturbations are added to the final model weights and accuracy is remeasured. A solution that remains stable under perturbation is considered to lie in a flatter region of the loss surface.  

4. One dimensional loss slice. The loss is evaluated along a random direction passing through the final parameter vector to observe whether the loss rises sharply or gradually. This provides a simple view of local landscape sharpness or flatness.

These diagnostics allow for a qualitative understanding of the geometry surrounding the minima that each model reaches.

## Results

Model B consistently trains faster and reaches higher validation accuracy than Model A. The improvement is visible from early epochs onward and continues through the end of training.  

Final validation accuracy for Model A is 87.69 percent.  
Final validation accuracy for Model B is 91.32 percent.  

The generalization gap for Model A remains small but positive at 0.0144, which indicates mild overfitting. Model B finishes with a slightly negative generalization gap of approximately minus 0.0016, meaning that performance on unseen data slightly exceeds performance on the training set.

In the robustness experiment, Model B maintains accuracy above 90 percent even when moderate noise is applied to its parameters. Model A remains stable but performs distinctly worse across all noise scales. This suggests that Model B converges to a flatter and more forgiving region of the loss surface.

The one dimensional loss slice reinforces this observation. The loss around Model A increases more steeply as parameters are moved away from the solution, whereas the curve around Model B rises more gently. This indicates that Model B resides in a broader and more stable local basin.

## Interpretation

These results support the idea that SGD tends to gravitate toward wider and more stable minima, especially when the architecture encourages smoother optimization. The architectural elements in Model B create conditions that guide the optimizer into flatter regions of the loss landscape. These regions are associated with faster convergence, greater robustness to perturbation and stronger generalization.

Model A, in contrast, reaches a sharper and more sensitive minimum, which aligns with its slower training speed and lower validation accuracy.

The study also shows that simple indicators such as early learning curve behavior, generalization gap trends and sensitivity to parameter noise can serve as practical signals of how difficult optimization will be. These tools offer a straightforward way to reason about optimization and generalization without relying on complex theoretical machinery.

## Contents

This repository contains the full code used to train both models and generate all analysis plots, along with the written report that documents the study and its findings.

## Citation

If this work is referenced in academic or project contexts, please cite the accompanying report.
