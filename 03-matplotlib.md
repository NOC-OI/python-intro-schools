---
title: Visualizing Argo Data
teaching: 15
exercises: 15
---

::::::::::::::::::::::::::::::::::::::::::  questions

- "How can I visualize tabular data in Python?"
- "How can I group several plots together?"

::::::::::::::::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::::::::::  objectives

- "Plot simple graphs from data."
- "Plot multiple graphs in a single figure."
- "Use Argopy's plotting functions."

::::::::::::::::::::::::::::::::::::::::::::::::::

## Visualizing data
The mathematician Richard Hamming once said, "The purpose of computing is insight, not numbers,"
and the best way to develop insight is often to visualize data.  Visualization deserves an entire
lecture of its own, but we can explore a few features of Python's `matplotlib` library here.  While
there is no official plotting library, `matplotlib` is the _de facto_ standard.  First, we will
import the `pyplot` module from `matplotlib` and use two of its functions to create and display a
line graph of our data:



## Ensuring we have Loaded the Data

Let's load some temperature, pressure and salinity data with Argopy.

```python
import argopy
argo_data = argopy.DataFetcher().profile(6902746, 12).to_xarray()
temperature = argo_data.TEMP.values
pressure = argo_data.PRES.values
salinity = argo_data.PSAL.values
```



## Graphing Temperature Data

Let's use the Matplotlib library to plot this data. We'll need to import from the `matplotlib.pyplot` library. We can then use pyplot's `plot` function to plot the temperature data.

```python
import matplotlib.pyplot
image = matplotlib.pyplot.plot(temperature)
```


![](fig/temperature_plot.png){alt="A line graph representing the temperature readings from the Argo float data."}

The X axis corresponds to each row in the data and the Y axis is temperature in degrees celcius. 

## Graphing Salinity Data

Now let's take a look at the pressure and salinity during our Argo float's dive. 

```python
salinity_plot = matplotlib.pyplot.plot(salinity)
```

![](fig/salinity_plot.png){alt="A line graph showing the salinity readings from the Argo float data."}

### Adding Labels to a Graph

It's good practice to add axes labels to our graphs, these can be done with the `xlabel` and `ylabel` functions in `matplolib.pyplot`.

```python
matplotlib.pyplot.ylabel("Temperature (Degrees C)")
matplotlib.pyplot.xlabel("Reading Number")
temperature_plot = matplotlib.pyplot.plot(temperature)
```


![](fig/temperature_plot_with_labels.png){alt="A line graph showing the temperatuer from the Argo data with axes labels."}


::::::::::::::::::::::::::::::::::::::::::  callout

## Importing libraries with shortcuts

So far we use have used the code `import matplotlib.pyplot`
[syntax](learners/reference.md#syntax)
to import the `pyplot` module of `matplotlib`. An alternative method for importing is to use
`import matplotlib.pyplot as plt`.
Importing `pyplot` this way means that after the initial import, rather than writing
`matplotlib.pyplot.plot(...)`, you can now write `plt.plot(...)`.
Another common convention is to use the shortcut `import numpy as np` when importing the
NumPy library. We then can write `np.loadtxt(...)` instead of `numpy.loadtxt(...)`,
for example.

Some people prefer these shortcuts as it is quicker to type and results in shorter
lines of code - especially for libraries with long names! You will frequently see
Python code online using a `pyplot` function with `plt`, or a NumPy function with
`np`, and it's because they've used this shortcut. It makes no difference which
approach you choose to take, but you must be consistent as if you use
`import matplotlib.pyplot as plt` then `matplotlib.pyplot.plot(...)` will not work, and
you must use `plt.plot(...)` instead. Because of this, when working with other people it
is important you agree on how libraries are imported. From this point onwards this lesson uses
`plt` to mean `matplotlib.pyplot`.

::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::  challenge

## Plot the pressure data

Create a plot showing the pressure (depth) across a Argo profile.


:::::::::::::::  solution
```python
import matplotlib.pyplot as plt
plt.xlabel("Reading number")
plt.ylabel("Depth (metres)")
pres_plot = plt.plot(pressure)
```
:::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::


### Saving Plots
We can call the `savefig` function to store the plot as a graphics file. This can be
a convenient way to store your plots for use in other documents, web
pages etc. The graphics format is automatically determined by
Matplotlib from the file name ending we specify; here PNG from
'argo6902746-profile12-temperature.png'. Matplotlib supports many different graphics
formats, including SVG, PDF, and JPEG.

```python
matplotlib.pyplot.ylabel("Temperature (Degrees C)")
matplotlib.pyplot.xlabel("Reading Number")
temperature_plot = matplotlib.pyplot.plot(temperature)
temperature_plot.savefig("argo6902746-profile12-temperature.png")
```

![](fig/argo6902746-profile12.png){alt="Three line graphs showing the temperature, salinity and presssure."}

## Plot using Argopy

Instead of calling functions in Matplotlib we can also call some plotting functions within Argopy (and these will call Matplotlib for us). 
This offers two advantages:

1. we don't need to import matplolib ourselves.
2. there are some Argo specific plots available within Argopy.

### Plotting a Map of Where our Float has Travelled

One of the plots that Argopy can generate is a map showing the position of the float every time it surfaced. 

```python
float_data = argopy.DataFetcher().float(6902746).load()
argopy.plot.scatter_map(float_data.index, set_global=False)
```

![](fig/scatter_map.png){alt="A scatter graph comparing temperature and presssure."}

You can also see the same data on an interactive map at https://fleetmonitoring.euro-argo.eu/float/6902746. For some reason the data returned by ArgoPy for this float is limted to the first 118 profiles
and there are a few more after that being shown on the fleetmonitoring website. 

### Plotting Temperature Across Multiple Profiles

Another useful feature of the Argopy library is that it can plot data from multiple Argo profiles (dives). 
This can be done by supplying a whole Xarray dataset for all our profiles, we can extract this from
the `float_dat` object we got earlier by calling the `to_xarray()` function on it. This can be passed
to the `scatter_plot` function in Argopy, we also have to give it the variable name which is "TEMP" (or PSAL for salinity).
This plot uses colour to show the temperature and puts depth/pressure on the y axis and date on the x axis. 

```python
fig = argopy.plot.scatter_plot(float_data.to_xarray(), 'TEMP')
```
![](fig/temperature_multi_profile.png){alt="A scatter graph from Argopy showing temperature, depth and time."}


:::::::::::::::::::::::::::::::::::::::  challenge

## Find Another Float to Plot

Pick a different float to load some data from. You can find a list of recently launched UK floats at
https://fleetmonitoring.euro-argo.eu/dashboard?Status=Active&Year%20of%20deployment=2025&Country=United%20Kingdom&Network=CORE

Float numbers 7902230, 1902114, 1902725, 1902724, 1902109, 1902111, 1902110, 1902112, 4903834, 4903656, 6990513 or 2903943 could all be good contenders.
Some floats will not work because they are missing data and you will ValueError, if this happens try a different float. 

Create a new notebook with the following graphs for you float:

* A map showing where it has been
* A scatter plot of temperature against depth over time
* A scatter plot of salinity against depth over time

If you have time add some description about each graph by creating a cell with the Markdown type.
Look at https://www.markdownguide.org/basic-syntax/ to see some of the syntax you can use with markdown.

:::::::::::::::  solution
```python
import argopy
float_data = argopy.DataFetcher().float(7902230).load()
argopy.plot.scatter_map(float_data.index, set_global=False)
fig = argopy.plot.scatter_plot(float_data.to_xarray(), 'TEMP')
fig = argopy.plot.scatter_plot(float_data.to_xarray(), 'PSAL')
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::::::::::::  keypoints

- "Use the `pyplot` module from the `matplotlib` library for creating simple visualisations."
- "We can give imported modules a short name by using the `as` keyword after the import."
- "Argopy has its own built in visaulisation functions"

::::::::::::::::::::::::::::::::::::::::::::::::::
