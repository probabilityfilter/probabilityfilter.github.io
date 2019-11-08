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

If you are in a hurry then go [see the code here](https://github.com/probabilityfilter/Learn-Python/blob/master/RectToSphere/RectToSphere.py) or else read along ....  
This will be a two step process where the first step is to convert the x-y data that is in 2D to 3D co-ordinates as if we were to take a sheet of paper and warp it around a sphere. This will need some high school level trigonometry as shown below, to adapt the formulae to our case either use:  
RA = 90$$^o$$ - $$\varphi$$  
Dec = 90$$^o$$ - $$\theta$$  
or just swap the **sin** and **cos** operations.  
![Trignometry](/img/RectToSphere/Trignometry.png "Trignometry"){: .center-block :}  
```python
# Compute spherical co-ordinates
k = 1  # Arbitrary radius
# Initialize arrays
ra = np.linspace(0, 1, N, dtype=float)  # RA: Right Ascension
dec = np.linspace(0, 1, N, dtype=float)  # Dec: Declination
t = np.linspace(0, 1, N, dtype=float)
x3d = np.linspace(0, 1, N, dtype=float)
y3d = np.linspace(0, 1, N, dtype=float)
z3d = np.linspace(0, 1, N, dtype=float)

# Convert RA's HH:MM:SS to Radians and Dec's degrees to Radians
ra = np.multiply(xScaledValues, 2 * np.pi / 24)
dec = np.multiply(yScaledValues, 2 * np.pi / 360)

# Calculate projections of vector on x,y,z axis
t = np.multiply(k, np.cos(dec))  # Projection of unit vector k on x-y plane
x3d = np.multiply(t, np.cos(ra))  # Projection of t on x-axis
y3d = np.multiply(k, np.sin(dec))  # Projection of unit vector k on y-axis
z3d = np.multiply(t, np.sin(ra))  # Projection of t on z-axis
```

The spherical grid shown earlier can be drawn by using the code below which uses some more trigonometry:
```python
# Wireframe of Sky (sphere)
fig = plt.figure(figsize=(5, 5))
ax = fig.add_subplot(111, projection="3d")

u = np.linspace(0, 2 * np.pi, 100)
v = np.linspace(0, np.pi, 100)
x = 1 * np.outer(np.cos(u), np.sin(v))
y = 1 * np.outer(np.sin(u), np.sin(v))
z = 1 * np.outer(np.ones(np.size(u)), np.cos(v))

# Overlaying Wireframe of Sky over Candidate data
ax.plot_wireframe(x, y, z, rstride=10, cstride=10, color="b", alpha=0.1)
```
  
Combining the 3D representation of data and the spherical grid will produce this beautiful plot:
![Spherical](/img/RectToSphere/Spherical coordinates.JPG "Random Data"){: .center-block :}   

One thing to note here, notice the bunching up of points on the North and South pole?! That is the opposite of the [Mercator Projection](https://en.wikipedia.org/wiki/Mercator_projection). In other words the data points close to the top and bottom of a Cartesian co-ordinate system will have less space to occupy when projected on to a sphere since the circumference of rings gets smaller as one approaches the poles! Neat :smile:
![BunchingOfPoints](/img/RectToSphere/BunchingUp.jpg "anti-Mercaptor Projection Effect"){: .center-block :} 

