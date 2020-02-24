---
layout: post
title: Side Project - Analyzing All Los Angeles Parking Violations from 2018
---

<!-- 
Need to take file id from sharable link and stick it into a new format... ie: if https://drive.google.com/file/d/<FILE_ID>/view?usp=sharing is the sharable link, make it: https://drive.google.com/uc?export=view&id=<FILE_ID>
-->

![Image](https://drive.google.com/uc?export=view&id=15vwG3Jr6j0ksBJJVPxq5frij2xJ7r9yK "Violations Map")

With a bit of free time this weekend, I decided to do some hobby coding in Python, which I've presented <a href="https://stevebottos.github.io/jupnotes/LA Parking Violations 2018" target="_blank">here as a Jupyter Notebook</a> with an interactive map and some interesting visualizations extracted from the data. The point of this side project is to create a map of LA according to parking tickets received from last year (2018) and to produce some helpful visualizations/gain some insights. I want to start with the full dataset (~9-million x 19, saved as a .csv > 1gb) to gain more experience handling large .csv files that are cumbersome to work with in Python unless processed in batches (especially when you don't have much RAM available). (Note: as os 2020 I'd have done this in Spark rather than Pandas to take advantage of its distributed computing features and excellent dataframe implementation).
> **Key Concepts**: Python (Numpy/Matplotlib/Pandas/Folium(Mapping Package)), Jupyter Notebooks, Data Science, Big Data
