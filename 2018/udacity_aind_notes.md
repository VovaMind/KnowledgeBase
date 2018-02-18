# AIND udacity

##### Content    
[Overall](#overall)  
[HMM](#HMM)  
[Deep learning notes](#DL)  
[CNN contes](#CNN)  

<a name="overall"/>

## Overall

Using anaconda (conda). It helps to maintain several enviroments. Is it python-sprecific?

Using cloud computing power with GPUs. Possible option: https://aws.amazon.com/ru/ec2/. You pay for computational time.

<a name="HMM"/>

## HMM (hidden markov models).

Can be very useful. Trick to setup probability distributions inside nodes with some HMM configuration.

Helpful with analysing time series/data.

<a name="DL"/>

## Deep learing notes

Context: classification of points.

Perceptron trick: change weights of a linear function by coordinates of a point, use a class label to modify bias. Use a learning rate.

Perceptron algorithm: making iterations of perceptron trick.

To consider classification probabilities we can use sigmoid function: 1/(e^(-t) + 1).

Using error-function for a gradient descent. It should be continuous and differentiable.

Log loss function = -log(probability of correct classification). We should minimize it. We should use it to avoid probability multiplication and replace it with sum of logs.

Softmax function: e^(s_1) / (sum of e^(s_i)). It helps to move from scores to class probabilities.

Encoding: instead of enum, use boolean vector: is class 0, is class 1, ...

Likelihood: overall probability of smth. Likelihood -> max.

Cross entropy (CE): from max likelihood to minimum of -log(likelihood). CE = -sum(y_i * log(p(smth))). We can use CE for two classes or for multiclasses.

Logistic regression: sigmoid function over linear function with using CE. Algorithm: iterate points and go by gradient direction with a learning rate. 

Logistic regression vs preceptron algorithm: logistic regression trying to improve the score even in a context of correct classification.

In complicated cases we should consider non-linear models/functions.

We can combine many linear functions together with using sigmoid activation and build non-linear functions. We can do multi-class classification with using softmax. Thus, we got Neural Network(NN).

Each step in feedforward in NN can be computed by matrix multiplication. We can calculate an error in the end (cross-entropy etc).

Backpropogation - in dact it's just a gradient descent. We use chain rule in derivatives to compute it.

We can use Keras in order to fit and test NNs. We build a model from layers of computation and activation. We can compile the model with setting loss, optimizer, metrics. Then we can fit and evaluate the model.

We can use batches in the gradient descent. For each epoch we don't need all data, we can use subdata in oder to optimize everything.

Learning rate: too high -> no convergence, too small -> fitting a model will be too slow -> we won't able to train the model. If doesn't work try to descreace (?). Learning rate should be small if the solution is close.

It's important to have test + train datasets.

We can have two kind of problems with a model: overfitting, underfitting. Overfitting - we are considering the problem too specific, underfitting - we are using too simple model or we trained it poorly. NN are typically too complicated and we will use some technics to avoid overfitting.

Early stop - look at the train error and validation error and select the best model by the validation error.

We can use regularization. Common regularizations: L1 and L2. With L1 we can have king of features selection (many zeroes coefficients). With L2 we can get a better solution (?). It helps against overfitting.

Droupout. We can have a probability for each NN layer. With can drop X% of a layer in each iteration. In other words, we don't use the whole NN for each training iteration. It helps against overfitting.

Vanishing gradient. We use derivatives multiplication in order to perform gradient descent. If we will have too many layers, then gradient can "vanish" after many multiplications. We can use not sigmoid, but other activation functions: tanh, relu = max(0,x). At the end we still need to have sigmoid in case of binary classification.

Gradient descent makes locally optimal step. But with this appoach we can stuck at a local minima. To avoid we can do random restarts. We can use momentum (current_step + alpha * previous_sum, alpha < 1). 

We can use following optimizers in Keras:

*  Stochastic Gradient Descent (SGD). You can specify: learning rate, momentum, nesterov moment (?).
*  Adam (Adaptive Moment Estimation). It uses second moment (acceleration).
*  RMSProp. See my other notes about it.

Links about optimizers: https://keras.io/optimizers/, http://ruder.io/optimizing-gradient-descent/index.html#rmsprop (cool blog about NLP!).

<a name="CNN"/>

## CNN notes

Image input data. MNIST dataset.

Simple (MLP ?) NN works not that well on MNIST.

Train, validation, test.

Local connectivity (idea of using non fully conntected layers).

Convolutional layers. Use pattern (filter) and calculate result signal with an activation function.

Convolutional layers work like filters. 

Consider separetly R data, G data and B data. Normalize them to 0..1.

Stride - with which step are we moving convolutional filter. Padding adding zeroes "outside" of the image in order to get more conovultional results, but some of them will be computed by small parts of the image.

We can import and use convolutional layers in Keras.

Pooling layer -> reduce size by performing max / mean operation in submatrices. They also have stride. 

We can import and use pooling layers in Keras.

CNN finished with fully connected layers and softmax. CNN significantly outperforms "simple" NN in image recognition.

cifar 10 dataset. Images with classes.

Augmentation in image processing - add more data to a dataset. We can move image, rotate it, scale etc. In this way we will have much more data. We can do smth of it in Keras by using generation+fit_generator.

ImageNet - big dataset of images with many classes. 

Very strong CNNs: AlexNet, VGG, ResNet. See more at https://keras.io/applications/.

We can use CNNs to inject a picture to another picture.

We can look at the layers. First layers understand simple patterns. But with more layers it can find more and more specific patterns.

