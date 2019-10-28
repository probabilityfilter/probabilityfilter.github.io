---
layout: post
title: Machine Learning Code Challenge by SETI and IBM
subtitle: Prototyping to Implementation 
gh-repo: probabilityfilter
gh-badge: [star, fork, follow]
tags: [Machine Learning, Data Analysis, Jupyter Notebooks, Python, NumPy, astronomy]
comments: true
---

## Code Challenge

Can you spot a signal? may be a line, a dashed line, something? anything! Read on......  
![Signal](/img/SETI Code Challenge/Is there a signal.jpg "May be just noise?!?"){: .center-block :} 

The [Hackathon](https://probabilityfilter.github.io/2017-07-20-SETI-IBM-Hackathon/) was followed by 4 weeks of Code Challenge. A new and expanded dataset was released. Here is how the progression looked:
- Primary Small Dataset
  - To be used for early-stage prototyping, ~2 GB in total
  - Signals form all 7 classifications: 1,000 simulations/class

- Primary Medium Dataset
  - To be used for relatively robust model construction, ~10 GB in total
  - Signals from all 7 classifications: 5,000 simulations/class

- Primary Full Dataset
  - Enormous training data set, ~50 GB in total
  - Signals from all 7 classifications: 20,000 simulations/class

The Code Challenge was a whole different animal since we had to deal with a low SNR and the number of signal classes went up from 4 to 7. My Hackathon methods, more like tricks, could not rescue me!! Many of the signals were invisible to the eye, extreme data processing was required to start seeing these signals. [Code](https://github.com/probabilityfilter/ML-SETI-IBM/blob/master/notebooks/ArunBasic_DSP_try.ipynb).

Here is one signal; top figure - hard to discern the signal, middle figure - better after FFT and removing color, last figure - actual signal  
![Compare](/img/SETI Code Challenge/Compare.jpg "Barely visible"){: .center-block :}  

Here is a challenging one; top figure - impossible to see the signal, bottom figure - slight improvement after FFT cleanup  
![Compares](/img/SETI Code Challenge/Compare2.jpg "Impossible to discern"){: .center-block :}  

I had to resort to some creative visualizations but the low SNR and higher number of classes proved to be a challenge. Here are some artistic results, each color represents a type of signal: [Code](https://github.com/probabilityfilter/ML-SETI-IBM/blob/master/notebooks/Arun_nonNN%2BPrimary_testset_preview.ipynb).
![DSP1](/img/SETI Code Challenge/PSmall_MenMedianRatio.JPG "Fountain :-)"){: .center-block :}  
![DSP2](/img/SETI Code Challenge/PSmall_pVal.JPG "Not very helpful"){: .center-block :}  
![DSP3](/img/SETI Code Challenge/PSmall_pVal_slopeLinearFit.JPG "Buttetfly from top"){: .center-block :}  
![DSP4](/img/SETI Code Challenge/PSmall_StdDevTime.JPG "Taking off"){: .center-block :}  

## Future Work

The Code Challenge that followed the Hackathon focused on bringing the powers of Supervised Learning to the task of classifying the signals into seven categories. Although the [winning team](https://arxiv.org/abs/1803.08624?context=astro-ph.IM) attained a [95% signal classification accuracy](https://github.com/setiQuest/ML4SETI/blob/master/results/effsubsee_seti_code_challenge_1stPlace.ipynb) using Wide Residual Networks, the Universe does not limit itself to just seven categories. Hence, I firmly believe that this is an appropriate problem for Unsupervised Learning algorithms which could detect previously unseen yet interesting signals.

Here's yours truly giving a [brief explanation of the feature extraction work](https://youtu.be/Yn2SBPs5-88?t=1822)
![Presenting](/img/SETI Code Challenge/Presenting.JPG "Feature Extraction"){: .center-block :}
