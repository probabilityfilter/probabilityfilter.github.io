---
layout: post
title: Random Walk - Concept to Code
subtitle: Use a simple concept and learn to code it 
gh-repo: probabilityfilter/Learn-Python
gh-badge: [star, fork, follow]
tags: [Python, NumPy]
comments: true
---

![RandomWalk](/img/RandomWalk/GaltonBoard.jpg "Galton Board"){: .center-block :}  
In this post I will take a simple algorithm from its concept all the way to code, in essence learn to convert Maths into code. I feel coding a mathematical concept gives a deeper understanding of the underlying dynamics and allows for some fun experimentation while yielding some cool pictures. So let us start with Random Walk.

The premise is that you start with a number on a number line, in the simple case a 0, then randomly pick either a 1 or a -1, say by tossing a coin. If you get a +1 then you take one step to the right, aka the positive side, whereas if you get a -1 then take one step to the left, the negative side. Now repeat the process of choosing 1 or -1, and subsequent moving, from this new position and keep repeating this multiple times. Simple enough?!

Before we can code this process it will be beneficial to convert this into Maths so that we are clear about the underlying process. So let's say the initial position is:

$$ \begin{align*} x_{0} \end{align*} $$

Toss a coin and choose to move left or right, the new position will be:

$$ \begin{align*} x_{0} \pm 1 \end{align*} $$

If we keep this going then we will get something like this:  
$$ \begin{align*} x_{0} \pm 1 \pm 1 \pm 1 \pm 1 \pm 1 \pm \dotsc \end{align*} $$

The sum of the above series will yield the final position of the Random Walk process. This can be interpreted as initial position plus a series of random choices between +1 and -1, thus we could rewrite the sum as:

$$ \begin{align*} x_{0} + x_{1} + x_{2} \dotsc \end{align*} $$

where the likes of $$x_{1}$$ and $$x_{2}$$ are results of random choices between +1 and -1.

One can agree that even though this series represents what we want to depict but it is inconvenient to write this expanded series all the time and what if we need to write many such series in a single formula!? So the mathematicians have come up with a shortened version which is written as:  
$$ \begin{align*} \displaystyle\sum_{i=0}^{n} x_{i} \end{align*} $$

So all we got to code is start with the initial number then run a loop and keep adding/subtracting a 1, simple isn't it. And since we said loop, let's use a simple **for loop**
```python
# Random Walk in 1 dimension (no function, no class, no vectorization)
import random

n = 100 # Total number random steps
x = 0 # Starting position
path = [] # Store all the intermediate steps

for i in range(n):
    x += 2*random.randint(0, 1) - 1 # Slight trickery to get only +/-1 and ignore 0
    path.append(x) # Store the result of each step

print(path)
```

And the result is:
```python
[1, 0, 1, 0, -1, -2, -3, -2, -3, -4, -3, -2, -1, -2, -3, -2, -1, -2, -3, -2, -1, 0, -1, -2, -1, 0, 1, 0, 1, 2, 1, 2, 3, 4, 3, 4, 3, 4, 3, 2, 1, 2, 1, 2, 3, 4, 5, 4, 3, 2, 1, 2, 1, 2, 1, 0, 1, 2, 3, 4, 3, 2, 3, 2, 1, 2, 3, 4, 5, 4, 5, 4, 3, 4, 5, 6, 7, 8, 7, 8, 9, 10, 9, 10, 9, 10, 11, 12, 11, 12, 11, 12, 11, 12, 11, 10, 9, 10, 9, 10]
```

to codeHere is one element of a receiver/feed which is the essence of a radio telescope. The varying size of the spikes allow the radio telescopes at the Allen Telescope Array to capture different wavelengths of radio waves ...... who knows at what frequency the aliens are transmitting!  

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
