# Regression-model-week-2
Regression modeling in practice week 2 assignment
Dataset: NESARC Wave 1 data
Variables considered for this analysis:
Explanatory Variable: 
S1Q2B (BIOLOGICAL FATHER EVER LIVE IN HOUSEHOLD BEFORE RESPONDENT WAS 18 [Yes=1, No=2])
Response Variable: 
S11AQ1A6 (MORE THAN ONCE QUIT A JOB WITHOUT KNOWING WHERE WOULD FIND ANOTHER ONE [Yes=1, No=2])
Research Question: 
Is there a relation between whether biological father live in the household before respondent was 18  and More than once quit a job without knowing where would find another one [ANTISOCIAL PERSONALITY DISORDER (BEHAVIOR)]?
Data Preparation:
Categories ‘blank’ and 9 are converted to NAN in explanatory variable.
Centering explanatory variable - As the explanatory variable is categorical, ‘No’ category is coded to 0.

Number of categories in both explanatory and response variables are 2.
Summary Statistics:
Below are the results of frequency tables ran on both explanatory and response variables.
Frequency table for S1Q2B (BIOLOGICAL FATHER EVER LIVE IN HOUSEHOLD BEFORE RESPONDENT WAS 18 (Explanatory variable):
1    36862 
0     4750
Frequency table for S11AQ1A6 (MORE THAN ONCE QUIT A JOB WITHOUT KNOWING WHERE WOULD FIND ANOTHER ONE  [Yes=1, No=2] (Response variable)

2    37298 
1     4644
Below is the Summary statistics result run on both explanatory and response variables:
            IDNUM             	S1Q2B        	S11AQ1A6
count  43093.000000  41612.000000  41942.000000
mean   21547.000000      0.885850      1.889276
std    12440.021912          0.317997      0.313794
min        1.000000         	0.000000       1.000000
25%    10774.000000      1.000000      2.000000
50%    21547.000000      1.000000      2.000000
75%    32320.000000      1.000000      2.000000
max    43093.000000      1.000000      2.000000

Regression model summary:
OLS Regression Results                            
=============================================================
Dep. Variable: S11AQ1A6                                   	R-squared:0.002
Model: OLS                                                         	Adj. R-squared:0.002
Method: Least Squares                                       	F-statistic: 70.62
Date: Fri, 04 Dec 2015                                        	Prob (F-statistic): 4.48e-17
Time: 05:51:39                                                    	Log-Likelihood: -10470.
No. Observations: 40676                                    	AIC: 2.094e+04
Df Residuals: 40674                                           	BIC: 2.096e+04
Df Model: 1                                         
Covariance Type: nonrobust                                         
=============================================================
                coef        	std err          t          	P>|t|      [95.0% Conf. Int.]

Intercept      1.8534      0.005    403.856      0.000        1.844     1.862
S1Q2B         0.0410     0.005      8.403        0.000         0.031     0.051
=============================================================
Omnibus: 19017.592                                            	Durbin-Watson: 2.007
Prob(Omnibus): 0.000                                          	Jarque-Bera (JB):71326.372
Skew: -2.482                                                         	Prob(JB): 0.00
Kurtosis: 7.177                                                      	Cond. No. 5.75
=============================================================
Statistical explanation:
R-squared is low (0.002) which shows that only 0.2% of variation in response variable is explained by explanatory variable.
p-value is low (4.48e-17) which shows there is a significant relationship between explanatory and response variables.
Regression coefficients: Intercept is 1.8534 and slope is 0.0410. As the slope is greater than 0, explanatory variable is positively related to the response variable. 

Regression equation is y = 1.8534+0.0410*x (where y is response variable and x is explanatory variable)


Python program:
import numpy
import pandas
import statsmodels.api as sm
import seaborn
import statsmodels.formula.api as smf
pandas.set_option(‘display.float_format’, lambda x:’%.2f’%x)
nesarc = pandas.read_csv('nesarc_pds.csv’, low_memory=False)
#setting variables you will be working with to numeric
nesarc['S1Q2B’] = nesarc['S1Q2B’].convert_objects(convert_numeric=True)
nesarc['S11AQ1A6’] = nesarc['S11AQ1A6’].convert_objects(convert_numeric=True)
# replace blanks and 9 category in explanatory variable S1Q2B to nan
nesarc['S1Q2B’]=nesarc['S1Q2B’].replace(9, numpy.nan)
nesarc['S1Q2B’]=nesarc['S1Q2B’].replace(’ ’, numpy.nan)
nesarc['S1Q2B’]=nesarc['S1Q2B’].replace(2, 0)
# replace 9 category in response variable S11AQ1A6 to nan
nesarc['S11AQ1A6’]=nesarc['S11AQ1A6’].replace(9, numpy.nan)
# Summary statistics
nesarc['S1Q2B’].describe()
nesarc['S11AQ1A6’].describe()
# frequency tables
nesarc['S1Q2B’].value_counts()
nesarc['S11AQ1A6’].value_counts()
# regression model
reg = smf.ols('S11AQ1A6 ~ S1Q2B’, data=nesarc).fit()
print (reg.summary())

