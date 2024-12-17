# Self-Driving-Car
Self-Driving Car using udacity's Car Sim
I used a Deep Neural Network to clone car driving behavior in this project. It is a supervised regression problem between the car steering angles and the road images, speed, etc of a car.
Those images were taken from three camera angles (from the center, the left, and the right from the car).

This Deep Learning model took inspiration from NVIDIA's [Paper](https://arxiv.org/pdf/1604.07316)
The Simulator used for this task is downloaded from Udacity's [Repo](https://github.com/udacity/self-driving-car-sim.git)


### Files included

- `model.ipynb` This file is used to create and train the model.
- `Autonomous.py` This is the script to drive the car.
- `model.h5` This is the trained model that is saved with all the weights and biases.

## Model Architecture Design

The design of the network is based on [the NVIDIA model](https://devblogs.nvidia.com/parallelforall/deep-learning-self-driving-cars/), which has been used by NVIDIA for the end-to-end self driving test.  As such, it is well suited for the project.  

It is a deep convolution network which works well with supervised image classification / regression problems.  As the NVIDIA model is well documented, I was able to focus how to adjust the training images to produce the best result with some adjustments to the model to avoid overfitting and adding non-linearity to improve the prediction.

I've added the following adjustments to the model. 

- I've added an additional dropout layer to avoid overfitting after the convolution layers.
- I've also included ELU for activation function for every layer except for the output layer to introduce non-linearity.

In the end, the model looks like as follows:

- Image normalization
- Convolution: 5x5, filter: 24, strides: 2x2, activation: ELU
- Convolution: 5x5, filter: 36, strides: 2x2, activation: ELU
- Convolution: 5x5, filter: 48, strides: 2x2, activation: ELU
- Convolution: 3x3, filter: 64, strides: 1x1, activation: ELU
- Convolution: 3x3, filter: 64, strides: 1x1, activation: ELU
- Drop out (0.5)
- Fully connected: neurons: 100, activation: ELU
- Fully connected: neurons:  50, activation: ELU
- Fully connected: neurons:  10, activation: ELU
- Fully connected: neurons:   1 (output)
