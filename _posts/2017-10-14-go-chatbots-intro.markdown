---
layout:     post
title:      "Intro to Goal-Oriented (GO) Dialogue Systems"
subtitle:   "Demystifying GO Chatbots"
date:       2017-10-15 12:00:00
author:     "Vladimir Ilievski"
header-img: "img/chatbot-front.jpg"
---

<h2> Before the Intro </h2>

<p>I recently started my final Master Thesis Project in <a href="https://www.swisscom.ch/en/business/enterprise/news/digital-lab.html" target="_blank"> Swisscom Digital Lab </a>, which is located in the <a href="https://epfl-innovationpark.ch" target="_blank"> EPFL Innovation Park </a> in Lausanne, Switzerland. My Master Thesis is building advanced goal-oriented dialogue systems, also known as chatbots. This is a first, of the series of blog posts I plan to write about my jorney. In this blog post, I will write a brief overview of the goal-oriented chatbots we are interested in.</p>


<h2> Intro </h2>


<p>Today, we live in the era of the Artificial Intelligence, which is penetrating in every aspect of our life. A part of this AI ecosystem are also the dialogue systems or so called chatbots, which usage is increasing every day. An example of such systems are the popular <a href="https://www.apple.com/ios/siri/" target="_blank">Apple's Siri</a>, <a href="https://en.wikipedia.org/wiki/Google_Now" target="_blank">Google Now</a> and <a href="https://www.microsoft.com/en-us/windows/cortana" target="_blank">Cortana</a> from Microsoft. </p>


<img src="{{ site.baseurl }}/img/what-are-chatbots.jpg" alt="">
<span class="caption text-muted">The user is trying to get a help from the chatbot</span>


<p>There are two different types of chatbots, depending on the conversation's nature. Therefore, there are open domain and closed domain dialogue systems. In the open domain setting, the conversation can go in any direction, thus, they are harder to implement. On the other side, the closed domain dialogue systems are easier to implement, since they focus only on several aspects and usually have predetermined intent, with a purpose to help the user to easily achieve some goal. For example, it could be a flight or restaurant table booking dialogue system, that helps users to book a flight or a table in a restaurant, in a most convenient way, i.e. by conversation. These are the chotbots I will ellaborate in depth.</p>


<h2> Goal-Oriented (GO) Dialogue Systems </h2>

<img src="{{ site.baseurl }}/img/goal-achieving.png" alt="" align="middle">
<span class="caption text-muted"></span>


<p>The Goal-Oriented (GO) Dialogue Systems are complex systems consisted of several subcomponents. In general there are two ways to implement dialogue systems.</p>

<p>The first way, is by modeling them as a <a href="https://en.wikipedia.org/wiki/Partially_observable_Markov_decision_process" target="_blank">Partially Observable Markov Decision Process (POMDP)</a>. The <a href="https://en.wikipedia.org/wiki/Reinforcement_learning" target="_blank">Reinforcement Learning (RL)</a>, is one rich subset of powerful and promising algorithms that can be applied to POMDP-based dialogue systems.</p>

<p>The second one is fully supervised, by applying the recurrent neural nets encoder-decoder principles, mainly applied in the machine translation. These models are trained in a sequence-to-sequence fashion and require a considerable amount of annotated human-human or human-machine dialogues since the system is trying to mimic the knowledge of the expert. Moreover, we don't have a control over the internal state, which means we can not model the dialogue as we wish.</p>


<h2> GO Chatbots as Partially Observable Markov Decision Processes </h2>

<p>If we model the Dialogue Systems as POMDP, then, several components are compromising that system. At the core of the dialogue system lies the Dialogue Manager (DM), and there are two other important components around the DM, namely the Natural Language Understanding (NLU) unit and the Natural Language Generator (NLG) unit. Additionally, the DM could be connected to some external knowledge base or data base, such that, it can produce more meaningful answers. This composition is shown in the image below. </p>


<img src="{{ site.baseurl }}/img/Dialogue_System.png" alt="">
<span class="caption text-muted">Dialogue System modeled as a Partially Observable Markov Decision Process. The user utterance is parsed by the NLU unit producing a dialogue act understandable for the system. In the Dialogue Manager, the state tracker is estimating the state such that the RL agent could take the ideal action. This action is further passed to the NLG unit and finally presented to the user in a human readable form.</span>


<h3> Natural Language Understanding Unit </h3>

<p>The NLU unit is responsible for transforming the user utterance, to a predefined semantic frame according to the system's conventions, i.e. to a format understandable for the system. Therefore, it is a glue between the user and the rest of the system. This component is usually a recurrent neural network with LSTM cells.
</p>

<h3> Natural Language Generator Unit </h3>

<p>The Natural Language Generator Unit, on the other side is the glue between the system and the user. Given the system response, given as a semantic frame, it maps back to a natural language sentence, understandable for the user. The NLG component can be rule-based, using hand-crafted features or model-based, having learnable parameters. In some scenarios it can be a hybrid model, i.e. a combination of both. </p>


<h2> Dialogue Manager </h2>

<p>The central part of the Dialogue System is the Dialogue Manager (DM), which is constituted of the following two parts: the Dialogue State Tracker (DST) and the Policy Learning which is the RL agent.</p>

<p>The Dialogue State Tracker (DST) is a complex and essential component that should correctly infer the belief about the state of the dialogue, given all the history up to that turn. The Policy Learning is responsible for selecting the best action, i.e. the system response to the user utterance, that should lead the user towards achieving the goal in a minimal number of dialogue turns. I will elaborate more on these topics in the next blog post.</p>


<h2> Closing </h2>

<p>Given all of this, the goal-oriented chatbots based on Markov Decision Processes are quite interesting and challenging topic to research. My opinion is that, it is still quite new topic and there are a lot of missing parts, until we reach highly efficient and super intelligent chatbots, but we are on that way.</p>

