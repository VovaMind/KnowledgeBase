# AIND udacity

##### Content    
[Overall](#overall)  
[HMM](#HMM)  
[Deep learning notes](#DL)  
[CNN notes](#CNN)  
[Autoencoders](#autoencoders)  
[RNN](#RNN)  
[LSTM](#LSTM)  
[RNN/LSTM notes](#RNN_LSTM_notes)  

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

Transfer learning. The idea is to reuse finished CNN arcitecture and replace only last layes there and train only small part of the model. Potentially we can retrain from starting weights or retrain the whole model. 

Instructions (datasets - old and new):
Size | Similar datasets | Different datasets
--- | --- | ---
Small | end of ConvNet | start of ConvNet
Large | fine-tune | fine-tune or retrain

In Keras/practically: we precompute signals from other CNN and use them to finish training.

We can use CNNs for image segmentation.

<a name="autoencoders"/>

## Autoencoders

Can help with removing noise from images. The idea is to train a NN which will transform input->input over a small bottleneck layer. We can use CNN to train autoencoders. 

It's a kind of advanced PCA, but non-linear.

<a name="RNN"/>

## RNN

Motivation - taking into account "sequential" property of data. In "usual" NN (FNN) we consider inputs independently. And a lot of data is sequntial: text, stocks price etc. We can't take a sequence into account with usual NNs.

We can train usual NN on sequential data and for some simple cases it would work. However, it still have the fundametal problem - context ignoring. Data isn't i.i.d., it's a sequence.

The main trick - F(t) (result function), will depend not only on input(t), but also from hidden_state(t-1). So we don't loose the information about "context" and about previous data. In "usual" networks we don't remember previous inputs and context.

Idea of representation - over time layers.

RNNs require large datasets. Vanishishing gradient problem (we do backprop over many time layers back). To avoid it we can use special architectures (LSTM, GRU etc) and other gradient descendants. You should split long sequences of data into the smaller windows.

tanh activation function is popular. Does it help with the vanishing gradient??

<a name="LSTM"/>

## LSTM

Key links:

*  http://colah.github.io/posts/2015-08-Understanding-LSTMs/
*  http://blog.echen.me/2017/05/30/exploring-lstms/
*  https://www.youtube.com/watch?v=iX5V1WpxxkY

Key idea of LSTM is splitting memory into two parts: long-term memory (LTM) and short-term memory (STM). LTM rembeber the whole context on a high-level. STM remembers only recent changes.

It contain 4 gates: forget gate (we remove info from LTM), learn gate (we combine STM and input), remember gate (we add learn gate data to forget data) and use gate (we combine learn gate and forget gate). Rember gate result -> new LTM. Use gate -> new STM.

Idea LSTM(input[t], LTM[t-1], STM[t-1]) - > output[t], LTM[t], STM[t].

LSTM is just a one possible RNN architecture. We also have GRU, LSTM modified by peephole connections etc.

<a name="RNN_LSTM_notes"/>

## RNN/LSTM notes

We can use character-wise RNNs. Input - 1 character, output - 1 character. We use softmax at output layer.

We can use multiple layers of LSTM with stucking them up. LSTM[i - 1]->LSTM[i] (feed-forward), LSTM[i]->LSTM[i] (recursion).

We should do batching - split input sequence into several parts. Than we will move "window" with some width and height == number of parts. The idea is to use matrix operations and don't put into the NN too big sequences.

dynamic rnn in TF - the idea is having arbitary size input.

hyperparameters: batch_size (amount of parts?), num_steps (length of training sequence, width of the window, longer is better - longer dependencies, but it's also time consuming, 100 is a good starting point, lstm_size - amount of nodes/units in the hidden layer, keep_prob - dropout rate, num_layers, learning_rate).

RNN resources:

*  https://www.youtube.com/watch?v=iX5V1WpxxkY
*  http://colah.github.io/posts/2015-08-Understanding-LSTMs/
*  https://r2rt.com/recurrent-neural-networks-in-tensorflow-i.html

### Hyperparams

Heavily depend on a task.

We can split into two categories. Optimizer params: learning rate, minibatch size, number of epochs. Model params: number of layers/units, model details, activation etc.

Learning rate. Too small - not converging, too big - suboptimal or even explode. Potencial values: 0.1, 0.001 etc till 10^-6 or 10^-7. We can use adaptive learning to change learning rate dynamically. TF adaptive learning optimizers: AdamOptimizer, AdagradOptimizer.

Minibatch size. Typically 2^x. Popular values: 32, 64, 128, 256. Small minibatch size have an advantage - stochastic and doesn't stuck at a local minima. Bigger minibatch size - faster computation, because of matrix multiplication.

Number of epochs/iterations. See on validation error. Validation error can be noisy - so be careful with the stop rule (like, stop only in a case of absence of improvements for X epochs).

Number of hidden units. It can be quite high, because of regularization and dropout. Too high is overfitting. But small overfitting is ok for NNs. So, put it high nut not super-high. Number of layers - increase in a case of underfitting. Underfitting - make the model more complicated (by units/layers).

FNN - 3 layers is better than 2, but 4 rarely helps. CNN - deeper often means better. RNN with LSTM/GRU performance can be good at 2, but 3 can be bad. For modern speech recognition they use 5-7 RNN layers.

Long story short: experiment and take a look on the data and the results.

Sources:

*  https://arxiv.org/abs/1206.5533
*  http://www.deeplearningbook.org/contents/guidelines.html
*  http://neuralnetworksanddeeplearning.com/chap3.html#how_to_choose_a_neural_network's_hyper-parameters
*  http://yann.lecun.com/exdb/publis/pdf/lecun-98b.pdf
*  https://arxiv.org/abs/1507.05523
*  https://arxiv.org/abs/1606.02228
*  https://arxiv.org/abs/1506.02078

### Sentiment analysis

tBD
