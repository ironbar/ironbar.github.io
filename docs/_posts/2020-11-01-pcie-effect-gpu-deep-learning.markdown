---
layout: post
title:  "PCIe X16 vs X8 vs X4 when using GPU for Deep Learning"
date:   2020-11-01 17:06:14 +0100
categories: gpu "deep learning"
---

## Goal

The goal of this experiment is to find if using X4 PCIe has an impact in performance when using the GPUs for Deep Learning. 
I'm currently designing my new PC and I need that information to choose the motherboard. I have found a [comparison for X16 vs X8](https://www.pugetsystems.com/labs/hpc/PCIe-X16-vs-X8-with-4-x-Titan-V-GPUs-for-Machine-Learning-1167/#pcie-x16-vs-x8-vgg-in-keras-tensorflow-disk-streaming-25000-images-brtitan-v-gpus-br-training-time-for-4-epochs) 
but I have been unable to find information for X4. 

I will also be testing if having a greater distance between gpus leads to better performance due to better cooling.

## Setup

TODO: add a table with the hardware 

TODO: add a picture of the computer

![picture of the motherboard pcie ports](/assets/2020-11-02-10-36-31.png)

Experiments to run:

* Single gpu on all the PCIe ports
* Two gpus in all the possible combinations.
  * Independent trainings
  * Training with the two gpus

Compare training speed and temperature of the gpus.


## Results

## Summary
