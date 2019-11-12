---
layout: post
title: Random Walk - Concept to Code, Part 1
subtitle: Start with a simple concept and learn to code it 
gh-repo: probabilityfilter/Learn-Python
gh-badge: [star, fork, follow]
tags: [Python, NumPy]
comments: true
---

![RandomWalk](/img/RandomWalk1/GaltonBoard.jpg "Galton Board"){: .center-block :}  [Code](https://github.com/probabilityfilter/Learn-Python/blob/master/RandomWalker/RandomWalk_1d_multiple%20walkers_histogram.py)
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

To code this, all we got to do is start with the initial number then run a loop and keep adding/subtracting a 1, simple isn't it. And since we said loop, let's use a simple `for loop`
```python
# Random Walk in 1 dimension (no function, no class, no vectorization)
import random

n = 100 # Total number random steps
x = 0 # Starting position
path = [x] # Store all the intermediate steps

for i in range(n):
    x += 2*random.randint(0, 1) - 1 # Little bit of Math trickery to get only +/-1 and ignore 0
    path.append(x) # Store the result of each step

print(path)
```

And the result is:
```python
[0, 1, 0, 1, 0, -1, -2, -3, -2, -3, -4, -3, -2, -1, -2, -3, -2, -1, -2, -3, -2, -1, 0, -1, -2, -1, 0, 1, 0, 1, 2, 1, 2, 3, 4, 3, 4, 3, 4, 3, 2, 1, 2, 1, 2, 3, 4, 5, 4, 3, 2, 1, 2, 1, 2, 1, 0, 1, 2, 3, 4, 3, 2, 3, 2, 1, 2, 3, 4, 5, 4, 5, 4, 3, 4, 5, 6, 7, 8, 7, 8, 9, 10, 9, 10, 9, 10, 11, 12, 11, 12, 11, 12, 11, 12, 11, 10, 9, 10, 9, 10]
```

One thing to clarify right off the bat is that using a for loop is a telltale sign thata newbie is at work. Don't worry, most non-computer science graduates, including me, end up coding everything using a for loop. One of the main reasons against using a for loop is the slower speed of execution, more on that later.

Now imagine we wanted to answer the question of whether our Random Walker typically walks away from the starting position or returns back to it. The only way to answer this question is to run this code multiple times and may be even vary the number of steps taken. Yes, we could place the above code inside another for loop but remember what I said in the previous paragraph! So as a next step in programming like a pro, we shall use the concept of placing a modified version of this code inside a package called definition and using it multiple times.

### Improvement #1: Use numpy's `random.choice`
```python
import numpy as np
print(np.random.choice([-1, +1], (10, 5)))
```

This would produce 5 columns of 10 random +/-1 choices representing 5 Random Walkers taking 10 steps each.... all of this in one shot!
```python
[[ 1  1  1  1 -1]
 [-1  1 -1  1 -1]
 [ 1 -1 -1 -1 -1]
 [-1 -1 -1 -1 -1]
 [-1 -1  1  1 -1]
 [ 1  1 -1 -1 -1]
 [-1 -1  1 -1  1]
 [ 1  1 -1  1 -1]
 [ 1 -1  1  1 -1]
 [ 1  1 -1 -1  1]]
```

### Improvement #2: Use numpy's `cumsum` to cumulatively add the random steps
```python
import numpy as np
steps = np.random.choice([-1, +1], (5, 3))
print("steps =\n", steps)
print("path =\n", np.cumsum(steps, axis=0)) # Add along the column
```

Just to simplify, I have shown 3 Random Walkers taking 5 steps each:
```python
steps =
 [[-1 -1  1]
 [-1 -1  1]
 [-1  1  1]
 [-1  1  1]
 [ 1 -1 -1]]
path =
 [[-1 -1  1]
 [-2 -2  2]
 [-3 -1  3]
 [-4  0  4]
 [-3 -1  3]]
```

### Improvement #3: Use `functions`
For `functions` go to the next post: [Random Walk - Concept to Code, Part 2](https://probabilityfilter.github.io/2018-05-05-RandomWalk2/)
