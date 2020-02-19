---
layout: post
title: Side Project - Webcam Eye Tracker
---

<video width="480" height="320" controls="controls">
<source src="https://drive.google.com/file/d/1f-ut3deaM1Uz_6YP6-ZlMmx69Kmlo377/view?usp=sharing" type="video/mp4">
</video>

<!-- [![Video](http://img.youtube.com/vi/KOxbO0EI4MA/0.jpg)](https://www.youtube.com/watch?v=KOxbO0EI4MA "Audi R8") -- >

test A webcam eye tracker, a work in progress. Intended to perform comparably to more expensive hardware/software for a mere fraction of the price. This began as an experimental project that was to be used during my grad research, however at some point other endeavors took priority. There is much improvement to be done here, first some kind of smoothing/estimation algorithm should be put to work so that the iris detection isn't so jittery/inconsistent, I know that the Kalman filter would be a good candidate. Next, the pupul should be extracted from the iris and drawn as a point. Finally, the pupil location should be mapped to (x,y) coordinates on a plane - ie: the computer screen. <a href="https://stevebottos.github.io/jupnotes/LA Parking Violations 2018" target="_blank">here as a Jupyter Notebook</a>.
> **Key Concepts**: Python (Numpy/Matplotlib/Pandas/Folium(Mapping Package)), Jupyter Notebooks, Data Science, Big Data
