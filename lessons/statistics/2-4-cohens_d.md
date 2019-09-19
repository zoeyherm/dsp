"""
[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)


Below is the code I wrote to compute Cohen's d. 
The question asked for the Cohen's d for total weight.
I computed the answer to be 0.089. 
A Cohen's effect size greater than 0.08 is considered to be 
"large". 
This value is greater than 0.029 effect size for 
pregnancy length.

"""

from __future__ import print_function, division

%matplotlib inline

import numpy as np

import nsfg
import first

def my_cohens_d(attr):

    """A function that takes the pregnancy data
    and returns the size effect of an attribute
    compared between first-borns and other live births
    """
    preg = nsfg.ReadFemPreg()
    live = preg[preg.outcome == 1]
    firsts = live[live.birthord == 1]
    others = live[live.birthord != 1]
    
    # First get the means of the two groups:
    
    mean_firsts = firsts[attr].mean()
    mean_others = others[attr].mean()
    
    len_firsts = len(firsts)
    len_others = len(others)
    
    std_firsts = firsts[attr].std()
    std_others = others[attr].std()
    
    weighted_std_num = (std_firsts * len_firsts + std_others * len_others)
    weighted_std_denom = (len_firsts + len_others)
    
    weighted_std = weighted_std_num / weighted_std_denom


    cohens_d = (mean_firsts - mean_others) / weighted_std
    
    return round(abs(cohens_d), 3)
    
    
    
print(my_cohens_d('totalwgt_lb'))       