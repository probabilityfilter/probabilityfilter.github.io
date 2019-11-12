---
layout: post
title: Random Walk - Concept to Code, Part 2
subtitle: Start with a simple concept and learn to code it 
gh-repo: probabilityfilter/Learn-Python
gh-badge: [star, fork, follow]
tags: [Python, NumPy]
comments: true
---

![RandomWalk](/img/RandomWalk1/RandomWalker1D.jpg "Multiple Random Walks"){: .center-block :}  
Continuing from the previous post [Random Walk - Concept to Code: Part 1](https://probabilityfilter.github.io/2018-04-28-RandomWalk1/)
### Improvement #3: Use `functions`
While learning a new concept its useful to ignore the fancy syntax and keywords and focus on the core feature that we are trying to implement. In this case the goal is to package our previous code such that instead of re-writing it we just give it a name and call it whenever we need the functionality. So in our case whenever we need a Random Walk to be calculated we will call the `function`. But once we call it to do a job we also need to give it some details for it to be useful to us, example values can be how many steps do you want the Random Walker to take, the starting value etc. Hence while creating the `function` we also provide few variables that the `function` will need to do its thing. Here is an [example](https://github.com/probabilityfilter/Learn-Python/blob/master/RandomWalker/RandomWalk_1d_multiple%20walkers.py):

```python
# Defining a function and the variables it needs to carry out its task
def random_walk_1d(steps, walkers):
    steps = np.random.choice([-1, +1], (steps, walkers))  # Each column is an independent Walker
    return np.cumsum(steps, axis=0)
```
See the [previous post](https://probabilityfilter.github.io/2018-04-28-RandomWalk1/) for `random.choice` and `cumsum`
Once this `function` named **random_walk_1d** has been created, it can be called any number of times from any part of the code to deliver the path taken by a Random Walker as long as we provide it with two pieces of information: number of steps the Random Walker needs to take and the number of Walkers participitating. Here is a [slightly different example](https://github.com/probabilityfilter/Learn-Python/blob/master/RandomWalker/RandomWalk_1d.py), spot the difference:

```python
import numpy as np
import matplotlib.pyplot as plt

def random_walk_1d(n):
    steps = np.random.choice([-1, +1], n)  # randomly select either left or right
    return np.cumsum(steps)

plt.subplot(2,2,1)
plt.plot(random_walk_1d(100))
plt.title('100 steps')
plt.xticks([])

plt.subplot(2,2,2)
plt.plot(random_walk_1d(1000))
plt.title('1000 steps')
plt.xticks([])

plt.subplot(2,2,3)
plt.plot(random_walk_1d(100000))
plt.title('100,000 steps')
plt.xticks([])

plt.subplot(2,2,4)
plt.plot(random_walk_1d(10000000))
plt.title('10,000,000 steps')
plt.xticks([])

plt.tight_layout()
plt.suptitle('Random Walk in 1D')
plt.show()
```

Now we are in a position to answer the question: how likely is it for the Random Walker to walk away from the starting position or return back to starting position? Best way to investigate it is to compute a large number of Random Walkers taking numerous steps and plotting a Histogram of the distribution. See the previous post for the result of simulating 10,000 Random Walkers each taking 1000 steps. To me this explains the [Galton Board](https://en.wikipedia.org/wiki/Bean_machine) behaviour where each peg is a random number generator pushing the ball either left or right, and when hundereds of balls are dropped most of then end up getting close to the starting position but there are few that meander far, never to return :worried:
![GaltonBoard](/img/RandomWalk1/GB.mp4 "Galton Board in Action"){: .center-block :}
