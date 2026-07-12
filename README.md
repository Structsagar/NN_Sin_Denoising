# Reinforced Smoothing Neural Network for Sinusoidal Signal Denoising

This repository demonstrates a neural network approach for denoising noisy sinusoidal signals using a **smoothness-regularized loss function**. Instead of minimizing only the Mean Squared Error (MSE), the model incorporates a curvature penalty based on the second-order derivative of the predicted signal, resulting in smoother and more physically meaningful predictions.

---

## Neural Network Architecture

The network consists of:

- **Input Layer:** 1 neuron
- **Hidden Layers:** 2 fully connected layers
- **Output Layer:** 1 neuron

### Activation Function

The hidden layers use the **Tanh** activation function because:

- The target signal, **sin(x)**, contains both positive and negative values.
- Tanh naturally outputs values in the range **(-1, 1)**.
- Tanh is infinitely differentiable, making it suitable for computing higher-order derivatives required in the custom smoothness loss.

---

## Custom Loss Function

The total loss is defined as

\[
L = \text{MSE} + \lambda \times \text{Smoothness}
\]

where

- **MSE** minimizes the prediction error.
- **Smoothness** penalizes the second derivative of the predicted signal

\[
\text{Smoothness} = \left(\frac{d^2y}{dx^2}\right)^2
\]

The smoothness term discourages high-frequency oscillations and prevents the neural network from fitting the noise.

---

## Training

The model is trained using:

- Optimizer: **Adam**
- Forward propagation for prediction
- Backpropagation for weight updates
- User-defined number of epochs

---

## Results

Two models are compared:

1. Neural Network trained using only MSE loss.
2. Neural Network trained using MSE + Smoothness Loss.

### Observation

- Using only MSE causes the network to overfit the noisy observations.
- Adding the smoothness penalty (λ = 0.02) successfully reconstructs the underlying sinusoidal signal while suppressing noise.

Although the total loss becomes larger after adding the regularization term, the predicted signal is smoother and follows the true trend more accurately.

---

## Motivation

In structural engineering applications, measured acceleration records often contain high-frequency noise.

Training a neural network using only MSE may reproduce this noise, which can lead to unrealistic structural responses during finite element analysis.

By penalizing the curvature of the predicted signal, the network produces physically meaningful denoised acceleration histories suitable for structural dynamic analysis.

---

## Future Work

- Extension to earthquake acceleration denoising
- Application to structural health monitoring
- Integration with finite element simulations
- Comparison with wavelet-based denoising techniques
