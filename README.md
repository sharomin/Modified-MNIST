# Modified-MNIST
Image Processing Project which the goal was to perform an image analysis prediction challenge. The task is based upon the MNIST dataset (https://en.wikipedia.org/wiki/MNIST_database). The original MNIST contains handwritten numeric digits from 0-9 and the goal is to classify which digit is present in an image. Here, I worked with a Modified MNIST dataset. In this modified dataset, the images contain more than one digit and the goal was to find which number occupies the most space in the image. Each example is represented as a 64 × 64 matrix of pixel intensity values (i.e., the images are grey-scale not color).
# Introduction
In this project, we design a supervised classification model for a Modified MNIST prediction task. Our dataset consists of 50, 000 grayscale images with 64x64 pixel resolution, containing MNIST handwritten digits, and each image may contain multiple digits and background noise. Each digit in an image, has a different size and has been transformed (rotated, translated, etc.), therefore image preprocessing tasks are performed prior to feeding the data to our model. OpenCV and numpy libraries are used for preprocessing to find and crop the largest contour in each image, and normalize the pixel values. Also, our classification model is a CNN (Convolu- tional Neural Network) implemented using Keras library with Tensorflow backend and written in Python. Training dataset consists of 37, 500 images labeled based on the digit that occupies the most space in the image, and is fed to our CNN for training the model. Validation data consists of 2,500 labeled images and is used to fine-tune hyperparameters and select the best model. Our test dataset contains 10,000 unlabeled images and best CNN model is used to classify these data into 10 classes (0-9). Finally test labels are submitted to class competition website on Kaggle which resulted in an accuracy of 0.95566 for prediction of labels on test data.
> MNIST database (Modified National Institute of Standards and Technology database) is a collection of handwritten digits used for training and testing of various image processing systems [1]. We use a model based on Convolutional Neural Network (CNN) to detect the largest digit present in each image in our MNIST dataset.
OpenCV is an Open-source Computer Vision library designed for computational efficiency and with a strong focus on real-time application. It is written in optimized C/C++ and has become popular worldwide for use in image processing, robotics and real-time video and image applications [2].
1
Convolutional Neural Network (CNN) is a state-of-the-art image recognition technique, used mainly in computer vision and image analysis, and is part of a larger family of modern machine learning methods called deep learning. CNN based models consist of networks of fully and partially connected layers designed to recognize visual patterns directly from pixel images with minimal preprocessing. These networks can recognize patterns with extreme variability such as handwritten character and digits (MNIST), and are robust systems with high accuracy even in presence of distortions and simple geometric transformations [3].
Keras is a high-level neural network API, written in Python and can run on top of other libraries such as Tensorflow and Theano. Keras is highly popular and has a large community mainly due to offering a single API across many popular neural network libraries, and because of enabling fast experimentation [4]. For reasons mentioned above, we have selected Keras to implement our CNN.
Tensorflow is also an open-source software library for neural network developed originally by Google researchers and engineers working on Google Brain team to conduct machine learning and deep neural network research [5].
4 Proposed Approach
Convolutional Neural Networks (CNN) are biologically-inspired variants of Multilayer percep- trons (MLP)[3] which exploit spatially-local correlation in images by enforcing a local connec- tivity pattern between neurons of adjacent layers [7]. A CNN consists of an input and an output layer as well as multiple hidden layers. These hidden layers consists of convolutional layers, ReLU layers (an activation function), pooling layers (e.g. MaxPool), fully connected layers and/or normalization layers [10, 11]. CNNs are trained using back propagation. They are made up of neurons that have learnable weights and biases, and have a loss function on the last (fully-connected) layer such as Sigmoid for binary and Softmax for multi-class classification tasks. We implement 2 CNN models based on figures 1 and 2 , using Keras library, and opti- mize hyperparameters to select the best performing model on our validation dataset. We also experiment with pretrained models VGG16 and ResNet. Following section describes steps and layers used in our CNNs.
4.1 Data augmentation
Data augmentation is done using ImageDataGenerator module to improve generalization. Small random rotation, shifting horizontally and vertically, and zooming is applied to training data to help with capturing important features in our training dataset [4].
4.2 Callback Functions
Callback functions from Keras library, used to save internal states and statistics of the model during training at the end of an epoch if accuracy of validation set has increased, and also to reduce learning rate when model accuracy has stopped improving.(we used two functions, ReduceLROnPlateau and LearningRateScheduler)
4.3 Convolutional Layer
3x3 kernel size and ReLU activation used at each convolutional output. Activation layer controls how the signal flows from one layer to another. Output signals which are strongly associated with past references would activate more neurons, enabling signals to be propagated more efficiently for identification. The most common activation function is Rectified Linear Unit because of faster training speed (ReLU = Max(0,x)) [7, 4].
4.4 Max-pooling
2x2 max-pooling with strides of 2x2 is used at the end of each block. Max-pooling is a form of non-linear down-sampling and outputs the maximum value. Max-pooling is useful in vision for two reasons: By eliminating non-maximal values, it reduces computation for upper layers. Since it provides additional robustness to position, max-pooling is a “smart” way of reducing the dimensionality of intermediate representations. [10, 6]
3
 4.5 Dropout
Figure 1: CNN1
 Figure 2: CNN2
Dropouts applied by randomly setting a fraction rate of input units to 0 at each update during training time, which helps prevent overfitting[4].
4.6 Output Layer
Softmax activation function is used at the output layer with 10 classes [7].
ezj σ(zj) = 􏰂Kk=1 ezk
4.7 Batch Size & Number of Epochs
Our final CNN is trained on data generated in batches of 128 and 30 epochs, chosen based on accuracy and computational efficiency.
4.8 Compilation
CNN is compiled with Adam optimizer, accuracy metric and categorical-crossentropy loss. Adam is a computationally efficient algorithm for gradient-based optimization aimed towards machine learning problems with large datasets and/or high-dimensional parameter spaces [12].
4.9 Validation Dataset
Prediction on validation data is used to evaluate the accuracy of the network. This will help to fine-tune hyperparameters, prevent overfitting on the training data, and lower the learning rate
 4

if necessary.
4.10 VGG16 & ResNet
A pre-trained network is a saved network that was previously trained on a large on a large-scale image-classification task. We adapted architecture of VGG16 for one CNN, used an ensemble of our CNN and VGG, and also experimented with ResNet model[6, 8].
