---
layout: post
title:  "PCIe X16 vs X8 vs X4 when using GPU for Deep Learning"
date:   2020-11-01 17:06:14 +0100
categories: GPU "deep learning"
---

* TOC
{:toc}

## Goal

The goal of this experiment is to find if using X4 PCIe has an impact in performance when using the GPUs for Deep Learning.
I'm currently designing my new PC and I need that information to choose the motherboard. I have found a [comparison for X16 vs X8](https://www.pugetsystems.com/labs/hpc/PCIe-X16-vs-X8-with-4-x-Titan-V-GPUs-for-Machine-Learning-1167/#pcie-x16-vs-x8-vgg-in-keras-tensorflow-disk-streaming-25000-images-brtitan-v-gpus-br-training-time-for-4-epochs)
but I have been unable to find information for X4.

I will also be testing if having a greater distance between gpus leads to better performance due to better cooling.

## Setup

| hardware    | model                                                                |
|-------------|----------------------------------------------------------------------|
| motherboard | [Z170A SLI PLUS](https://es.msi.com/Motherboard/Z170A-SLI-PLUS.html) |
| gpus        | 2x 1080                                                              |
| cpu         | Intel Core i7-6700K 4.0 Ghz 4core                                    |

TODO: add a picture of the computer

![picture of the motherboard pcie ports](/res/2020-11-02-10-36-31.png)

Experiments to run:

* Single GPU on all the PCIe ports
* Two gpus in all the possible combinations.
  * Independent trainings
  * Training with the two gpus

Compare training speed and temperature of the gpus.

## Results

### Single GPU

On this experiments I simply moved the GPU over all PCIe slots and performed the same training.
Placing the GPU on PCIe6 was difficult because there are some connections of the motherboard below
that slot and I had to remove them all. I had to use an screwboard after removing the connections.

TODO: picture of the wires

![time per epoch](/res/2020-11-03-15-33-10.png)

| PCIe | epoch time (s) | slowdown    |
|------|----------------|-------------|
| X16  | 30.92          | 0           |
| X8   | 31.61          | 2.1%        |
| X4   | 32.51 (32.93)  | 4.9% (6.1%) |

![GPU temperature](/res/2020-11-03-15-41-47.png)

### Double GPU

![time per epoch](/res/2020-11-03-15-48-04.png)

| PCIe   | epoch time (s) | slowdown |
|--------|----------------|----------|
| X16 X4 | 36.81          | 7.7%     |
| X8 X4  | 37.46          | 9.2%     |
| X16 X8 | 33.98          | 0        |

There is a clear slowdown when not using the X16 slot for double GPU training.
On the training X8-X4 the gpus were closer than any on the other trainings and
thus the temperature was higher. So part of the slowdown of that experiment could
be caused by hotter GPU.

![GPU temperature](/res/2020-11-03-15-50-50.png)

### Relation between GPU temperature and frequency

## Summary

A slowdown has been observed both when using single gpu training and dual gpu training.
