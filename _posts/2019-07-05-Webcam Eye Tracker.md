---
layout: post
title: Side Project - Fingerpainting
---
<!-- 
Need to take file id from sharable link and stick it into a new format... ie: if https://drive.google.com/file/d/<FILE_ID>/view?usp=sharing is the sharable link, make it: https://drive.google.com/uc?export=view&id=<FILE_ID>
-->

[![Video](https://drive.google.com/uc?export=view&id=1Jmhx7iZ_OHfoR-M_ndZ_UFMtyiZHc0Lg)](https://drive.google.com/file/d/1a1NFsWVs_xlhgb0FV8ehbv2VC7uQHslN/view?usp=sharing "Fingerpainting Demo")

Earlier this week, I got the idea for a little side project - an app that lets you "fingerpaint" in real time over a video. So far, I've gotten the foundations of an "eraser" function down (shown in the video) which allows the use the palm of your hand to erase your doodles. The actual finger painting portion is next on the list.

I've seen a lot of hand gesture recognition models out there, but they have their limitations - an image processing approach to segment out hands is prone to error in different lighting conditions/background noise environments (eg. if there's a face in the picture that's the same color as the hand), while RCNN/CNN approaches give either the region that a hand exists in or the gesture on screen, but not the actual boundaries of the hand. A more robust approach is to use a Mask-RCNN in order to detect the each pixel that contains a hand and its gesture, and then go from there. I used the Matterport Mask-RCNN in this demo, trained on a custom dataset that I put together and labeled myself. It's a bit choppy in real time, but I attribute that partly to my GPU which only has 4gb vram available - Google Colab's Tesla T4's have about a 90ms processing time per image whereas I'm getting about 300ms on my hardware. Nonetheless I plan on replacing the Resnet101 backbone with a mode computationally friendly model, such as MobileNet, to allow for fast inference regardless of hardware. The source code can be found <a href="https://github.com/stevebottos/fingerpainting" target="_blank">here</a>.
> **Key Concepts**: Python (OpenCV), Machine Learning, Computer Vision, Real-Time Image Processing, Mask Region-Based Convolutional Neural Networks, Custom Models
