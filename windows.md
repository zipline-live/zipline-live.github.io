---
title: zipline-live
description: On premise live trading with zipline
---
# zipline-live installaion on Windows

This tutorial assumes you have a clean Windows installation with Administrator rights. This tutorial has been implemented using Windows 10 on [Microsoft Azure Cloud](https://azure.microsoft.com).
 
## Install Anaconda
Download and install [Anaconda](https://www.anaconda.com/download/) (Python 2.7).

## Install Microsoft Visual C++ Compiler for Python 2.7
Download and install from [here](https://www.microsoft.com/en-us/download/details.aspx?id=44266)

## Install zipline-live
Open up Anaconda Shell and install zipline-live as follows:
```
pip install zipline-live[ib]
```

## Update Numpy
In Anaconda Shell, run the follwing command to update Numpy. If you get permissions denied errors, close Anaconda Shell and open it as Administrator and run:
```
pip install numpy --upgrade
```

## Install ta-lib (optional)
Open Anaconda Shell as Adminstrator and install talib using `conda`:
```
conda install -c quantopian ta-lib
```

## Download and install IB TWS
Download, install, and configure IB TWS as shown [here](/tutorial)


