# ml-object-classifier- Robotics Components

## What I built
A CNN image classifier that classifies 4 robotics objects:
-Screwdriver
-Robotic car wheel
-Arduino Uno board 
-Stepper Motor 

I chose these 4 objects because they are all part of my robotics workspace and have distinctly different shapes. Like, a wheel is circular, a screwdriver is long and thin, an Arduino board is flat and rectangular, and a stepper motor is compact and cylindrical and has a long wire attached to it. This visual variety makes them ideal for classification since the model has clear shape differences to learn from.

## What the model does:
- I fed the model a dataset of 112 images (that has around 30 images per object), out of which, 80% of the images (approximately 90 images) are used for training purposes, and 20% of the images (approximately 22 images) are used for testing.
- After training, the model takes an unseen test image. The CNN scans that image for patterns like edges and shapes and gives an output of the predicted label.
- The predicted label is then compared to the actual label to calculate the model's accuracy.

## Dataset
I collected the dataset myself using my phone camera, photographing 4 different objects from my desk. Images were taken from different angles, distances, orientation, lighting conditions (Cool light, Warm light and Natural lighting), different desk surfaces (white and black).

I created two versions of datasets:
- Dataset 1: 82 images (appx. 20 per class)
- Dataset 2: 112 images (appx. 30 per class), which I collected after identifying that Dataset 1 was too small.

## Model Architecture
My CNN has two convolutional layers that extract patterns from images, followed by one hidden layer with 128 neurons, and a final output layer with 4 neurons, one per class.
### Convolutional Layers:
The first conv layer used 16 filters that slide across the image looking for basic things like edges and textures. The second conv layer used 32 filters that build on what the first found and detect more complex patterns. After each conv layer, a MaxPool layer shrank the image by half to reduce the amount of data being processed.

### Fully connected layers
The output of the convolutional layers is flattened into a single list of numbers and passed into a hidden layer with 128 neurons. This layer combines all the patterns detected by the conv layers to make sense of the image. The final output layer has 4 neurons, one for each class. Whichever neuron has the highest value is the model's prediction.

# Experiments
All three experiments were run on both datasets to observe how dataset size affects results
### Experiment 1- Baseline
-I initially fed the model Dataset 1.
-After training using this dataset, the training accuracy reached 100% by epoch 7 while test accuracy was just 88.24% on unseen data images, indicating the model had memorized the training data rather than learning generalizable patterns. This is called overfitting and is common with small datasets.

- Next, I fed the model Dataset 2, which was larger
- After training using this dataset, the training accuracy reached 100% by epoch 7 again, with testing accuracy of 87.50%.

Training accuracy hit 100% in both cases, meaning the model memorized the training data. This is *overfitting*, the model learned the training images too well instead of learning general patterns.

### Experiment 2- Dropout (rate = 0.5)
Added a dropout layer that randomly switches off 50% of neurons during training.
| Dataset | Train Accuracy | Test Accuracy |
|---------|---------------|---------------|
| 1 (82 imgs) | 93.85% | 76.47% |
| 2 (112 imgs) | 98.96% | 83.33% |

Dropout hurt performance on both datasets because the dataset was still too small.

### Experiment 3- Augmentation
Applied random flips, rotations, and brightness changes to training images.
| Dataset | Train Accuracy | Test Accuracy |
|---------|---------------|---------------|
| 1 (82 imgs) | 95.38% | 64.71% |
| 2 (112 imgs) | 87.50% | 79.17% |

Augmentation made training unstable and reduced test accuracy, however the model with dataset 2 seemed to perform better than the smaller dataset





