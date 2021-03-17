---
date: "2021-03-13"
title: Lec 3 CNN & Self-Attention
type: book
weight: 3
math: true
---

# Convolutional Neural Network

[CNN Slides](https://1drv.ms/b/s!AhPTUXN0QjiSzVgnNZdCaB541wom?e=ExXHDj)

<p align="center"><iframe src="https://onedrive.live.com/embed?cid=923842747351D313&resid=923842747351D313%219944&authkey=AM1atCz6L5jgfFw&em=2" width="760" height="500" frameborder="0" scrolling="no"></iframe></p>

The homework may be more important than the lectrue, in this part.

## Neuron Version Story

One image can be represented 3-D tensor, one dimension for length, one dimension for width, one dimenstion for channel (e.g. RGB). Width and length determines the pixels, channel determines the color.

Fully connected network may lead to overfitting. We tend to focus on critical patterns by choosing **Receptive Field**. 

Receptive field can be very free, there is one typical setting of receptive field: all channels, kernel size (e.g., 3×3).

[![6wQho4.md.png](https://s3.ax1x.com/2021/03/13/6wQho4.md.png)](https://imgtu.com/i/6wQho4)

The neurons with different receptive fields share the parameters.

## Filter Version Story

There are a set of filters detecting small patterns. Each filter convolves over the input image.

## Pooling

Max pooling, mean pooling etc. make the image smaller.

Flatten the output after pooling into a vector, then it may be put into a fully-conneted layer.


# Self-Attention

[Self-Attention Slides](https://1drv.ms/b/s!AhPTUXN0QjiSzVdq7Lk3kyp9RoL9?e=QAMZmw)


<p align="center">
<iframe src="https://onedrive.live.com/embed?cid=923842747351D313&resid=923842747351D313%219943&authkey=AGZNmF_BZ4BJeMM&em=2" width="760" height="500" frameborder="0" scrolling="no">
</iframe>
</p>

When the input is a set of vector, e.g., in word embedding,voice recognition.

What is the output:
- Each vector has a label **Sequence Labeling**
- The whole sequence has a label
- Model decides the number of labels itself. **seq2seq**

Self-attention absorbs all vectors and output the same number of vectors with (context)

# Videos (from youtube)

## CNN

{{<youtube OP5HcXJg2Aw>}}

## Sell-Attention

{{<youtube hYdO9CscNes>}}

