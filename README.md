# Case Study about Keras from XiangkunYe
## Technology and Platform used for development
### 1. Language
Keras is a high-level neural networks API, written in Python and capable of running on top of [TensorFlow](https://github.com/tensorflow/tensorflow), [CNTK](https://github.com/Microsoft/cntk), or [Theano](https://github.com/Theano/Theano). 
It was developed by Python. **I think the same languages would be used and I myself would used the same language if the project was started today** for following reasons:

a) Python is widely used in deep learning field. It even become more popular today. Many other library are based on Python so that they can cooperate well. There's no reason for Keras to choose another language.

b) Since Keras is focusing on enabling fast experimentation. Just as they wrote in readme: *Being able to go from idea to result with the least possible delay is key to doing good research.* 
The easy-to-use and flexible feature makes Python exactly the language for this project.

c) Although Keras support TensorFlow, CNTK, and Theano. But by default and in most cases it will use TensorFlow as its tensor manipulation library. And the interface provided by Tensorflow is also in Python.
### 2. Build System
The build system used by Keras is Cmake and Bazel.
### 3. Frameworks / Libraries
![Frameworks](https://github.com/ec500-software-engineering/case-study-XiangkunYe/blob/master/Frameworks.png)
## Test Framework
Keras is using **Travis-CI** platform. To make sure it's meaningful, it has a varitey of tests include integration tests, component tests and performance tests. The most recent test coverage I find is in 
[Issue#60](https://github.com/keras-team/keras/issues/60):

![Coverage](https://github.com/ec500-software-engineering/case-study-XiangkunYe/blob/master/Test_Coverage.png) 

As we can see in this picture, the platform is **Linux2** and the total coverage is **80%**.
## Software Architecture
In [User experience design for APIs](https://blog.keras.io/user-experience-design-for-apis.html), we can find that:
>Keras is an API designed for human beings, not machines. Keras follows best practices for reducing cognitive load: it offers consistent & simple APIs, it minimizes the number of user actions required for common use cases, and it provides clear and actionable feedback upon user error.

So basically Keras won't require user to implement or specify a lot of details but provided complete and detailed APIs. But if we want to add/edit functionality, of course we could do that. For example, we can define our own optimizer by subclassing keras.optimizers.Optimizer:
```
class MyOptimizer(Optimizer):
    optimizer functions here.
```
Then instantiating it in our model:
```
myOpt = MyOptimizer()
model.compile(loss='binary_crossentropy', optimizer=myOpt, metrics= ['accuracy'])
```
Instead of standalone program, the most common way to use Keras is to import it into your own project, and it's already been integrated into Tensorflow.
But according to my research, Tensorflow supports threads and queues to train heavy tensors asynchronously, which provides TPUs a better and much faster processing speeds. However Keras is synchronous, so you won't be able to do that in Keras. Here's the system diagram:

![Diagram](https://github.com/ec500-software-engineering/case-study-XiangkunYe/blob/master/System_Diagram.png) 

We can use those modules to build our specific nerual network and use dataset to train it. Then the weight information would be stored into a hdf5 file and be used later. And since Keras is based on Python, I think it's a mix of object oriented or functional component. Object oriented
might be the larger part because each module I mentioned before is actually a call and will be use as a instance.
##  Defect Analysis
### 1. Language
Keras is based on Python, which make it user-friendly and easy to use. However, this is also its defect. Python is known to have a low efficiency. Also, the human-oriented API design without a lot of user specified detail make it hard to build a outstanding model.
### 2. Deep learning implementation
[ISSUE#7515](https://github.com/keras-team/keras/issues/7515) discussed a particular approach of the data-parallel SGD algorithm. It remarkably increased the efficiency of SGD by computing gradients in each tower separately, then averaged on PS device. But now it's still not implemented yet beacause
the main contributor in this issure before don't have much time to continue working on this problem.
## Demo
I developed a program consist of a 3 lays convolutional neural network and a 5 lays convolutional neural network based on Keras and Tensorflow.
Then using about 700 images of car and cat to train them. Here's the predict result:

![Predict](https://github.com/ec500-software-engineering/case-study-XiangkunYe/blob/master/Predict.png) 

And here're two line charts about the trend of loss and accuracy during training process of 3/5 lays convolutional neural network ***(First for 3, second for 5)*** .

![image](https://github.com/XiangkunYe/EC601_Deep-Learning/blob/master/Chart/Original_Chart3.png)

![image](https://github.com/XiangkunYe/EC601_Deep-Learning/blob/master/Chart/Original_Chart5.png)

As you can see, in this amount of datasets, the 3 lays convolutional neural network perform well while overfitting occured just after several epoches in the 5 lays convolutional neural network model.
