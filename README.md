# Statistics-in-Python    
This project explains how to perform basic and advanced statistics in Python using Pandas, NumPy, and SciPy. It covers descriptive statistics, measures of dispersion, correlation, covariance, and different hypothesis tests like t-tests, ANOVA, Chi-square, and Mann-Whitney tests.

Summary - 

1.Created a sample dataset using Pandas.

2.Calculated mean, median, mode, range, IQR, variance, and standard deviation.

3.Measured skewness and kurtosis to understand distribution shape.

4.Computed covariance and correlation between skills.

5.Performed hypothesis tests: one-sample t-test, two-sample t-test, paired t-test.

6.Applied ANOVA, Chi-square, and Mann-Whitney tests.

7.Interpreted p-values to accept or reject null hypotheses.


```python
## 1 - Import pandas and create dataframe
import pandas as pd
sample_data = {'name':['john','jack','happy','rupa','priya'] , 
               'gender':['male','male','male','female','female'],
               'Communication_skill_score':[40,45,23,39,39],
               'quantitative_skill_score':[38,41,42,48,32]}

  ## 2 
  data = pd.DataFrame(sample_data,columns = 
  ['name','gender','Communication_skill_score','quantitative_skill_score'])

## 3 - Mean
find mean of Communication_skill_score col
data['Communication_skill_score'].mean(axis=0)

##
Mode
find mode of Communication_skill_score col
data['Communication_skill_score'].mode()

## 4
Median
find median of Communication_skill_score col
data['Communication_skill_score'].median()

## 5
Measuring dispersion
find range of Communication_skill_score col
column_range = data['Communication_skill_score'].max() - data['Communication_skill_score'].min()
print(column_range)


## 6.IQR 
## First Quartile
q1= data['Communication_skill_score'].quantile(.25)
q3= data['Communication_skill_score'].quantile(.75)
## Inter Quartile Ratio
IQR = q3 - q1
print(IQR)



## 7.Variance
data['Communication_skill_score'].var()


## 8.Std dev
data['Communication_skill_score'].std()


## 9.Describe dataframe
data.describe()


## 10.Skewness  -symmetry of distribution - output is negative skewness -  mean is less than mode and median
data['Communication_skill_score'].skew()


## 11.Kurtosis - measures tailedness - (0-mesokurtic, -ve platykurtic(Normal Distribution), >3 Leptokurtic)
data['Communication_skill_score'].kurtosis()



## 12
covariance 
data1 = pd.DataFrame(sample_data,columns = 
 ['Communication_skill_score','quantitative_skill_score'])
## covariance - relationship between pair of variables - shows degree of change in variables : range + to - infinity 
## covariance between columns of dataframe
data1.cov()
## 69.20 - High variation in communication scores
## 34.20 - moderate variation in quantiative scores 
## -6.55 - Weak negative relationship between the two skills


## 13
 Pearson's Correlation coefficient 
data1.corr(method ='pearson')
## 1.00000 → Perfect correlation with itself
## -0.13464 Very weak negative relationship - almost no correlation 
## No predictive link between skills - Skills are independent - Improve both separately



## 14
Parametric test - quantitative and continous data - T-test
## One sample T-test
import numpy as np
from scipy.stats import ttest_1samp
data = np.array([63,75,84,58,52,96,63,55,76,83])  #### create data
mean_value = np.mean(data) ## ## Find mean
print("Mean:",mean_value)

t_test_value ,p_value = ttest_1samp(data,68)
print("P-value: ", p_value)
print('Ttest_value:', t_test_value)

if p_value <0.05:
  print("Reject null hypothesis")
else:
  print("Accept null hypothesis") 





## 15
Two Sample Ttest - significant diff between independent groups
from scipy.stats import ttest_ind
# create numpy arrays 
data1 = np.array([63,75,84,58,96,63,55,76,83])
data2 = np.array([53,43,31,113,33,57,27,23,24,43])
#compare samples 
stat,p= ttest_ind(data1,data2)
print("P-values:",p)
print("T-test: ", stat)

if p<0.05:
  print("Reject null hypothesis")
else:
  print("Accept null hypothesis")




## 16
Paired sample T-test
from scipy.stats import ttest_rel
# weights before treatment
data1 = np.array([63,75,84,58,52,96,63,65,76,83])
data2 = np.array([53,43,31,113,33,57,27,23,24,43])
# Compare weights
stat, p= ttest_rel(data1,data2)
print("P-values:",p)
print("T-test: ", stat)

if p<0.05:
  print("Reject null hypothesis")
else:
  print("Accept null hypothesis")




# 17 ANOVA
from scipy.stats import f_oneway
# performance score of mumbai location
mumbai= [0.4571202 , 0.72662912, 0.48446207, 0.614338  , 0.69460859,
       0.69358957, 0.99339649, 0.81508554, 0.22369787, 0.20925829]
      
#performance scores of chicago location 
chicago = [0.61096471, 0.98417245, 0.45611384, 0.50842402, 0.80139376,
       0.3556954 , 0.10237514, 0.88676153, 0.3204297 , 0.17387475]

##performance scores of london location 
london= [0.79215927, 0.67546637, 0.52866739, 0.6543885 , 0.34175879,
       0.25354941, 0.78719995, 0.96130432, 0.62228626, 0.56975604]

# compare results using one-way anova
stat,p= f_oneway(mumbai,chicago,london)
print("P-values:",p)
print("T-test: ", stat)

if p<0.05:
  print("Reject null hypothesis")
else:
  print("Accept null hypothesis")





#18
 Non-Parametric test - chisquare 
from scipy.stats import chi2_contingency
average =[20,16,13,7] # Average performing employees
Outstanding = [31,40,60,13] # Outstanding performing employees
Contigency_table = np.array([average,Outstanding])

#Apply test
stat,p,dof,expected = chi2_contingency(Contigency_table)
print("P-values:",p)

if p<0.05:
  print("Reject null hypothesis")
else:
  print("Accept null hypothesis")




# 19
Mann whitney u-test
from scipy.stats import mannwhitneyu
data1=[7,8,4,9,8]
data2=[3,4,2,1,1]
stat,p= mannwhitneyu(data1,data2)
print("P-values:",p)

if p<0.05:
  print("Reject null hypothesis")
else:
  print("Accept null hypothesis")

## Variance
data['Communication_skill_score'].var()

Conclusion -

Python makes statistical analysis easy and efficient. Using Pandas and SciPy, we can quickly understand data, measure relationships between variables, and test hypotheses.
The results show that communication and quantitative skills are almost independent, and statistical tests help identify meaningful differences between groups.
