# Dogs-vs-Cats
# Objective

- This project belongs to [kaggle's competitions](https://www.kaggle.com/c/dogs-vs-cats/overview) and I carried out as a part of a specialization called [DeepLearning.AI TensorFlow Developer Specialization](https://www.coursera.org/account/accomplishments/specialization/certificate/L6R6AFWVXHZT) which is given by DeepLearning.AI. This specialization is conformed by 4 courses: 
1. Introduction to TensorFlow for Artificial Intelligence, Machine Learning, and Deep Learning 
2. Convolutional Neural Networks in TensorFlow 
3. Natural Language Processing in TensorFlow 
4. Sequences, Time Series and Prediction

  Specifically this project is part of the second course in this specialization. 

- Dogs vs Cats is a dataset of 1500 images for each dogs and cats. Each image have a different sizes and is unlabel.

- The objective of this study is to correctly identify if the image is a dog or a cat.

# Code and Resources Used

- **Phyton Version:** 3.0
- **Packages:** pandas, numpy, sklearn, seaborn, matplotlib, tensorflow, keras, os. 

# Data description  

- Dogs vs Cats is a dataset of 1500 images for each dogs and cats. Each image have a different sizes and is unlabel.

- The images looks like:
  <p align="center">
   <img src="https://github.com/lilosa88/Dogs-vs-Cats/blob/main/Images/Screenshot%20from%202021-05-22%2006-57-57.png" width="760" height="480">
  </p> 
  
# Feature engineering

- We define each directory using os library.

- Use of data generators. It read the pictures in our source folders, convert them to float32 tensors, and feed them (with their labels) to our network. We have one generator for the training images and one for the validation images. The two generators yield batches of images of size 150x150 and their labels (binary). 

- Data that goes into neural networks should usually be normalized in some way to make it more amenable to processing by the network. In our case, we will preprocess our images by normalizing the pixel values to be in the [0, 1] range (originally all values are in the [0, 255] range). In Keras this can be done via the keras.preprocessing.image.ImageDataGenerator class using the rescale parameter. This ImageDataGenerator class allows you to instantiate generators of augmented image batches (and their labels) via .flow(data, labels) or .flow_from_directory(directory). These generators can then be used with the Keras model methods that accept data generators as inputs: fit, evaluate_generator, and predict_generator.

- Imagen Augmentation (only in the second and third model) which is a very simple, but powerful tool to help to avoid overfitting. To put it simply, if you are training a model to spot cats, and your model has never seen what a cat looks like when lying down, it might not recognize that in future. Augmentation simply amends your images on-the-fly while training using transforms like rotation, among others.

# Neural Network model

#### First model: Neural Network with convolution and pooling

- This model was created using tf.keras.models.Sequential, which defines a SEQUENCE of layers in the neural network. These sequence of layers used were the following:
  - Four Convolution layers with a corresponding MaxPooling layer each one which is then designed to compress the image, while maintaining the content of the           features that were highlighted by the convlution.
  - One flatten layer: It turns the images into a 1 dimensional set.
  - Two Dense layers: This adds a layer of neurons. Each layer of neurons has an activation function to tell them what to do. Therefore, the first Dense layer           consisted in 512 neurons with relu as an activation function. The second, have 1 neurons and sigmoid as activation function. 

- We built this model using RMSprop optimizer with lr=0.001 and binary_crossentropy as loss function.

- The number of epochs=100

- We obtained Accuracy 0.9875 for the train data and Accuracy 0.7050 for the validation data. As we can see we obtained a bag accuracy in validation, this is the result of overfitting.

 <p align="center">
   <img src="https://github.com/lilosa88/Dogs-vs-Cats/blob/main/Images/Screenshot%20from%202021-05-22%2007-12-00.png" width="360" height="480">
  </p> 
  
#### Second model: Neural Network with convolution and pooling making use of Imagen augmentation.

- This model was created using tf.keras.models.Sequential, which defines a SEQUENCE of layers in the neural network. These sequence of layers used were the following:
  - Four Convolution layers with a corresponding MaxPooling layer each one which is then designed to compress the image, while maintaining the content of the           features that were highlighted by the convlution.
  - One flatten layer: It turns the images into a 1 dimensional set.
  - Two Dense layers: This adds a layer of neurons. Each layer of neurons has an activation function to tell them what to do. Therefore, the first Dense layer           consisted in 512 neurons with relu as an activation function. The second, have 1 neurons and sigmoid as activation function.
  
- We built this model using RMSprop optimizer with lr=0.001 and binary_crossentropy as loss function. This was applied on the images with Imagen Augmentation.

- The number of epochs=100

- We obtained Accuracy 0.7970 for the train data and Accuracy 0.8030 for the validation data.

<p align="center">
   <img src="https://github.com/lilosa88/Dogs-vs-Cats/blob/main/Images/Screenshot%20from%202021-05-22%2007-12-00.png" width="360" height="480">
  </p> 
  
#### Third model: Neural Network with convolution and pooling

- This model was created using tf.keras.models.Sequential, which defines a SEQUENCE of layers in the neural network. These sequence of layers used were the following:
  - Three Convolution layer with a MaxPooling layer which is then designed to compress the image, while maintaining the content of the features that were                highlighted by the convlution. By specifying (3,3) for the MaxPooling, the effect is to quarter the size of the image.
  - One flatten layer: It turns the images into a 1 dimensional set.
  - Two Dense layers: This adds a layer of neurons. Each layer of neurons has an activation function to tell them what to do. Therefore, the first Dense layer           consisted in 512 neurons with relu as an activation function. The second, have 1 neurons and sigmoid as activation function. 

- We built this model using RMSprop optimizer with lr=0.001 and binary_crossentropy as loss function.

- The number of epochs=15

- We obtained Accuracy 0.9555 for the train data and Accuracy 0.7930 for the validation data.
