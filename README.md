#**Reinforced Smoothing Neural Network**
###Building Neural Network Architecture


*   One input | Two Hidden Layer | One Output

*   Non-Linear Activation FUnction : Tanh --> Since the ground truth sin(x) have both positive and negative values, for which the tanh is ideal, as its output range is (-1,1). Additionally, Tanh is infinitely differentiable. This is the requirement for the custom loss function, which relies on the second-order derivative (curvature) to enforce smoothness

* Forward function for prediction


### Loss Computation
1.   **Smooth_Loss**: This function calculates the second-order derivative of the network's output with respect to the input. By minimizing the mean squared curvature ($d^2y/dx^2$), it discourage high-frequency oscillations caused by noise.

$$Loss = \text{MSE} + \lambda \cdot \text{Smoothness}$$

2.   **custom_loss**: This is the primary objective function. It combines standard Mean Squared Error (MSE) with smoothness penalty, weighted by the hyperparameter $\lambda$ (lyambda), for reducing the overfitting and following the trend  with smooth regularization.
###Training Loop:

*   Created an object"model" for a class"Neural Network"
*   **Optimizer used** : Adam optimizer for convergence
* Loop iterates for N "epochs" times which includes forward pass for prediction and backward pass for computing and updating the optimized weights and biases


###PLOT:


*   **Plot** reveals that the Neural network with only MSE function overfits the noisy data with the loss of 1.79%. However, penalizing the curvature with the lambda = 0.02 (i.e, introducing the smooth loss), the neural network sucessfully predicted the approximate sinx curve without overfitting.

* Loss evaluation in above cell depicts, the loss increases with the inclusion of the smoothness function which gives insight of moving away from the actual noise data.

*   **Findings**: Denoising the input acceleration using Neural Network in the structure while preprecessing, it is necessary to penalize the curvature loss. If not, the neural network overfits the data and give unrealistic response of the structure while post processing in finite element analysis.

