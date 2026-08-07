---
date: '2016-12-04'
title: '说话人识别相关'
draft: true
math: true
categories: ["Signal Processing", "CN"]
tags: ["research", "CN"]
---

开山之作，提出用GMM 和 GMM-UBM 来做说话人识别，统治了说话人识别十几年

- D. Reynolds, T. Quatieri, and R. Dunn, “Speaker verification using adapted gaussian mixture models”

联合因子分析方法

- P. Kenny, G. Boulianne, P. Ouellet, and P. Dumouchel, “Joint
factor analysis versus eigenchannels in speaker recognition"

I-vector 首次提出，用一个低维的向量来表征说话人特性
- N. Dehak, P. J. Kenny, R. Dehak, P. Dumouchel, and P. Ouellet,
“Front-end factor analysis for speaker verification”

在supervector上使用 SVM 做说话人区分学习
- W. Campbell, D. Sturim, and D. Reynolds, “Support vector machines using gmm supervectors for speaker verification”

开始使用 DNN 来提取GMM中的BW统计量，和用 DNN-HMM 做语音识别中的方法类似
- P. Kenny, V. Gupta, T. Stafylakis, P. Ouellet, and J. Alam, “Deep
neural networks for extracting baum-welch statistics for speaker
recognition"

Google 提出用深度网络做说话人区分性特征提取的工作
- V. Ehsan, L. Xin, M. Erik, L. M. Ignacio, and G.-D. Javier, “Deep
neural networks for small footprint text-dependent speaker verification"

PLDA 方法
- S. Ioffe, “Probabilistic linear discriminant analysis”
