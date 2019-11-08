---
layout: post
title: How to convert a Cartesian plot into a Spherical plot
subtitle: Fun with trignometry 
gh-repo: probabilityfilter/Learn-Python
gh-badge: [star, fork, follow]
tags: [Data Visualization, Python, NumPy, Matplotlib]
comments: true
---

![Cartesian](/img/RectToSphere/Cartesian coordinates.JPG "Random Data"){: .center-block :}  
This post will delve into the details of how the rotating celestial sphere was created in the [previous post](https://probabilityfilter.github.io/2018-01-15-Cartesian-to-Spherical-Kepler-Data/). The challenge is to map the above distribution (random data) on to the spherical grid as shown below.
![SphericalGrid](/img/RectToSphere/Spherical grid.JPG "Random Data"){: .center-block :}  

This will be a two step process where the first step is to convert the x-y data that is in 2D to 3D co-ordinates as if we were to take a sheet of paper and warp it around a sphere. This will need some high school level trignometry as shown below:
![Trignometry](/img/RectToSphere/Trignometry.png "Trignometry"){: .center-block :}  

Now it is time to draw the spherical grid (as shown above) using more trignometry using the code below.
<code>

~~~
# Wireframe of Sky (sphere)
fig = plt.figure(figsize=(5, 5))
ax = fig.add_subplot(111, projection="3d")
# Wireframe of Sphere
u = np.linspace(0, 2 * np.pi, 100)
v = np.linspace(0, np.pi, 100)
x = 1 * np.outer(np.cos(u), np.sin(v))
y = 1 * np.outer(np.sin(u), np.sin(v))
z = 1 * np.outer(np.ones(np.size(u)), np.cos(v))
# Overlaying Wireframe of Sky over Candidate data
ax.plot_wireframe(x, y, z, rstride=10, cstride=10, color="b", alpha=0.1)
~~~

```
# Wireframe of Sky (sphere)
fig = plt.figure(figsize=(5, 5))
ax = fig.add_subplot(111, projection="3d")
# Wireframe of Sphere
u = np.linspace(0, 2 * np.pi, 100)
v = np.linspace(0, np.pi, 100)
x = 1 * np.outer(np.cos(u), np.sin(v))
y = 1 * np.outer(np.sin(u), np.sin(v))
z = 1 * np.outer(np.ones(np.size(u)), np.cos(v))
# Overlaying Wireframe of Sky over Candidate data
ax.plot_wireframe(x, y, z, rstride=10, cstride=10, color="b", alpha=0.1)
```
  
```javascript
# Wireframe of Sky (sphere)
fig = plt.figure(figsize=(5, 5))
ax = fig.add_subplot(111, projection="3d")
# Wireframe of Sphere
u = np.linspace(0, 2 * np.pi, 100)
v = np.linspace(0, np.pi, 100)
x = 1 * np.outer(np.cos(u), np.sin(v))
y = 1 * np.outer(np.sin(u), np.sin(v))
z = 1 * np.outer(np.ones(np.size(u)), np.cos(v))
# Overlaying Wireframe of Sky over Candidate data
ax.plot_wireframe(x, y, z, rstride=10, cstride=10, color="b", alpha=0.1)
```
```python
# Wireframe of Sky (sphere)
fig = plt.figure(figsize=(5, 5))
ax = fig.add_subplot(111, projection="3d")
# Wireframe of Sphere
u = np.linspace(0, 2 * np.pi, 100)
v = np.linspace(0, np.pi, 100)
x = 1 * np.outer(np.cos(u), np.sin(v))
y = 1 * np.outer(np.sin(u), np.sin(v))
z = 1 * np.outer(np.ones(np.size(u)), np.cos(v))
# Overlaying Wireframe of Sky over Candidate data
ax.plot_wireframe(x, y, z, rstride=10, cstride=10, color="b", alpha=0.1)
```
  
Combining the 3D representation of data and the spherical grid will in this beautiful plot:
![Spherical](/img/RectToSphere/Spherical coordinates.JPG "Random Data"){: .center-block :}   

One thing to note here - notice the bunching up of points on the north and south pole?!




Here is one element of a receiver/feed which is the essence of a radio telescope. The varying size of the spikes allow the radio telescopes at the Allen Telescope Array to capture different wavelengths of radio waves ...... who knows at what frequency the aliens are transmitting!  

[SETI (Search for Extraterrestrial Intelligence)](https://www.seti.org/) Institute is dedicated to answering one of the most endearing questions – is there intelligent life elsewhere in the universe? To this end it runs the [Allen Telescope Array](https://www.seti.org/seti-institute/project/details/fact-sheet), a radio telescope array in Hat Creek Radio Observatory, northern California, which observes radio signals from distant stars and nebulae. This is a report of my efforts to participate in this cosmic pursuit.

![ata](https://upload.wikimedia.org/wikipedia/commons/0/0c/C_G-K_-_DSC_0421.jpg "Radio Telescope"){: .center-block :}  

ATA's existing detection software does a simple real-time search for signals. If the signal persists for more than a few seconds then the software flags the observation and calls for human intervention. Needless to say, this is a very broad classification and catches all types of signals with no regard to their periodicity, uniqueness, or shape. IBM partnered with SETI and challenged citizen scientists to use the tools of Machine Learning to classify the radio signals. IBM provided tools like Bluemix, Data Science Experience, Apache Spark Enterprise cluster, and simulated data. A Slack channel was opened for discussions and collaboration.

While the application of Machine Learning to SETI’s radio telescope data will serve to answer the ultimate question, it will also help development of better tools to probe numerous astronomical phenomenon like galaxy evolution, identify planetary systems, detect and characterize solar flares etc. Lessons learned from this analysis will be transferable to other fields like medical diagnosis, which shares lots of traits with astronomical data in terms of confounding of signals and no clear demarcation between different types of signals.

Even though Machine Learning garners the highest appeal, I realize that there will be significant amount of ancillary work to be done, ex. setting up a data pipeline, choosing the right metric, testing etc.

Many thanks to the wonderful people from IBM and SETI who gave me this opportunity ........ and yes that is the legendary Jill Tarter. Her astronomical work is the source for Carl Sagan's novel Contact which was adapted into the film ['Contact'](https://en.wikipedia.org/wiki/Contact_(1997_American_film)) played by Jodie Foster.

![people](/img/SETI using ML/people.jpg "Highlight of my day"){: .center-block :}  

## Digital Signal Processing
Any data collected in the real world will have noise. One of the first steps was to deal with the SNR (Signal to Noise Ratio) and extra relevant data so that our Machine Learning algorithm can do a better job at classifying the signals. Here are four types of radio signals that have been extracted from noisy data. This simplified image will enhance the speed and accuracy of the Machine Learning algorithm downstream in the data pipeline. [Code](https://github.com/probabilityfilter/ML-SETI-IBM/blob/master/notebooks/ArunPrimary_testset_preview_DSP.ipynb).
![Signals](/img/SETI using ML/BasicData_4types.JPG "4 types of signals"){: .center-block :}  

## Hackathon
The Hackathon was held in San Francisco, CA. The above Signal Processing allowed my team to plot the data in such a way that the clusters were clearly visible. As seen in the Leader Board my team 'Benders' won the Signal Processing Contest part of the Hackathon. Brownie points to anyone who can guess the pop culture reference of the team's name. [Code](https://github.com/probabilityfilter/ML-SETI-IBM/blob/master/notebooks/Arun_nonNN%2BHakcathonBasic.ipynb).

![Scatter](/img/SETI using ML/BasicData_clusters.JPG "4 clear clusters"){: .center-block :}  
![LeaderBoard](/img/SETI using ML/LeaderBoard_SignalProcessingContest.jpg "woohoo..... we are winning"){: .center-block :}  

Next step: [Code Challenge](https://probabilityfilter.github.io/2017-09-10-SETI-IBM-CodeChallenge/)

A proud moment for me :smile:
![Award](/img/SETI using ML/award_win.jpg "3 sleepless nights but grinning"){: .center-block :}

Here is our team being [interviewed](https://youtu.be/yYk4eNAVR1k?t=1197).
![Team](/img/SETI using ML/Team.JPG "Woohoo"){: .center-block :}  
