# Simulation study

We present a simulation study in Stata

## Simulated Data

we simulated data for 10,000 individuals. The simulation process is described below

### Smoking status at time zero
variable name: **sm_status0** 

32% never smokers
20% former smokers
48% current smokers

### Sex
variable name: **sex**

50% men
50% women

### Age (in years) at time zero
variable name: **age**

Drawn from a normal distribution with: Mean: 50, sd: 2.5

###  Family history of CVD
variable name: **fh_CVD**

It is drawn from a Bernoulli distribution with 
Pr(fh_CVD=1) = 0.12+ sd 0.05

###  Diuretics at time zero
variable name: **diuretics0**

It is drawn from a Bernoulli distribution with 
Pr(diuretics0 =1) = -0.14+0.03*age+0.1*sex + sd 0.04

### BMI at time zero
variable name: **BMI0**

Conditional on age, sex, family history of CVD, smoking status (at time zero) and diuretics (at time zero), BMI at time zero was drawn from a normal distribution with mean 25.8+0.06*(age-18)+0.1*sex+0.5*fh_CVD-0.1*sm_status0-0.2*diuretics0 and sd 0.56

### Height 
variable name: **height**

Drawn from a normal distribution with: 
Mean: 1.63m, sd: 0.03m --> for women
Mean: 1.80m, sd: 0.03m --> for men

### Smoking cessation between time zero and the 1st follow-up
variable name: **sm_cess1**

It is equal to 0 for never and former smokers at time zero and for those who were current smokers at time zero, it is drawn from a Bernoulli distribution with 
Pr(sm_cess=1) = -1.8+0.041*age-0.01*sex+0.2*diuretics0+ sd 0.04

### Diuretics at the 1st follow-up
variable name: **diuretics1**

It is drawn from a Bernoulli distribution with 
Pr(diuretics1 =1) = 1.4+0.03*age+0.1*sex+0.1*diuretics0 + sd 0.04
	
### CVD at the 1st follow-up
variable name: **CVD1**

It is drawn from a Bernoulli distribution with 
Pr(CVD1 =1) = -1.9+0.035*age+0.03*sex+0.3*fh_CVD+0.1*diuretics0 + sd 0.03

### BMI at the 1st follow-up
variable name: **BMI1**

Conditional on BMI at time zero, age, family history of CVD, smoking status (at time zero) and diuretics (at time zero), BMI at time zero was drawn from a normal distribution with mean 
BMI0-0.9*CVD1+ 0.1* sm_status0 +2.5*sm_cess1-1.8*diuretics0-0.9*diuretics1+0.005*age and sd 1.4

### Weight
variable name: : **weight0** (at time zero) and **weight1** (at 1st follow-up)

Weight0=BMI0*height^2   
Weight1=BMI1*height^2

### Weight change
Combining information on weight1 and weight0, we created the 3 categories of weight change, i.e.
#### weight loss:
(weight1- weight0)/ weight0 < -5%

#### weight maintenance: 
(weight1- weight0)/ weight0 ≥ -5% & (weight1- weight0)/ weight0 ≤ 5%

#### weight gain:
(weight1- weight0)/ weight0 >5%

### Time to event data
We then simulated time to event data for the next 18 years from a Weibull distribution with lambda 10^(-4) and gamma 1.1 and the following log hazard ratio for the covariates (Table S4), after deleting the participants that developed CVD between time zero and the 1st follow-up


# Weighted Kaplan-Meier curves

We run an example in Stata (script "Weighted Kaplan Meier curves").

We present how we can estimate the Weighted Kaplan-Meier curves using IPW from the 1st simulated dataset "Final dataset_1" from the "simulation study" script


# Risk Curves using the g-formula

We run an example in Stata (script "Risk Curves using the g-formula").

We present how we can estimate the risk curves using the g-formula from the 1st simulated dataset (in a long format) "Final dataset (pooled)_1" from the "simulation study" script

