[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

>The prompt for this question was to:
>
>> 1. Construct distributions for the number of children in the household for all of the respondents to the NSFG study. 
>>
>>    a. For the raw data.
>>
>>    b. For a simulated biased data set that reflects what the responses would look like had they been generated from a survey of the children in the households. 
>>
>> 2. Report the means of the two data sets.
>
>My answers are: (1) The figure below shows both histograms and Pmfs of each data set, where orange is the unbiased, raw data, and blue results illustrated the simulated, biased results. (2) The mean of the raw data is 1.024 children per household, and the mean of the simulated biased data is 2.404 children per household. 
>
>The code I wrote to answer the question is below.





>![Graph1](/Users/zoeyherm/Desktop/download.png)


    

```python
from __future__ import print_function, division

%matplotlib inline

import numpy as np

import nsfg
import first
import thinkstats2
import thinkplot


resp = nsfg.ReadFemResp()

# Start the plotting process just with the unbiased data.

num_children_reported = thinkstats2.Pmf(resp.numkdhh)

thinkplot.PrePlot(2, cols=2) 
thinkplot.Hist(num_children_reported, align='right', width=width, color = 'orange', label = 'Unbiased') 
thinkplot.Config(xlabel='Number of children in household', ylabel='probability', axis=[-1, 5, 0, 0.5])

thinkplot.PrePlot(2) 
thinkplot.SubPlot(2) 
thinkplot.Pmfs([num_children_reported], align = 'edge', label = 'Unbiased', color = 'orange')
thinkplot.Show(xlabel='Number of children in household', axis=[-1, 6, 0, .5])


# Now make a new PMF to illustrate what
# biased data would look like according to
# the "class size paradox", where reporting
# by interviewing people generates skewed results

def make_data_biased(pmf, label):
    new_pmf = pmf.Copy()
    
    for x, p in pmf.Items():
        # This is what is originally in the file:
        new_pmf.Mult(x, x)
        print(p)
    
    new_pmf.Normalize()
    
    return new_pmf


# Plot the simulated biased data in addition to the raw data above.

biased_children_reported = make_data_biased_2(num_children_reported, label = "Simulated Biased Data")

thinkplot.PrePlot(2, cols=2) 
thinkplot.Hist(num_children_reported, align='left', width=width, color = 'orange', label = 'Unbiased raw data') 
thinkplot.Hist(biased_children_reported, align='right', width=width, color = 'b', label = 'Simulated biased results') 
thinkplot.Config(xlabel='Number of children in household', ylabel='Probability', axis=[-1, 5, 0, 0.5])

thinkplot.PrePlot(2) 
thinkplot.SubPlot(2) 
thinkplot.Pmfs([num_children_reported], label = 'Unbiased raw data', color = 'orange')
thinkplot.Pmfs([biased_children_reported], label = 'Simulated biased results', color = 'b')
thinkplot.Show(xlabel='Number of children in household', axis=[-1, 6, 0, .5])


# Now compute the mean of each:

hist = thinkstats2.Hist(resp.numkdhh, "Number of Children")

def get_pmf_mean(pmf):
    
    mean = 0
    
    for x, p in pmf.Items():
        mean += x * p
    
    return round(mean, 3)
        
print("Mean of raw data:", get_pmf_mean(num_children_reported))
print("Mean of simulated biased data:", get_pmf_mean(biased_children_reported))
```

