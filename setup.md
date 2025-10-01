---
title: Setup
---

## Setup

This lesson is designed to be run on a computer with Python and the Matplotlib, Numpy and Argopy libraries installed.
We expect most learners to use a pre-configured environment for this and not to install it themselves. 

A pre-configured MyBinder image is available which will provide all the required software. If you have not been provided 
with any other system then use this. Click on the "Run this lesson on MyBinder" icon below.

[![Run this lesson on MyBinder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/NOC-OI/python-intro-schools/binder)


## Argo floats

This lesson is intended for people with an interest in oceanography and uses some example data from an Argo float.
Argo floats are small drifting floats that spend most of their time moving up and down between the surface and mid level water (usally one or two thousand metres).
The control their buoyancy by inflating and deflating a small bladder which causes them to sink or float. 
They usually measure the water temperature, conductivity (which tells us how salty it is) and pressure (which tells us how deep they are). 
Some of them also measure biochemical information such as acidity, the amount of chlorophyll or dissolved oxygen. An Argo float usually spends 10 days under the 
water gathering data, it then surfaces and transmits back the information it has gathered to a satellite. Once it has transmitted its data it will dive again
and repeat the process. Each dive generates one "profile" of data showing the temperature and salinity of the ocean at each depth level.

Thousands of Argo floats have been deployed since 1999 and they are spread all over the oceans. Many countries operate Argo floats but they all report their data
in a commonly agreed upon format and the data is archived at a series of regional Data Assembly Centres or DACS. These DACS then pass on the data to two Global Data Assembly Centres
(GDACs), one in the USA and one in France. Anybody can access data from the GDACs and use it in their work. It is quite common for oceanographers to use the data from 
many Argo floats to look at changes in the ocean temperature and salinity. 

