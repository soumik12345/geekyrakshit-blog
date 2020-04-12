---
toc: true
layout: post
description: Deep Learning Techniques used to verify and recognize faces can also be extended to replicate Facebook apps saying which celebrity do you look like
categories: [ComputerVision, DeepLearning, FaceNet, Inception, Keras, NearestCelebrityFace, Python, Tensorflow]
title: Nearest Celebrity Face using Deep Learning
---
# Nearest Celebrity Face using Deep Learning

## Face Recognition

Face Recognition is one of the more interesting applications of Deep Learning i. At a single glance, it may seem like a simple classification problem; classify if this photo shows Soumik’s face or Souranil’s. You might be quick to jump to the conclusion, oh, the handsome face on the right belongs to Soumik and the ugly face on the left belongs to Souranil but, Ahem!!! We beg to differ.

<figure class="image">
    <center>
        <img src="{{site.baseurl}}/images/nearest-celeb-face/img_1.jpg">
        <figcaption>Dear ConvNet, which of these is Soumik and which one is Souranil???</figcaption>
    </center>
</figure>

See, the problem with traditional ConvNets is that they need to look at lots of images of your face and lots of other faces to learn to correctly classify them; maybe a thousand images from each category. Imagine yourself as the teacher of a class where you want to install a system, which monitors every student and recognize them by faces so that they would not bunk classes (poor students 😓). In order to do so you have to collect 1000 mugshots of each of your students!!! Even if you manage to do this insane task, just imagine having to retrain the model again if a new student decides to join your lecture!!!

Ideally, we would want to verify the face of a person from any footage given only one photo of the person available in the database. Hence, our challenge, in this case, can be formalized as a **One-Shot Learning** problem. History has been witness to the fact that Deep Learning algorithms do not work well if you have only one training example.

## One-Shot Learning

Let’s focus a bit more light on the problem discussed earlier with an example. Our dear friend Atul is supposed to appear for a video interview for a company and he wants to remain undisturbed during the interview, so he won’t allow anyone into his room other than Abhik who speaks a lot of Crox English and would help him with the interview (from behind the laptop of course). So, he wants sets up a system using his phone camera which would verify if the person who wants to enter his room is Abhik or not. Now, Atul can simply design a ConvNet with convolutional layers followed by a couple of fully connected layers ending in a softmax activation with 3 outputs corresponding to the three of us.

<figure class="image">
    <center>
        <img src="{{site.baseurl}}/images/nearest-celeb-face/img_2.jpg">
        <figcaption>Which of us speaks the best Crox will be decided upon by Atul’s algorithm!!!</figcaption>
    </center>
</figure>

There are several demerits to this approach such as

- Atul does not have more than thirty of our mugshots which he painfully collected from Facebook and Instagram. Such a small training set would not be enough.
- If he decides to accept help from Avishek besides Abhik, he would have to retrain the model again (after painfully collecting his mugshots) in order for the algorithm to recognize Avishek also.

So, in order to make this work, Atul thinks of a different approach. Instead of building a model to differentiate various faces, he decides to build a model that would learn a Similarity Function D. Then that would say how similar the current image is with a mugshot of Abhik that is present in his dataset and he decides upon a similarity threshold τ upon meeting which the door will open.

<center>
D(image1, image2) = Degree of Difference between the Images
D(image1, image2) <= τ means images are same, and
D(image1, image2) > τ means images are different
</center>