---
layout: page
title: Projects
---
---
## Side Project - Fingerpainting
[![Video](https://drive.google.com/uc?export=view&id=1Jmhx7iZ_OHfoR-M_ndZ_UFMtyiZHc0Lg)](https://drive.google.com/file/d/1a1NFsWVs_xlhgb0FV8ehbv2VC7uQHslN/view?usp=sharing "Fingerpainting Demo")

Earlier this week, I got the idea for a little side project - an app that lets you "fingerpaint" in real time over a video. So far, I've gotten the foundations of an "eraser" function down (shown in the video) which allows the use the palm of your hand to erase your doodles. The actual finger painting portion is next on the list.

I've seen a lot of hand gesture recognition models out there, but they have their limitations - an image processing approach to segment out hands is prone to error in different lighting conditions/background noise environments (eg. if there's a face in the picture that's the same color as the hand), while RCNN/CNN approaches give either the region that a hand exists in or the gesture on screen, but not the actual boundaries of the hand. A more robust approach is to use a Mask-RCNN in order to detect the each pixel that contains a hand and its gesture, and then go from there. I used the Matterport Mask-RCNN in this demo, trained on a custom dataset that I put together and labeled myself. It's a bit choppy in real time, but I attribute that partly to my GPU which only has 4gb vram available - Google Colab's Tesla T4's have about a 90ms processing time per image whereas I'm getting about 300ms on my hardware. Nonetheless I plan on replacing the Resnet101 backbone with a mode computationally friendly model, such as MobileNet, to allow for fast inference regardless of hardware. The source code can be found <a href="https://github.com/stevebottos/fingerpainting" target="_blank">here</a>.
> **Key Concepts**: Python (OpenCV), Machine Learning, Computer Vision, Real-Time Image Processing, Mask Region-Based Convolutional Neural Networks, Custom Models

---
## Side Project - Webcam Eye Tracker
[![Video](https://drive.google.com/uc?export=view&id=1rSsakx7WO5QPaCVOOysAef5OVoMKBksi)](https://drive.google.com/file/d/1f-ut3deaM1Uz_6YP6-ZlMmx69Kmlo377/view?usp=sharing "Eye Tracker Demo")

A webcam eye tracker, currently a work in progress, which is intended to perform comparably to more expensive hardware/software for a mere fraction of the price. This began as an experimental side project that was to be tested during my graduate research, however at some point other research endeavors took priority. The end goal was to obtain map an individual's eye-gaze points to (x,y)-coordinates on a plane - ie: the computer screen. In its current state, the program functions as an accurate iris localization tool. The source code can be found <a href="https://github.com/stevebottos/eye-tracker" target="_blank">here</a>.
> **Key Concepts**: Python (dlib, OpenCV), Machine Learning, Computer Vision, Real-Time Image Processing

---
## Side Project - Analyzing All Los Angeles Parking Violations from 2018
![Image](https://drive.google.com/uc?export=view&id=15vwG3Jr6j0ksBJJVPxq5frij2xJ7r9yK "Violations Map")

With a bit of free time this weekend, I decided to do some hobby coding in Python, which I've presented <a href="https://stevebottos.github.io/jupnotes/LA Parking Violations 2018" target="_blank">here as a Jupyter Notebook</a> with an interactive map and some interesting visualizations extracted from the data. The point of this side project is to create a map of LA according to parking tickets received from last year (2018) and to produce some helpful visualizations/gain some insights. I want to start with the full dataset (~9-million x 19, saved as a .csv > 1gb) to gain more experience handling large .csv files that are cumbersome to work with in Python unless processed in batches (especially when you don't have much RAM available). (Note: as os 2020 I'd have done this in Spark rather than Pandas to take advantage of its distributed computing features and excellent dataframe implementation).
> **Key Concepts**: Python (Numpy/Matplotlib/Pandas/Folium(Mapping Package)), Jupyter Notebooks, Data Science, Big Data

---
## Cognitive Context Detection With Tensorflow
In previous projects, I demonstrated how to implement a Neural Network from start to finish using only home-made functions written in both Matlab and Python. I've uploaded [a Tensorflow implementation](https://github.com/stevebottos/TENSORFLOW-Cognitive-State-Detection) for the sake of comparison (note that this was written pre-Keras, Tensorflow code can now be written much more intuitively using Keras wrappers). I've concluded that Tensorflow offers increased productivity in the form of quicker-to-write code and faster training times. The optimization functions that TF offers are great, and allowed me to train my models in a fraction of the time that Matlab or Python+Numpy in conjunction with the GPU acceleration capabilities. Comparing the two files MatlabResults in the [Matlab Implementation](https://github.com/stevebottos/Matlab-Cognitive-State-Detection) and TensorflowResults in this repo demonstrate the notable accuracy improvements that Tensorflow offers as well.
> **Key Concepts**: Tensorflow, Python (Numpy/Scipy/Matplotlib/Pandas), Machine Learning, Neural Networks, Data Science

---
## Cognitive Context Detection With Python
In a previous project, I demonstrated how to implement a Neural Network from start to finish using only home-made functions written in Matlab. I've finally uploaded [an identical Neural Network, but written with Python](https://github.com/stevebottos/PYTHON-Cognitive-State-Detection). This is just the Neural Network itself for comparison, and it does not include any of the pre-processing steps that the Matlab code base showcases. Data which was already prepared is included in the repository. For a full ReadMe describing the original use of the code, and its applications, check the <a href="https://github.com/stevebottos/MATLAB-Cognitive-State-Detection" target="_blank">original Matlab repository</a>.
> **Key Concepts**: Python (Numpy/Scipy/Matplotlib/Pandas), Machine Learning, Neural Networks, Data Science

---
## Hidden Markov Model Tutorial
Hidden Markov Models are powerful tools, commonly used in a wide range of applications from stock price
prediction, to gene decoding, to speech recognition.<a href = "https://github.com/stevebottos/stevebottos.github.io/blob/master/_downloads/HMM_Tutorial.pdf" target = "_blank"> This is a tutorial</a> on Hidden Markov Models that I wrote, and thought to would make publicly available for download since I believe it captures the intuition quite well. 
> **Key Concepts**: Hidden Markov Models, Machine Learning, Tutorials, Statistical Analysis

---
## C++ Tutorials
<a href="https://github.com/stevebottos/cpp_tutorials" target="_blank">This repository </a>contains a collection of C++ tutorials that I put together for a class of junior electrical engineering students. They're designed to be short, simple, and accessible to complete beginners. I've been getting good feedback from the students, so I thought that I would share the tutorials with whoever may be interested in them.
> **Key Concepts**: C++, C, Coding, Tutorials

---
## Gaze Tracking System
<a href="https://stevebottos.github.io/jupnotes/GazeTrackerWriteup" target="_blank">Here </a>you’ll find a Jupyter Notebooks writeup detailing Version 1 of the Gaze Tracking System. The Gaze Tracking System designed to determine which line of text that an individual is currently reading given absolutely no prior knowledge of the page layout or what is being displayed on the screen whatsoever. Currently, the algorihm is able to detect when a reader progresses from one line to the next down the page, beginning from the top, and is able to accurately pinpoint in real time when this change of lines takes place. Given noisy data, the system performs well, and is able to accurately construct the layout of the page in terms of lines of text on the page in real time.<br/>
> **Key Concepts**: Machine Learning, Python (Numpy/Pomegranate), Bayesian Statistics, Hidden Markov Models

---
## Cognitive Context Detection With Matlab
<a href="https://github.com/stevebottos/MATLAB-Cognitive-State-Detection" target="_blank">This repository </a>contains a program which employs a Neural Network (NN), written by me from scratch, designed to recieve input data in the form of an individual's pupil diameter in order to detect whether or not the particular individual is currently engaged in a task which they consider to be easy, somewhat difficult, or very difficult. A short training/calibration period is necessary (approximately 20 minutes - the duration can be adjusted depending on necessity), during which time the NN learns the specific parameters of that individual. After the training period the program is designed to take measurements every 2 minutes using data from that time frame to construct a single feature vector, outputting the level of focus that the individual was most likely experiencing during those two minutes.
> **Key Concepts**: Machine Learning, Neural Networks, Matlab, Feature Engineering, Data Science

---
## The Hockey Summit Website
<a href="http://thehockeysummit.com/" target="_blank">TheHockeySummit.com</a> is an ongoing project of mine. The coach of the San Diego Gulls and founder of THS, Justin Roethlingshoefer, had approached me asking if I was available to work on the site for him in early 2018. I was, and still am, a bit of a web-dev hobbyist so I welcomed the opportunity to work on something new. I currently manage any front-end or back-end changes to the site that must be implemented as the company grows. 

