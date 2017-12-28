
# Testing a Perceptual Phenomenon
### An in-depth statistical analysis of the Stroop Effect

## Variables

1.) In this circumstance the independent variable is the color of ink shown to the individual as it relates to the word, i.e. congruency or incongruency. And therefore, the dependent variable is the amount of time it takes the individual to name said ink color

## Hypotheses

2.) My hypotheses are as follows:

My null hypothesis is that the population mean of the congruent data set and the incongruent data set will have no significant difference. My alternative hypothesis is that the population mean of the congruent data set will be different than that of the incongruent data set.


$ H_{0}: \mu_{congruent} - \mu_{incongruent} = 0 \\
H_{A}: \mu_{congruent} - \mu_{incongruent} ≠ 0 $


For this situation, I will conduct a paired t-test. The reason for this is that we only have a sample of the actual population of all human beings, but two results are being measured from each individual. There are no pre/post test conditions, there is not more than one sample to test, and the sample should be representative of the population at large, assuming it is random. For these reasons, and the fact we are comparing two sets of results from the same individuals, the paired t-test is the best solution.


## Descriptive Statistics



```python
congruent = [12.079,16.791,9.564,8.63,14.669,12.238,14.692,
             8.987,9.401,14.48,22.328,15.298,15.073,16.929,
             18.2,12.13,18.495,10.639,11.344,12.369,12.944,
             14.233,19.71,16.004]

incongruent = [19.278,18.741,21.214,15.687,22.803,
               20.878,24.572,17.394,20.762,26.282,
               24.524,18.644,17.51,20.33,35.255,22.158,
               25.139,20.429,17.425,34.288,23.894,17.96,
               22.058,21.157,]
```


```python
import numpy as np


print "Congruent Mean Time: " + str(np.mean(congruent))
#Notice that ddof is set to 1 to account for Bessel's correction as this is a sample not a population standard devitation
print "Congruent Standard Deviation: " + str(np.std(congruent, ddof = 1))
print "Incongruent Mean Time: " + str(np.mean(incongruent))
print "Incongruent Standard Deviation: "+ str(np.std(incongruent, ddof = 1))


```

    Congruent Mean Time: 14.051125
    Congruent Standard Deviation: 3.55935795765
    Incongruent Mean Time: 22.0159166667
    Incongruent Standard Deviation: 4.79705712247


3.)	This dataset shows that the mean time to identify colors with congruent words is **14.051125** with a standard deviation of **3.55935795765**. Additionally, the mean time to identify colors with incongruent words is **22.0159166667** with a standard deviation of **4.79705712247**.


## Visualizations


```python
%matplotlib  inline
import matplotlib.pyplot as plt

plt.hist(congruent)
plt.title("Congruent Histogram")
plt.xlabel("Time")
plt.ylabel("Frequency")

```




    <matplotlib.text.Text at 0x10a7b6290>




![png](output_6_1.png)



```python
plt.hist(incongruent)
plt.title("Incongruent Histogram")
plt.xlabel("Time")
plt.ylabel("Frequency")

```




    <matplotlib.text.Text at 0x10a7b6e50>




![png](output_7_1.png)


4.) Above are the two histograms of times taken to identify congruen and incongruent words. As detailed by the visulization, you can see that the congruent times make a more normalized distrobution, while the incongruent times are more variable. There seems to be some interesting times in the incongruent data set that are much larger than the rest of the data. 

## Performing the Test


```python
import math

#Subtracting incongruent from congruent data to get the diffeneces from each
diff = [i - j for i, j in zip(congruent, incongruent)]

#Calculating the mean differences
diff_mean = np.mean(congruent) - np.mean(incongruent)

#Calculating standard deviation of differences
#Squaring the differences
diff_squared_deviation_mean = []
for i in diff:
    diff_squared_deviation_mean.append((i - diff_mean) ** 2)

#Adding squared deviation differences
sum_diff_squared_deviation_mean = 0
for i in diff_squared_deviation_mean:
    sum_diff_squared_deviation_mean += i

#Dividing sum_diff_squared_deviation_mean by n - 1
variance = sum_diff_squared_deviation_mean / (len(diff) - 1)

#Taking square root of variance    
diff_stdv = math.sqrt(variance)

#Calculating T-Statistic
t_stat = diff_mean / (diff_stdv / math.sqrt((len(diff))))

print "The mean of the differences is " + str(diff_mean)
print "The standard deviation of the differences is " + str(diff_stdv)
print "The T-Statistic is " + str(t_stat)
```

    The mean of the differences is -7.96479166667
    The standard deviation of the differences is 4.86482691036
    The T-Statistic is -8.02070694411


## Evaluating the Results
5.) With a significance level of $\alpha = .05$ and $23 DOF$, we get a t-critical of $\pm 2.06865761$. Therefore, our t-statistic obtained by the calculations above($ -8.02070694411 $) gives us evidence to reject our null hypothesis $ H_{0}: \mu_{congruent} - \mu_{incongruent} = 0 $.


## Conclusion

In conclusion, there is significant difference between the congruent and incongruent words. With the data at hand, we see that the incongruent words take exceedingly more time to identify than the congruent words. This was what I had expected, especially after taking the test myself I proposed that the incongruent words would take much longer.

Sources:

https://classroom.udacity.com/
https://stackoverflow.com/questions/534855/subtracting-2-lists-in-python
