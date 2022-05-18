---
title: "Fourier Transform"
date: 2021-08-14
# weight: 1
# aliases: ["/first"]
tags: ["Signal Processing"]
author: "Orange"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: true

canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
math: true
---
* Cute Fourier Transformation coming !


### Fourier transformation
$X(t)$ is the amplitude-time function, we want to transform this into frequency domain. Typically, we want to decompose the function into several sine and cosine function with different frequency, phase and amplitude.  $F$ represents the frequency we focus on. 

$$X(F) = \int_{-\infty}^{+\infty} X(t) e ^{-i2\pi Ft}dt$$

The dot product verifies the similarity of the analysis function and the amplitude-time function.  

![](//img/post/fft/fft.png)

### Discrete Fourier transformation
When we can only sample data from the signals, we replace the X with the folowwing.

$$X_k = \sum_{n=0}^{N-1} X(t) e ^{-\frac{i2\pi kn}{N}}dt$$

$$F=\frac{k}{n}, t=n$$

Expansion of DFT
Euler's equation

$$e^{ix} = cosx + isinx$$

According to Euler's equation, and regards the $\frac{2 \pi kn}{N}$as $b_n$, we have the following

$$X_k = x0[cos(-b0)+isin(-b0)]+ \dots$$

$$X_k =A_k + B_k i$$

What is A and B w.r.t. k?
![](//img/post/fft/abk.png)
A and B is the amplitude and phase of cosine wave.

### Experiment
Let's take an experiment!

We first generate a sine signal from 0 to 2 second. We sample the signal with frequency 512 Hz. 
```python
# sample frequency is 512 Hz, i.e. sample 512 data per second  
fs = 512  
# time duration 2s  
t = 10  
# number of sample  
N = int(t*fs)  
# sample spacing  
T = 1 / fs  
# generate signals
samples = np.linspace(0,t,N,endpoint=False)  
signals = np.sin(samples) 
```
1. Take Fourier Transformation(fft). It returns an array with A/2 +B/2 * i for each frequency from negative to positive.
	```python
	yf = fft(signals)
	```
2. Take fftfreq to get the frequency bin. It returns an array with positive frequency bin and negative frequency bin.
	```python
	xf = fftfreq(N, T)
	```
3. According to Nyquist limit
	Nyquist limit = $fs/2$, we only take the positive frequency.
	We multiply the value in positive frequency by 2 and take fraction of sample number N to get the true FFT value.
	
	```python
	result = 2.0/N * np.abs(yf[0:N//2])
	```
	
	
The complete code is as follows:

```python
  
from scipy.fftpack import fft, fftfreq  
import numpy as np  
import matplotlib.pyplot as plt  
  
## data generation  
# sample frequency is 512 Hz, i.e. sample 512 data per second  
fs = 512  
# time duration 2s  
t = 10  
# number of sample  
N = int(t*fs)  
# sample spacing  
T = 1 / fs  
# generate signals
samples = np.linspace(0,t,N,endpoint=False)  
signals = np.sin(samples)  
plt.figure()  
plt.plot(samples,signals)  
plt.xlabel("Time(s)")  
plt.ylabel("Amplitude")  
plt.show()  
## fourier transformation  
yf = fft(signals)  
## frequency bin  
"""  
f = [0, 1, ..., n/2-1, -n/2, ..., -1] / (d*n)         if n is even  
f = [0, 1, ..., (n-1)/2, -(n-1)/2, ..., -1] / (d*n)   if n is odd  
"""  
xf = fftfreq(N, T)[:N//2]  
  
# nyquist limit  
nl = fs / 2  

# plot
plt.figure()  
plt.xlabel("Frequency(Hz)")  
plt.ylabel("Amplitude")  
plt.plot(xf,2.0/N * np.abs(yf[0:N//2]))  
plt.show()

```

We could see the result 

![](/img/post/fft/signal.png)
![](/img/post/fft/fftresult.png)


### great reference

[Simon Xu](https://www.youtube.com/watch?v=mkGsMWi_j4Q)

[Wolfram](https://mathworld.wolfram.com/FourierTransform.html)