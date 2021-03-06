---
layout:     post
title:      "Google Summer of Code '17"
subtitle:   "Accepted for GSoC '17 under the mentorship of CERN-HSF"
date:       2017-05-06 12:00:00
author:     "Vladimir Ilievski"
header-img: "img/gsoc17.png"
---

<h2> Intro </h2>
<p>What a good news, I was accepted to participate in the <a href="https://summerofcode.withgoogle.com" target="_blank">Google Summer of Code</a> 2017 under the mentorship of <a href="http://hepsoftwarefoundation.org" target="_blank">CERN-HSF</a> umbrella corporation. I will be working on the project "Convolutional Deep Neural Networks on GPUs for Particle Physics Applications". More about this project can be find <a href="http://hepsoftwarefoundation.org/gsoc/proposal_TMVAconvolutional.html" target="_blank">here</a>. </p>


<p>The <a href="https://en.wikipedia.org/wiki/Convolutional_neural_network" target="_blank">Convolutional Neural Networks (CNNs)</a> are one special type of a deep learning neural networks with an enormous discriminative power for image classification. In fact, they significantly outperform the standard Computer Vision techniques of manually extracting image features and then building classifiers on top of them. Although they are already established model in the Machine Learning community, their potential in the High Energy Physics is still growing.</p>

<p>Since <a href="https://root.cern.ch" target="_blank">ROOT</a> is the state-of-the-art data analysis tool developed by <a href="https://home.cern" target="_blank">CERN</a> and extensively used in the High Energy Physics, it is of paramount importance to integrate such a solution in its submodule called TMVA (Toolkit for Multivariate Analysis).</p>

<h2>Conv Nets</h2>
<p>Despite the fact that there is a vast amount of resources to learn about the CNNs, I will give a brief overview in this post. While I was learning for them, I've found very useful and I am highly recommending the <a href="http://cs231n.github.io" target="_blank">Stanford's CS231n course</a> "Convolutional Neural Networks for Visual Recognition".</p>

<p>The Convolutional Neural Networks have an architecture of predefined layers. Each layer is having its own characteristics and provides interfaces for interaction with the other layers. One CNN is typically consisted of the following layers: Convolutional layer (CONV), Pooling layer (POOL) and Fully-Connected (FC) layer. Logically, the Convolutional and the Pooling layers are represented as a cube of neurons, with specified width, height and depth. The output of the network is a vector representing the probabilities that the given input belongs to a corresponding class. One example of a CNN is given in the figure below.</p>


<img src="{{ site.baseurl }}/img/conv-net-bird.png" alt="">
<span class="caption text-muted">An example of a CNN which should learn that there is a bird on the picture</span>



<p>The CONV layer is a cube of neurons, where the cube is having a predefined number of identical rectangular slices with predefined width and height. The number of slices defines the depth of the layer. The neurons input values are calculated by means of <a href="https://en.wikipedia.org/wiki/Convolution" target="_blank">convolution</a>, of a small region in the input space and a predefined filter, such that each slice is associated with a different filter. The small region in the input space is called a receptive field of the neuron and all neurons extending in one depth column see the same region in the input space, or they have the same receptive field, but perceived through a different filter. The values inside of these filters are defining the parameters to be learned.</p>


<p>Similarly, the POOL layer is also a neuronal cube, derived from the previous layer, but only spatially downsampled. In fact, this is the only aim of the layer, to perform spatial downsampling of the previous layer, which means it does not contain any parameters to be learned. </p>

<p>The FC layer is a standard layer where each neuron is connected with each neuron in the previous layer.</p>

<p>The training of the CNN is also executed using the <a href="http://neuralnetworksanddeeplearning.com/chap2.html" target="_blank">backpropagation algorithm</a>, such that it is taking a slightly different form, since we have the convolution and downsampling operations.</p>

<h2>Closing</h2>

<p>I hope this summer will be interesting, challenging and productive and that all Google Summer of Code participants will do a good job and make the Open Source community stronger and richer.</p>

