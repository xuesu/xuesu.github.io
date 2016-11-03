# logistic classifier(linear classifier)
wx + b = y(w,b,x,y are all vector)

- just a giant matrix multiply
- x is input vector
- w weights
- b biased term
- scores in logistic classifier is often called logits

## softmax

```math
Score(y_i) = \frac{e_{yi}}{\sum_j {e_{yj}}}
```
turn scores into probabilities

```python
def softmax(x):
    return numpy.exp(x) / numpy.sum(numpy.exp(x),axis = 0)
```
注意numpy */ 是按元素进行乘除，矩阵乘法用dot

- if you increase the size of input(x), the classifier will be confident about the output

## one-hot encoding
L(yi):1.0 for right label yi, and 0 for others

1. using embeddings to handle big scale sparse matrix
2. measure how well we are doing by comparing two vectors(probabilities and vector after one-hot encoding) 

## cross entropy
to measure the distance between probabilities and vector after one-hot encoding

```math
D(S,L) = - \sum_i{(Li * log(Si))}

```
**Be careful,the cross entropy is not symmetric, D(S,L) != D(L,S)**

## Multinomial Logistic Classification
![image](https://github.com/xuesu/picture/blob/master/2016-10-10-173349_922x519_scrot.png?raw=true)

## Aim
1. have a high cross entropy distance for incorrect label, but have a low distance for correct label
2. to minimize the training loss


## Trainning loss
The average of cross entropy distance of all instances in training sets

it is a humongous function
![image](https://github.com/xuesu/picture/blob/master/2016-10-11-214408_716x437_scrot.png?raw=true)
## Normalized Inputs and Initial Weights and Bias
### 1. Normalized Inputs
To avoid lost accuracy

- mean(x) == e
    - ![image](https://github.com/xuesu/picture/blob/master/2016-10-11-213204_946x477_scrot.png?raw=true)
- equal variance(xi方差相等)

#### when dealing with Images
(r - 128)/128,(g - 128)/128,(b - 128)/128,
![image](https://github.com/xuesu/picture/blob/master/2016-10-11-214059_778x453_scrot.png?raw=true)
### 2. A simple way to picking initial weights
To avoid lost accuracy and fasten the process

- draw the weight randomly from **a Gaussian Distribution with mean zero and standard deviation sigma**
    - the sigma values determines the order of magnitude(数量级) of your outputs at initial point
    - a large sigma will make the distribution have large peaks, which going to be very **opinionated**
    - a small sigma will going to be less confident
- it is better to begin with an uncertain distribution and let it become more confident during progress

## a possible way - gradient descent
to compute the derivatives and finally reach the minimum.

Question: (where the optimizer is still in black-box)

1. how do you fill the pixels into classifier
2. where do you initialize the optimazation

## validation,test size - rule of thumb 30
a change that affects 30 examples in your validation set, one way or not,is usually statistically significant and typically can be trusted, 

the following picture descript which accuracy change is acceptable by rule of thumb 30
![image](https://github.com/xuesu/picture/blob/master/Deeplearning-ruleofthumb30-quiz.png?raw=true)

when validation set size > 30000, change > 0.1% is acceptable

cross-entropy is one way to mix this problem, but it is too slow,

get more data is often the right solution

## Optimizating a logistic classifier using gradient descent
the important Question is that how to scale gradient descent

## Stochastic Gradient Descent SGD
To reduce running time(calculate entire gradient takes a lot running time), instead of taking large step and calculate the gradient of all training sets, **taking small step and calculate small random fraction of the training sets(an estimate of actual gradient)**

- a terrible estimate in fact
- but it works in practice,comes with a lots of issues
- needs to pick very randomly

![image](https://github.com/xuesu/picture/blob/master/2016-10-11-115600_911x495_scrot.png?raw=true)

![image](https://github.com/xuesu/picture/blob/master/2016-10-11-115829_842x472_scrot.png?raw=true)

### Helping SGD

#### initial 
1. input
    - zero means
    - equal variable(SMALL)
2. initial weights
    - random
    - zero means
    - equal variable(SMALL)

#### Momentum(动量)
Cause:

1. each step toward a random direction
2. on aggregate, we toward the minimum loss

use w = 0.9w + gradient instead of gradient as the direction of each step

![image](https://github.com/xuesu/picture/blob/master/2016-10-11-220012_928x499_scrot.png?raw=true)

#### Learning Rate decay
1. exponential
2. reach the plateau

![image](https://github.com/xuesu/picture/blob/master/2016-10-11-220404_413x401_scrot.png?raw=true)

## Parameter Hyperspace
![image](https://github.com/xuesu/picture/blob/master/2016-10-11-220647_891x479_scrot.png?raw=true)

# Intro to Deep Neural Network
1. Regulation:make us enable to increase the scale of dataset
2. If you have N inputs, and K outputs, the complexity of the simple model above is (N+1)K![image](https://github.com/xuesu/picture/blob/master/2016-10-30-232511_944x443_scrot.png?raw=true)
3. linear model is limited ![image](https://github.com/xuesu/picture/blob/master/2016-10-30-234400_792x411_scrot.png?raw=true)
4. linear model is cheap(GPU) and good,we can show that small change in input can never yield big change in output
5. the derivative of the model is constant and stable.
6. we'd like to keep our model inside big linear models but we also want the model to keep nonlinear
# Rectified Linear Unit(RELU)
a nonlinear function lazy engineer perfered
```
y = x > 0?x:0
```
Add a RELU into Linear Function,the model is now nonlinear
![image](https://github.com/xuesu/picture/blob/master/2016-10-31-000150_917x453_scrot.png?raw=trueo)
H is the number of RELU units we inserted

The first Neural Network


1. The first layer effectively consists of the set of weights and biases applied to X and passed through ReLUs. **The output of this layer is fed to the next one, but is not observable outside the network**, hence it is known as a **hidden layer**.
2. The second layer consists of the weights and biases applied to these intermediate outputs, followed **by the softmax function to generate probabilities.**

# Chain Rule
For h(x) = g(f(x)),h'(x) = g'(f(x)) * f'(x)
- we can compute the derivative of h by taking the product of the derivative of different component
- It's easy to compute the derivative of whole function by lots of data reuse and pipeline
- So we can use a lot of simple funtion to build the model so that the deep learning model can handle it
# Back-propagation
![image](https://github.com/xuesu/picture/blob/master/2016-10-31-001714_843x379_scrot.png?raw=true)
- As long as the function is made up by simple block with simple derivatives, the learning framework help you work out the derivative by simple block
- It makes computing complex derivatives very effective


![image](https://github.com/xuesu/picture/blob/master/2016-10-31-002024_851x437_scrot.png?raw=true)
- Forward Prop:Running the model up to the prediction
- Back Prop:the model that goes backward and compute derivative
![image](https://github.com/xuesu/picture/blob/master/2016-10-31-002152_855x497_scrot.png?raw=true)
- The Back Prop always take twice compute complexity and memory complexity than Forward Prop