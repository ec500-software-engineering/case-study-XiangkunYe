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
![Frameworks](https://github.com/ec500-software-engineering/case-study-XiangkunYe/blob/master/Frameworks:Libraries.png)
## Test Framework
Keras is using **Travis-CI** platform. To make sure it's meaningful, it has a varitey of tests include integration tests, component tests and performance tests. The most recent test coverage I find is in 
[Issue#60](https://github.com/keras-team/keras/issues/60):
![Coverage](https://github.com/ec500-software-engineering/case-study-XiangkunYe/blob/master/test_coverage.png) 

As we can see in this picture, the platform is Linux2 and the total coverage is *80%*.