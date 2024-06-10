# VAEs Face Producer

In this project, I build and train a Variational Autoencoder (VAE) model to produce new human faces using the CelebA database. These models yield state-of-the-art machine learning results in image generation and reinforcement learning. Variational autoencoders (VAEs) were defined in 2013 by Kingma and Welling.

## Overview

This project demonstrates how well we can reconstruct images from the latent space (lower-dimensional representations).

### Concept

The idea behind VAEs is illustrated below:
![VAE Concept](https://github.com/omer1C/VAEs-face-producer-5.24/assets/135855862/019faad4-4df6-44bd-bba5-f37d378bee27)

### Encoder

The encoder's role is to compress the input data into a lower-dimensional representation. It consists of several convolutional layers that progressively reduce the spatial dimensions of the input while increasing the depth (number of channels). The final output of the encoder is a set of latent variables that represent the mean (μ) and the log variance (log(σ²)) of the latent space distribution.

### Latent Space

The latent space is a compressed representation of the data. With VAEs, we use the reparameterization trick to allow backpropagation through the stochastic sampling process. The encoder provides the mean and log variance, which allows us to reconstruct the original image effectively.

### Decoder

The decoder's role is to reconstruct the input data from the sampled latent variables. It consists of several transposed convolutional layers (also known as deconvolutional layers) that progressively increase the spatial dimensions of the data while reducing the depth. The final output of the decoder is an image that attempts to match the original input image.

If we manage to train the decoder to decode the vector from the latent space to restore the original image, we can generate a Gaussian random vector, and decode it to create a new face!

## Loss Function

Given a dataset X, the goal is to model the underlying data distribution P(X) and maximize the marginal likelihood of the data, log(P(X)), meaning:

![Loss Function](https://github.com/omer1C/VAEs-face-producer-5.24/assets/135855862/4a34b238-9592-491c-b1c9-c6092570a98d)

### Reconstruction Loss

Measures how well the decoder's output matches the original input. Typically, this is the binary cross-entropy loss between the input and the reconstructed output.

### KL Divergence

Measures how much the learned latent space distribution deviates from the prior distribution (usually a standard normal distribution). This regularizes the latent space to be close to the prior distribution.

## Results: 
I tried to first train the model with the following parameters : 

#### IMAGE_SIZE = 64
#### learning_rate = 5e-3
#### batch_size = 128
#### num_epochs = 60
#### dataset_size = 30000
#### latent1 = 256

With achieved :

## Tracking Loss values : 
![image](https://github.com/omer1C/VAEs-face-producer-5.24/assets/135855862/efd18c29-7525-49c0-8363-91b04acf0227)


Comparing the original images and the reconstructed images : 

## Original Images : 
![image](https://github.com/omer1C/VAEs-face-producer-5.24/assets/135855862/060445e2-28a5-41fe-842c-c35e59cfafcd)


## Reconstructed Images : 
![image](https://github.com/omer1C/VAEs-face-producer-5.24/assets/135855862/76c3d23a-82c1-4973-af73-5a572d9df4c6)

## Creating New Faces : 
As explained in the first part, the original image is encoded into the latent space, where it is represented by a single vector (with smaller dimensions than the dimensions of the original image) and then the decoder decodes the original image based on that vector.
In order to create a new face, we generate some random vector in the latent space and send it to the decoder, thus we will get new fictitious faces.

## Results : 

### The firs attempt to create new faces, after one epoch : 

![image](https://github.com/omer1C/VAEs-face-producer-5.24/assets/135855862/197363c6-8dae-467d-8ecc-2a0b960ea296)








