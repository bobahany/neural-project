# neural-project
neural networks-MNIST-Project

1. Problem Description
This project implements a Multilayer Perceptron (MLP) to classify handwritten digits (0-9) using the MNIST dataset. The goal is to build, train, and evaluate a neural network using PyTorch, while experimenting with different hyperparameters and applying regularization techniques to improve model performance and generalization.

2. Dataset Link
The MNIST dataset is used for this project. It is automatically downloaded via the torchvision library.

Official Source: http://yann.lecun.com/exdb/mnist/ (data set otomatcily download)
Dataset Characteristics: 60,000 training images and 10,000 testing images. Each image is a 28x28 grayscale pixel map.

3. Data Preprocessing
Handling Missing Values: The MNIST dataset is clean and contains no missing values.
Normalization/Scaling: Pixel values are scaled using transforms.Normalize((0.1307,), (0.3081,)) based on the global mean and standard deviation of the MNIST dataset to speed up convergence.
Encoding: Labels are already integer-encoded (0-9), which is directly compatible with PyTorch's CrossEntropyLoss (no One-Hot Encoding required).
Partitioning: The training data is split into 80% Training (48,000 images) and 20% Validation (12,000 images). The test set (10,000 images) is kept separate for final evaluation.

4. Model Architecture (MLP)
The model is a Multilayer Perceptron (MLP) built using PyTorch:

Input Layer: 784 neurons (28x28 flattened image).
Hidden Layer: Fully connected layer (size varies per experiment), followed by Batch Normalization, an Activation Function, and Dropout.
Output Layer: 10 neurons (representing digits 0-9).
Loss Function: nn.CrossEntropyLoss (standard for multi-class classification).

5. Regularization & Enhancement Techniques (Justified)
The following techniques were applied to improve model performance and prevent overfitting:

Data Augmentation (transforms.RandomRotation(10)): Randomly rotates the training images by up to 10 degrees. Justification: Handwritten digits can be slightly tilted; this forces the model to learn rotational invariance and generalize better to unseen handwriting styles.
Batch Normalization (nn.BatchNorm1d): Normalizes the activations of the hidden layer. Justification: Reduces internal covariate shift, allowing for higher learning rates, faster convergence, and more stable training.
Dropout (nn.Dropout(0.2)): Randomly zeros 20% of the neurons in the hidden layer during training. Justification: Prevents the network from relying too heavily on specific neurons, thereby reducing overfitting and improving generalization.

6. Experimentation & Results
Two experiments were conducted by varying the Activation Function, Number of Neurons, and Learning Rate to observe their impact on model performance.

Metric	Experiment 1 (ReLU)	Experiment 2 (Sigmoid)
Hidden Neurons	128	64
Learning Rate	0.001	0.01
Test Accuracy (%)	98.12%	97.67%
Final Test Loss	0.0593	0.0831
Mean Squared Error (MSE)	0.3971	0.4658
Analysis & Comparison
Experiment 1 (using ReLU) outperformed Experiment 2 (using Sigmoid).

ReLU is less computationally expensive and effectively solves the "vanishing gradient" problem, allowing the network to learn faster and achieve higher accuracy quickly.
Sigmoid squashes inputs into a small range [0, 1], which can cause gradients to vanish in deeper layers, resulting in slower convergence and slightly lower accuracy despite using a higher learning rate in Exp 2.

7. Visualizations
The training and validation curves for Loss and Accuracy are plotted to monitor the training process and check for overfitting. [https://colab.research.google.com/drive/1Pgbal7P54xZkkCO9AjA83YuFocxl9Yqp#scrollTo=kYTICYqnE338&fullscreenOutput=true](https://github.com/bobahany/neural-project/blob/main/README.md)

8. Instructions for Running the Project
Prerequisites: Ensure you have Python 3.x installed.
Clone the repository:
git clone <YOUR_REPO_LINK>cd <YOUR_REPO_NAME>
Install required libraries: It is recommended to use the provided requirements file.
pip install -r requirements.txt
Run the code:
Open the Project_Notebook.ipynb in Jupyter Notebook or Google Colab and run all cells sequentially. The dataset will download automatically.
