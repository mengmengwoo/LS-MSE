# Overview
The objective of this project is to explore the deep learning model’s ability to mimic the Rietkerk’s PDE model in generating the vegetation image dynamics. 
Therefore, the CNN-LSTM GAN model is constructed that extracts the key features of each consequtive timepoint input images and establishes the temporal relationship across input images. The evaluation of the generated images is conducted by the discriminator, a multi-layers CNN model. 

This capstone project proposes an innovative objective formula, the Least Squares Mean Squared Loss (LS-MSE) that modified from the traditional least squares loss. This proposed objective formula aims to directly compare the generated image data to the real data by adding the MSE term in the generator loss, calculating the average squared pixel differences between the generated and real images. In addition, the added MSE term may provide additional information for the CNN-LSTM model for the backpropagation stage. The results demonstrate that the CNN-LSTM trained under LS-MSE outperforms either the Wasserstein loss with gradient penalty (WGAN-GP) or the least
squares loss (LSGAN).

# Generator: CNN-LSTM
The generator ($G$) is a deep learning model composed of an encoder and a decoder.  The encoder processes input images from $t_{0}$ to $t_{6}$, using a 5-layer CNN and a 4-layer bidirectional LSTM. The encoder’s output is then fed into the 5-layer transpose CNN (the decoder), which aim to upsample the spatial features to the original image dimensions and to generate predicted images at $t_{7}$. 

<img width="951" alt="flowchart" src="https://github.com/user-attachments/assets/d855f8a1-7fbb-403b-84b8-c84428c0c7e3">

# Objective Function 
This project proposed a new loss function, the Least Squares and Mean Squared Generative Adversarial Networks (LS-MSE GAN). The LS-MSE loss modifies from the traditional least squares loss by introducing the means squared error term in the generator objective function, such that the pixel value differences between the generated and real images can be minimized. The LS-MSE loss
functions are as followed,

$\\text{Generator:}\min_{G} V_{LSMSE GAN}(G) =  \frac{1}{2}E_{z \sim p_{z(z)}} [(D(\tilde{x}) - b)^2]+\textcolor{red}{\frac{1}{2}MSE_{pixel}(x, \tilde{x})}\$

$\\text{Discriminator:}\min_{D} V_{LSMSE GAN}(D) = \frac{1}{2} E_{x \sim p_{data(x)}} [(D(x) - b)^2] + \frac{1}{2} E_{z \sim p_{z(z)}} [(D(\tilde{x}) - a)^2]\$

$\\text{ where } b = 1, a = 0, \tilde{x} = G(z)\$
