---
layout: page
title: Projects
---
---
## Side Project - Analyzing All Los Angeles Parking Violations from 2018
With a bit of free time this weekend, I decided to do some hobby coding in Python, which I've presented <a href="https://stevebottos.github.io/jupnotes/LA Parking Violations 2018" target="_blank">here as a Jupyter Notebook</a>. The point of this side project is to create a map of LA according to parking tickets received from last year (2018) and to produce some helpful visualizations. I want to start with the full dataset (~9-million x 19, saved as a .csv > 1gb) to gain more experience handling large .csv files that are cumbersome to work with in excel and are slow to work with in Python unless processed in batches (especially when you don't have much RAM available). 
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

