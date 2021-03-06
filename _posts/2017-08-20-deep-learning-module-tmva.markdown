---
layout:     post
title:      "Deep Learning Module in TMVA"
subtitle:   "The development of a Deep Learning Module in TMVA, submodule of CERN's data analysis tool, ROOT"
date:       2017-08-20 12:00:00
author:     "Vladimir Ilievski"
header-img: "img/gsoc17.png"
---

<h2> Intro </h2>
<p>As part of the <a href="https://summerofcode.withgoogle.com" target="_blank">Google Summer of Code</a> (GSoC) 2017, under the mentorship of <a href="http://hepsoftwarefoundation.org" target="_blank">CERN-HSF</a> umbrella organization, is the development of a Deep Learning Module in TMVA (Toolkit for Multivariate Analysis) which includes almost every Machine Learning method, except the Deep Learning one. TMVA is a submodule in <a href="https://root.cern.ch" target="_blank">ROOT</a>, a data-analysis tool for High Energy Physics.</p>

<p>Since this kind of a module is already too vast, we are a group of three students working on three different parts of the module. I am working on the Convolutional Neural Networks, one student is working on the Recurrent Neural Networks and the last one is working on the Auto Encoders.</p>

<p>Although these networks have a different kind of nature and goals, thinking on a Software Engineering plane, they all have a common ground and share to a big extent the same patterns.</p>

<p>For this reason, it was challenging to design such a module, that will satisfy and fit all needs, be easily maintainable and extensible and in the same time compatible with the TMVA standards. In the following blog post, I will give a general and brief overview of the Software Engineering solution for this Deep Learning Module within TMVA. </p>


<h2> Solution </h2>
<p>The solution and the implementation of this Deep Learning Module is motivated and it is based on the work done by Simon Pfreundschuh, GSoC 2016 student, who developed the foundations and enabled us to continue and add more complex and sophisticated solutions on top of it. The blog, describing his project can be found <a href="http://simonpf.github.io/gsoc/" target="_blank">here</a>.</p>

<p>The design of the entire Deep Learning Module is given in the figure below. As it can be seen, it is a big puzzle, so let me give you a more detailed view. </p>

<center>
<img src="{{ site.baseurl }}/img/TMVA_DL_General.png" alt="">
<span class="caption text-muted">An overview of the Deep Learning Module in TMVA</span>
</center>

<h3> Layers </h3>
<p>In general, one deep neural network, is a configuration of several layers with different nature. For this reason, the layers are playing the central role. Each layer is specialized to perform one particular operation on the input in order to produce some output that can be used by some other layer and so on.</p>

<p>In order to enable this smooth chaining of the layers, they all extend the generic, pure virtual <i>General Layer</i> class, which design is shown in the diagram below. The introduction of the generics, decouples the algorithmic implementation of the layers and the hardware-specific implementations of the underlying numerical operations. There are three types of low-level interfaces or also called architectures: <i>Reference</i>, <i>CPU</i> and <i>GPU</i>. The <i>Reference</i> one, is only for testing purposes and it is not using any specialized library. The <i>CPU</i> architecture is based on the <a href="http://www.netlib.org/blas/" target="_blank"><i>BLAS</i></a> (Basic Linear Algebra Subprograms) library, which is highly optimized for matrix multiplications. <a href="https://www.geforce.com/hardware/technology/cuda" target="_blank"><i>CuDA</i></a> is the only support for a GPU-based execution.</p>

<center>
<img src="{{ site.baseurl }}/img/General_Layer.png" alt="">
<span class="caption text-muted">General Layer class</span>
</center>


<p>Since the generic <i>General Layer</i> class, lies at the bottom of this module, it entails almost every class to be generic. Therefore, the generic <i>Deep Net</i> class contains a vector of pointers to <i>General Layer</i> class objects, therefore leveraging the polymorphic mechanism. It is responsible for the entire forward and backward propagation through the layers, as well as for the initialization, loss calculation and prediction.</p>

<h3> Tensor Data Loader and DL Minimizer </h3>
<p>The <i>Tensor Data Loader</i> and <i>DL Minimizer</i> classes are individual and independent classes, that represent crucial service classes. The <i>Tensor Data Loader</i> class is managing the streaming of the training and testing data to the accelerator device in a round-robin manner. It creates a set of batches by shuffling the training and testing examples. Therefore, a deep neural network is fed using these batches.</p>

<p>The <i>DL Minimizer</i> class represents a generic, architecture and input data independent implementation of the gradient descent minimization algorithm. It does that, by providing the functions, <i>Step</i>, <i>StepMomentum</i> and <i>StepNesterov</i>, that perform a single minimization step using different techniques.</p>

<h3> Method DL class </h3>
<p>This is the main class, assembling everything that was mentioned before. First, it parses the user input specifying the Deep Net configuration, and accordingly instantiating it. Then, given the training and testing settings it is managing the process of training, testing and evaluating the Deep Neural Net.</p>


<h2>Conclucion</h2>
<p>This blog post was only an outline and the general idea behind the Deep Learning Module in TMVA. There are a lot of details that were intentionally missed and that can be found in the official documentation. Working on this collaborative project was very challenging and in the same time funny. I learned a lot and I hope we established a solid foundation for the further development and advancing of this module.</p>
