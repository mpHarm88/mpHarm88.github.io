---
layout: post
title: 👩‍🦼Wheel Good CNN in 30 hours (Hackathon)
subtitle: Making a Convolutional Neural Network with limited data
bigimg: img/stepfree.jpg
image: img/wheelGood_horz.png
gh-repo: mpHarm88/wheelgood_cnn
gh-badge: [star, watch, fork, follow]
tags: [tensorflow, keras]
---

#### Purpose
The Wheelgood Convolutional Neural Network (CNN) purpose was to identify storefronts and routes in cities and determine how accessible the building or route was to limited mobility users (wheelchair, walkers, canes, etc.). The model would also issue a confidence rating with each prediction on how sure it was that the building could be accessed.

A user could theoretically type in an address as they would in any maps interface, and the corresponding street view image(s) would be fed into the CNN to determine if the route and building front were accessible. If the recommended route were deemed inaccessible by the CNN the model would direct the user to an alternate route that the model determined to be accessible and provide a confidence rating of its prediction. Using computer vision, the model would identify small pieces of each image, such as edges, corners, curves, and so on until it could recognize an entire accessible or inaccessible feature. 

<div align="center">
  <img src="/img/wheelGood_horz.png"><br>
</div>

#### Process
Initial tests of the model started by trying to identify curb cuts found in street view images. By manually gathering images from street view and reverse image search, we were able to collect 111 images depicting what we deemed were accessible curb cuts and 129 images that we determined to be inaccessible curb cuts. Moderns CNN's train, validate, and test on thousands of pictures, and our training and test sets became the bottleneck of our research while trying to complete out intended purpose in the time allotted (30 hours). 

To compensate for our lack of data, we applied data augmentation to the limited amount of photos. Data augmentation allows us to adjust each image slightly by rotating, zooming in, stretching, and flipping each image multiple times to artificially create more pictures and never letting our model to see the same image twice. After data augmentation, our entire image set increased to just under 2500 images.

To combat overfitting our CNN due to artificially similar images being introduced, we incorporated a dropout layer to help regularize the network. We also included max-pooling to deal with overfitting and to reduce computational cost during repeated iterations.

#### Results
Our mean baseline was 46.17%, and our highest iteration of our model was 51.67%. The model is not inherently useful and, in its current state, is not recommended as an indicator for determining if a route or building front is accessible to someone with limited mobility. 

#### Final Thoughts
With more time, we would significantly increase the size of our training set along with increasing the diversity of images in the training set. The initial groundwork implemented by the Data Science team should be taken into future iterations of the project and used as a reference for decisions moving forward.

Find the website for the project [here](https://wheelgood.netlify.com/)
