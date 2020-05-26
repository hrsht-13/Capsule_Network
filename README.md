# Dynamic Routing Between Capsules
A Keras implementation of CapsNet in the paper:

[Sara Sabour, Nicholas Frosst, Geoffrey E Hinton. Dynamic Routing Between Capsules. NIPS 2017](https://arxiv.org/abs/1710.09829) 

This repository contains code to the section(4) which closely simulate those run by Geoffrey Hinton in the paper linked to above.


**Differences with the paper:**   
1. We only report the test errors after `50 epochs` training. In the paper they trained for `1250 epochs` according to Figure A.1
2. We only experimented routing iteration 2 and 3 in our code but paper did on 2,3,5,7 and 10

## Warning

Please use Keras==2.2.4 with TensorFlow==1.15.0 backend, or the `K.batch_dot` function may not work correctly.

## Dataset

Download the training and test dataset from the link given below:

```
http://www.cs.toronto.edu/~tijmen/affNIST/
```

## Usage

This code has been compiled on `Colab Notebook` and thus has **Callbacks files** accordingly to save the model, weights and results. If you don't want to save these just comment out the lines corresponding to `ModelCheckpoint` and `CSVLogger`


**Step 1. Clone this repository to local.**
```
https://github.com/HB5101/CapsNet_Project.git
```
**Step 2.
Install Keras==2.2.4 with TensorFlow==1.15.0 backend.**
```
pip install tensorflow==1.15.0
pip install keras==2.2.4
```

To access `idx3-ubyte` file as numpy array:
```
pip install idx2numpy
```

## Trained Weights and biases 

We have trained a model using the above command, the trained model is
saved in `.h5 file`, which can be downloaded from:

for routing iteration=2
```
https://drive.google.com/file/d/1l2oiNhAeWxEKE4MlTwaL3oC3LShNy9g9/view
```
for routing iteration=3
```
https://drive.google.com/file/d/1pLiw2Boeedmbx9fe631dgBfkn9W_128c/view
```
The testing data is same as the validation data. It will be easy to test on new data, just change the code as you want.


## Results

#### Test Errors   

CapsNet classification test error on MNIST.
Losses and accuracies on Test set only for routing iteration=3

![](cap-master/training.png)
![](cap-master/loss.png)

The data for the above graph is save in CSV_data folder.


#### Training Speed

About `285s / epoch` on Google Colab GPU for routing iteration=2.

About `448s / epoch` on Google Colab GPU for routing iteration=3.


#### Reconstruction result

Digits at left-side are real images from MNIST and digits at right-side are corresponding reconstructed images.

![](cap-master/original.png)
![](cap-master/reconstructed.png)

#### Conclusions from the experiment

1. With different number of routings we have different losses for initial epochs, but after a sufficient number of epochs losses         
converges to the same range.
2. While, training with routing iterations 2 and 3, we observed that with 2 routings, loss was initially high which drastically dropped just after few initial epochs, whereas when number of routings was increased to 3, model started with low loss which eventually decrease slowly. 
3. In general more routing iterations increases the network capacity and tends to overfit to the training dataset 
4. The paper itself is not very detailed and hence it leaves some open questions about specifics of the network implementation that are as of today still unanswered because the authors did not provide their code.

