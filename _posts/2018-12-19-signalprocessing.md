---
layout: post
title: '地震背景噪声处理（信号处理理论）'
date: 2018-12-29
author: 路过音乐
color: rgb(255,210,32)
categories: myorigion
tags: 地震学 背景噪声 信号处理
---

#### 前言  

最近一直在看信号处理的东西，希望能将地震背景噪声处理的更好，已有的论文有利用S变换，曲波变换，小波变换等对地震噪声做处理，尤其是应用在pws和tf-pws（Time-Frequency phase weighted stack）的公式推导中，今日又看到一个[波原子变换](http://waveatom.org/)，甚是无解，又一直不太理解频率，尺度，相位，还有各种变换的联系和区别，故在这里做个总结。    


### 1.傅立叶变换（Fourier Transform）  
傅立叶变换是将信号分解为不同频率正弦波的叠加，得到频率域信息  

![fourier](/assets/article_img/2018-12-19-signalprocessing-1.jpg)  

注：针对不同种类的信号共有四种基本傅里叶变换，分别是：针对连续周期信号的连续傅里叶级数(Continuous Fourier Series, CFS，一般直接简称为FS)、针对连续非周期信号的连续时间傅里叶变换(Continuous Time Fourier Transform, CTFT，一般直接简称为FT)、针对离散周期信号的离散傅里叶级数(Discrete Fourier Series, DFS)、针对离散非周期信号的离散时间傅里叶变换(Discrete Time Fourier Transform, DTFT)，这四种基本傅里叶变换都不适合计算机处理（要求时域和变换域均为离散的、有限长的），因此把DFS进行变形，取其时域和频域的主值区间定义出了离散傅里叶变换(Discrete Fourier Transform, DFT)，直接按照DFT公式计算的话计算量太大，于是就又有了各种快速计算方法，统称为快速傅里叶变换(Fast Fourier Transform, FFT)。

傅立叶变换缺点：不能刻画时间域上信号的局部特性，只适用于确定性信号及平稳信号


### 2.短时傅立叶变换（Short-time Fourier Transform,STFT）  
傅立叶变换的时域是负无穷到正无穷，为了表现信号局部特性，通过**加窗**将信号分解为时域上的不同过程，得到频率域与时间域信息，属于时频分析  

![short-time fourier](/assets/article_img/2018-12-19-signalprocessing-2.jpg) 

g(s)表示窗函数，例如Gauss窗，Hanning窗，Hamming窗等等，当窗函数选择高斯窗，所得变换称为Gabor变换

短时傅立叶变换缺点：窗口一旦固定，不能完全表现突变信号与非平稳信号，对于时变的非稳信号，高频适合小窗口，低频适合大窗口  


### 3.小波变换（wavelet transform）  
小波变换将傅立叶变换的三角函数基换成了有限长的会衰减的小波基（Haar小波，db小波，morl小波等），这个基函数会伸缩、会平移，属于时频分析

![wavelet](/assets/article_img/2018-12-19-signalprocessing-3.jpg) 

小波变换有两个变量：尺度a（控制小波伸缩）和平移量 τ（控制小波平移）

小波变换缺点：不能“最优”表示含线或者面奇异的高维函数，但事实上具有线或面奇异的函数在高维空间中非常普遍

### 4.曲波变换（curvelet transform）
曲波变换与小波变换相似，采用基函数与信号的内积实现信号的稀疏表示，可以最优表示高维空间函数

![curvelet](/assets/article_img/2018-12-19-signalprocessing-4.jpg) 

下标j,l,k分别表示尺度、方向和位置向量



### 其他

1.与曲波变换类似的还有脊波Ridgelet、轮廓波Contourlet、条带波Bandelet、楔波Wedgelet、小线Beamlet

2.小波包变换——小波分析是只对低频部分进行分解,分解成低频、高频两部分；小波包分解对低频和高频部分都进行分解

![wavelet packet](/assets/article_img/2018-12-19-signalprocessing-5.jpg) 

3.S变换（Stockwell transform）采用高斯窗函数且窗宽与频率的倒数成正比,它的特别之处在于它既保持与傅里叶变换的直接关系，又可在不同频率有不同的分辨率。
![stockwell](/assets/article_img/2018-12-19-signalprocessing-6.jpg)

4.希尔伯特变换，信号经希尔伯特变换后，在频域各频率分量的幅度保持不变，但相位将出现90°相移
![hilbert](/assets/article_img/2018-12-19-signalprocessing-7.jpg)

5.解析信号（analytic signal），在能量不变的前提下，利用希尔伯特变换构造一个虚部，使之只有正频谱，可以用来估计瞬时频率(瞬时频率为相位的微分)

![analytic](/assets/article_img/2018-12-19-signalprocessing-8.jpg)

***最后是网上看到的一副关系图***  (其中有波原子变换)
![wavebasis](/assets/article_img/2018-12-19-signalprocessing-9.jpg) 