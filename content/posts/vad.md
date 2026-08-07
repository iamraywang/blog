---
title: "Review of Voice Activity Detection"
draft: true
date: 2023-02-28
math: true
categories: ["Signal Processing"]
tags: ["vad", "speech"]
---

In speech signal processing, auto speech recognition (ASR) is much well known than voice activity detection (VAD), because VAD a sub modual but not a full-application directly facing user interface. Indeed, VAD is very important in any production of speech data pre-processing.

## Task Definition
Voice activity detection is the task of looking for voice activity in an audio stream. Basically, it should tell speech apart from noise and silence. Given input audio feature $X = [x_1, x_2, ..., x_T]$, the task of VAD is the predict $Y = [y_1, y_2, ..., y_T]$, each $y_i$ is the probability of speech or noise/silence in current time. Here, the definition of $X$ and $Y$ is generalized in terms of time granularity(Can represent both audio chunk, frame, etc). 

Based on the definition. Oh! This task seems easy enough, just a binary classification problem. But, a modern VAD should satisfy some main criteria
- **High quality**: Enough high precision and recall, maybe separately consider in different situations.
- **Low user perceived latency**: It's only a pre-processing step, important but cannot affect the whole pipeline latency.
- **Generalization**: Robustness for all domains, audio sources, noise, quality, and SNR levels
   
## Related Works
   
### Traditional Solution

This kind of solution does not use any kind of external models, it uses signal processing methods or simple pattern recognition methods to estimate the silence and speech parts. Typically use GMM to model speech/silence frames and do iteratively estimation using algorithms like EM. This kind of solution has low latency but cannot generalize well for many situations. Indeed, it needs much parameter settings for a target situation to get usable performance. Google’s WebRTC VAD is a kind of this method.

### Deep Solution

Deep neural network (DNN) is currently widely used in many signal processing tasks. DNN-based methods all need supervised label data for training. VAD is such a hard task for human annotation, we don’t know what time granularity to labeling and human labeling can easily introduce errors. The time granularity of labeling decide the final system granularity, but as common sense, we know human may not hear clearly, and labeling is less than 100 ms.

Here are some typical DNN-based VAD.

**Pyannote**: Pyannote is a toolkit for speaker diarization, VAD is a sub-modular in its pipeline. It use rttm-like file as a label file, randomly select a 2000 ms chunk and calculate the label for each frame in the chunk. With this processing method, it can also support speaker change point detection, overlap detection, end-to-end diarization.

**NeMo**: Nemo is a NN toolkit developed by Nvidia that can use for many speech and NLP model implementations. The VAD detail in their published model MARBLENET, it use 630ms chunk size for a prediction. train, val and test chunk numbers are 160,994, 20,018 and 60,906. So, nearly 28 hours data.

**Silero**: Silero VAD claimed it’s trained using 13000h data, but it did not publish any training and data details, because they say their model is good enough and robust for any language in any situation. They do not need to publish their details, anyone did not need to train the model, only can use their model as a toolkit just like Google’s WebRTC VAD. In detail, in use a transformer-liked model. Using 512, 1024, 1536 samples for 16000 sample rate and 256, 512, 768 samples for 8000 sample rate. Nearly 30ms,60ms,100ms, it’s almost frame-level.

PS: Some other methods use ASR model to perform force-alignment for the training data and get a frame-level label for VAD.

## Others

Time granularity is important, it determines not only the performance but the availability of downstream tasks. Using deep solution, we need to face the problem of data collection and annotation. However, VAD seems a more or less solved task due to its simplicity and abundance of data in a way, but the reality is that we hardly use it in some situations.
