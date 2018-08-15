---
layout: post
title: Cognitive Context Detection With Matlab
---

<a href="https://github.com/stevebottos/MATLAB-Cognitive-State-Detection" target="_blank">This repository </a>contains a program which employs a Neural Network (NN), written by me from scratch, designed to recieve input data in the form of an individual's pupil diameter in order to detect whether or not the particular individual is currently engaged in a task which they consider to be easy, somewhat difficult, or very difficult. A short training/calibration period is necessary (approximately 20 minutes - the duration can be adjusted depending on necessity), during which time the NN learns the specific parameters of that individual. After the training period the program is designed to take measurements every 2 minutes using data from that time frame to construct a single feature vector, outputting the level of focus that the individual was most likely experiencing during those two minutes.
> **Key Concepts**: Machine Learning, Neural Networks, Matlab, Feature Engineering
