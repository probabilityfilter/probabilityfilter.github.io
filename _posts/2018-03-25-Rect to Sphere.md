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

This will be a two step process where the first step is to convert the x-y data that is in 2D to 3D co-ordinates as if we were to take a sheet of paper and warp it around a sphere. This will need some high school level trignometry as shown below, to adapt the formulae to our case either use:  
RA = 90$$^o$$ - $$\varphi$$  
RA = 90$$^{o}$$ - $$\varphi$$  
Dec = 90 - $$\theta$$  
or just swap the **sin** and **cos** operations.  
![Trignometry](/img/RectToSphere/Trignometry.png "Trignometry"){: .center-block :}  

The spherical grid as shown earlier can be drawn by using the code below which uses some more trignometry:
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
  
Combining the 3D representation of data and the spherical grid will produce this beautiful plot:
![Spherical](/img/RectToSphere/Spherical coordinates.JPG "Random Data"){: .center-block :}   

One thing to note here - notice the bunching up of points on the north and south pole?!

