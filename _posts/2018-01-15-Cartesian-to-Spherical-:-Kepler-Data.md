---
layout: post
title: Kepler Exoplanet Data - Cartesian to Spherical Projection
subtitle: Convert star locations from a rectangle to a sphere and make it spin! 
gh-repo: probabilityfilter
gh-badge: [star, fork, follow]
tags: [Data Visualization, Jupyter Notebooks, Python, NumPy, astronomy]
comments: true
---

## Star Locations

![gif](img/Cartesian to Spherical/CandidatesInSky_Fast.gif?raw=true)  

This is where my inner geek took over the steering wheel! As a warm up SETI had given the participants an introductory dataset. Among other things the dataset contained the location of all the target stars that the [Allen Telescope Array](https://www.seti.org/seti-institute/project/details/fact-sheet) (radio telescope array) had pointed to collect signals originating from possible extraterrestrial sources. There was no need for anyone to plot the distribution of the target star systems but curiosity got the better of me. Once I was done, I realized that a good visualization enables the viewer to gain a deeper understanding of the data.

To achive this visualizatio I took the Dec and RA system, which are the x-y cor-ordinates ([code](https://github.com/probabilityfilter/ML-SETI-IBM/blob/master/notebooks/CandidateLocation_BySize.ipynb)), used NumPy and my mathematical skills to map this Cartesian system onto a Spherical co-ordinate and represented the target stars on a celestial sphere. The magnanimity of SETI's undertaking was so utterly impressive that this result appeared in an article by IBM and IBM Watson Data Lab [tweeted](https://twitter.com/WatsonDataLab/status/864494962280460288)about it ([code](https://github.com/probabilityfilter/ML-SETI-IBM/blob/master/notebooks/RA_Dec_to_SphericalSystem.ipynb)). 

As a bonus material, I isolated the Kepler Field which clearly shows the '+' like pattern of the search field. The Kepler mission completely changed our understanding of the Universe and had a direct impact on SETI by bounding the 'Fraction of stars with planets' parameter in the Drake equation.

![Kepler](/img/Cartesian to Spherical/KeplerField.JPG)
