# InterventionEvaluatR
This package is designed to run several different types of analyses to evaluate the effect of interventions using time series data of counts. The package implements synthetic controls analyses (Broderson; Bruhn), STL+PCA analysis (Shioda), a simple time trend analysis (with or without an offset term), and a classic interrupted time series analysis. In all approaches, a Poisson model is used with an observation-level random intercept to capture overdispersion. The synthetic controls analysis uses Bayesian variable selection (spike and slab priors, as implemented in the pogit package) to fit the model.

## Installing the package:

-Install and load devtools in R.

-#install.packages('devtools')

-library(devtools)

-devtools::install_github('https://github.com/weinbergerlab/InterventionEvaluatR')

-library(InterventionEvaluatR)

### Note to Mac users: 
You need to have Xcode installed on your machine; not all OS have this pre loaded. Install Xcode from the Apple App Store, and then follow the instructions above.

## Getting started
After loading the package, run: vignette('PAHO-mortality'). You can view the compiled vignette at https://weinbergerlab.gitlab.io/InterventionEvaluatR/PAHO-mortality.html

## Important notes on the input data

*The input data should contain 1 variable with a grouping variable (e.g., age_group). If there is no grouping variable, include a column of 1s

*The input data should contain a date variable, preferably in the format YYYY-mm-01

*The code currently assumes the data are measured at monthly or quarterly time steps. Other time resolutions are not currently supported

*The outcome variable and all of the control variables should be counts. The control variables are log transformed in the program prior to model fitting. A continuity correction (addition of 0.5) is used to allow for log-transformation of the count variables when 0s are included. Because the control variables are log-transformed, negative values are not allowed.

## Sample Data

Sample data, which are described in Bruhn et al., are included with the package. There are five files, each containing time series of hospitalization for various conditions from five countries in the Americas. The data are subsetted by age group. The data can be accessed by:     

br1<-data(pnas_brazil, package = "InterventionEvaluatR") #load the data

ch1<-data(pnas_chile, package = "InterventionEvaluatR") #load the data

ec1<-data(pnas_ecuador, package = "InterventionEvaluatR") #load the data

mx1<-data(pnas_mexico, package = "InterventionEvaluatR") #load the data

us1<-data(pnas_us, package = "InterventionEvaluatR") #load the data


##Citations
Brodersen, Kay H., et al. "Inferring causal impact using Bayesian structural time-series models." The Annals of Applied Statistics 9.1 (2015): 247-274.

Bruhn, Christian AW, et al. "Estimating the population-level impact of vaccines using synthetic controls." Proceedings of the National Academy of Sciences 114.7 (2017): 1524-1529.

Shioda, Kayoko, et al. "Challenges in estimating the impact of vaccination with sparse data." Epidemiology 30.1 (2019): 61-68.
