---
layout: post
title: "Neural Networks"
meta: "neural-networks"
permalink: /case-studies/neural-networks/
next-case-study-title: "000"
next-case-study-url: /case-studies/000/
hide-hire-me-link: true
---

As part of general course work in 2011, I produced an artificial neural network capable of learning.

Artificial neural networks, in machine learning and cognitive science, are a family of models inspired by biological neural networks (the central nervous systems of animals, in particular the brain) and are used to estimate or approximate functions that can depend on a large number of inputs and are generally unknown. The connections between nodes have numeric weights that can be tuned based on experience, making neural nets adaptive to inputs and capable of learning. Like other machine learning methods - systems that learn from data - neural networks have been used to solve a wide variety of tasks that are hard to solve using ordinary rule-based programming, including computer vision and speech recognition.

In this case I created it to demonstrate the <a href="https://en.wikipedia.org/wiki/Simon_effect">'Simon effect' phenomenon</a>. In psychology, the Simon effect refers to the finding that reaction times are usually faster, and reactions are usually more accurate, when a stimulus occurs in the same relative location as the response, even if the stimulus location is irrelevant to the task. By replicating the effect in an artificial 'brain', I showed that Simon effect is inherent to the network. Regardless of whether it's a network of neurons or computer memory.

<strong>Material used</strong>
Feedforward neural network (FNN) library for R

<strong>Detailed walkthrough</strong>
The Simon task contains three relevant orthogonal dimensions and constitutes in this way a non-linear separable problem (3 factors, 2 levels each). Thus a multilayer network is required with a minimum of three hidden nodes to code for the underlying dimensions. Human subjects inherently experience a strong association between the spatial nature of stimuli and spatial responses. This could be a result of hebbian learning: objects to the left are grasped faster and more often by the left hand and vice versa. This would result in stimulus location and action response to get more strongly linked in the brain.
In the first phase this model is trained on exactly this association. Instructions are at this point irrelevant and are therefore absent. This mirrors daily life experience in that stimulus characteristics (other than spatial position) are irrelevant to plan a directional motor response. One learns to grasp a great many things while disregarding their form, colour or current task demands. The learning speed in this phase is set high, purely out of practical considerations (to reduce the required number of sweeps). To increase the external validity of this model however, it would have been better to implement an extremely high number of sweeps. Interaction with spatial objects is likely a very common task and the corresponding learning effect would be caused by sheer frequency, rather than some special benefit to the learning rate. However here it would seriously inflate processing time in the training phase and make simulations impractical to work with.

After the training phase the network is trained on the Simon task itself. The number of sweeps is here much smaller, since human subjects would be less experienced with this task as compared to their daily practise.

Finally, we check for any congruency effects as displayed by the model. To be exact, we expect a smaller difference in activation values between correct and incorrect response output during incongruent trials (due to interference effects). On congruent trials the difference would be much larger as both dimensions reinforce one another in eliciting the same response. These difference reflects the error rate of the model (rather than reaction time). The model’s reactions do indeed correspond to a Simon effect, confirming the original hypothesis.

<a href="/_post_images/2015/10/s1.jpg"><img src="/_post_images/2015/10/s1.jpg" alt="s1" width="301" height="528" class="aligncenter size-full wp-image-6256" /></a>
<em>Network training error, the artificial network 'making mistakes' while it is learning. After about 400 iteration the task is learned and hardly any errors remain.</em>

<a href="/_post_images/2015/10/t3.jpg"><img src="/_post_images/2015/10/t3.jpg" alt="t3" width="534" height="537" class="aligncenter size-full wp-image-6255" /></a>
<em>Hinton diagram, visualizing the values of a 2D array: Positive and negative values are represented by white and black squares.</em> 

<a href="/_post_images/2015/10/s2-123.png"><img src="/_post_images/2015/10/s2-123.png" alt="s2-123" width="1170" height="402" class="aligncenter size-full wp-image-6259" /></a>
<em>Network structure of 3 out of 9 input patterns. The squares represent the nodes of the network ('neurons') with their repective synaptic connections.</em>


---

{% include promo-next.html %}
