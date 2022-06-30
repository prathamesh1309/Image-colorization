# Image-colorization

## Overview

The aim of this project is to create a model that can be used to colorize images by taking a black and white image as input and producing a colourized image as output.

## Strategy

Instead of using the RGB color space, the project uses the LAB color space. This is because the LAB color space is more suitable for colorization tasks. It consists of three channels: L, a, and b. The L channel is used to represent the lightness of the color, and the a and b channels are used to represent the color channels.

The L channel which is the grayscale representation of the image is passed to the model and it outputs the a and b channels which we concatenate to form the final output.

## Model Architecture

The model trained is based on [Image-to-Image Translation with Conditional Adversarial Networks](https://arxiv.org/abs/1611.07004) paper.

### Generator

The Generator proposed in this paper is the U-Net. The architecture of the U-Net is depicted below.

![](https://production-media.paperswithcode.com/methods/Screen_Shot_2020-07-07_at_9.08.00_PM_rpNArED.png)

First path is the contraction path which is used to capture the context in the image. The encoder is just a traditional stack of convolutional and max pooling layers. The second path is the symmetric expanding path which is used to enable precise localization using transposed convolutions.

### Discriminator

The Discriminator proposed in this paper is the PatchGAN discriminator.
The PatchGAN discriminator tries to classify if each patch in an image is real or fake. This discriminator is run convolutionally across the image, averaging all responses to provide the ultimate output.

## Results

Upon training the above model for about 50 epochs, quite intersting results were obtained. The model was able to colorize common objects like sky and trees quite well, it faltered slightly on rare objects and produced circular patches of different colors on these objects. After plotting the losses it was seen that the Discrinator loss remained low whereas the Generator loss decreased over time.

## New model

To improve the results obtained, a new model was trained. A pretrained U-Net with ResNet backbone was imported and then it was trained on colorization task using L1 loss. Then it was trained adversarialy for 20 epochs.

## Final results

The new model performed much better than the initial model. It was able to colorize the images with more realistic colors. The initial model produced more grayish images as compared to the final model.

## Future work

Different model architectures could be tested to see if they gave better results. Also, the model could be trained for longer periods of time to decrease the error.
