[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

>> Based on the data provided for this question, 34% of men in the US are between 5'10" and 6'1". 
>>
>> Below is the code that I wrote to arrive at that answer. I also plotted the PMF of the data to ensure that visually the distribution looks normal, and to visualize that between those two heights the probability spans 49% and 83%.
>>
>> ![download (3)](/Users/zoeyherm/Desktop/download (4).png)
>>
>> ```
>> import scipy.stats
>> mu = 178
>> sigma = 7.7
>> dist = scipy.stats.norm(loc=mu, scale=sigma)
>> 
>> a = (scipy.stats.norm(178, 7.7).cdf(177.8))
>> b = (scipy.stats.norm(178, 7.7).cdf(185.42))
>> 
>> print(100 * round((b - a), 2))
>> ```
>>
>> 
