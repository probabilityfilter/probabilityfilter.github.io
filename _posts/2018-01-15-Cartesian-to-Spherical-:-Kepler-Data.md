---
layout: post
title: Kepler Exoplanet Data - Cartesian to Spherical Projection
subtitle: Convert star locations from a rectangle to a sphere and make it spin! 
gh-repo: probabilityfilter
gh-badge: [star, fork, follow]
tags: [Data Visualization, Jupyter Notebooks, Python, NumPy, astronomy]
comments: true
---

![gif](/img/Cartesian to Spherical/CandidatesInSky_Fast.gif "Oh look its spinning"){: .center-block :}  

This is where my inner geek took over the steering wheel. What if I could map a flat Cartesian co-ordinate system onto a Spherical co-ordinate system!?! As a warm up SETI had given the participants an introductory dataset which contained the location of all the target stars that the [Allen Telescope Array](https://www.seti.org/seti-institute/project/details/fact-sheet) (radio telescope array) had aimed at to collect signals originating from possible extraterrestrial sources. Star locations are given in RA (right ascension) and Dec (declination) that correspond to longitude and latitude on Earth. RA is location along the East/West and is measured in hours minutes and seconds of time so it goes from 0 to 24. Dec is location along the up and down direction and is measured in degrees so it goes from -90 to +90. There was no need for anyone to plot the distribution of the target star systems but curiosity got the better of me. Once I was done, I realized that a good visualization enables the viewer to gain a deeper understanding of the data.

This is how the star locations looked like in the Cartesian co-ordinate system:
![Flat](/img/Cartesian to Spherical/Density plot of Candidates.JPG "This is so flat"){: .center-block :} 

## Star Locations
To achieve this visualization I took the Dec and RA system, which are the x-y co-ordinates ([code](https://github.com/probabilityfilter/ML-SETI-IBM/blob/master/notebooks/CandidateLocation_BySize.ipynb)), used NumPy and my mathematical skills to map this Cartesian system onto a Spherical co-ordinate and represented the target stars on a celestial sphere. The magnanimity of SETI's undertaking was so utterly impressive that this result appeared in an article by IBM and IBM Watson Data Lab [tweeted](https://twitter.com/WatsonDataLab/status/864494962280460288) about it ([code](https://github.com/probabilityfilter/ML-SETI-IBM/blob/master/notebooks/RA_Dec_to_SphericalSystem.ipynb)). 

As a bonus material, I isolated the Kepler Field which clearly shows the '+' like pattern of the search field. The Kepler mission completely changed our understanding of the Universe and had a direct impact on SETI by bounding the 'Fraction of stars with planets' parameter in the Drake equation.

![Kepler](/img/Cartesian to Spherical/KeplerField.JPG "The ever beautiful Kepler Field"){: .center-block :}  

And here is my [Ode to the Kepler mission](https://twitter.com/click_arun/status/1016406934302257152)
