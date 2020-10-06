
# IDA 2016 Challenge: APS Failure prediction for Scania Trucks #

This project provides an end to end approach to develop a model for failure prediction of Air Pressure System (APS) of heavy Scania trucks using dataset provided in IDA, 2016 challenge. The proposed approach helps the predictive model outperform previous approaches by significant margin.

##	1. Introduction ##
The dataset consists of data collected from heavy Scania trucks in everyday usage. The system in focus is the Air Pressure system (APS) which generates pressurized air that are utilized in various functions in a truck, such as braking and gear changes. The dataset’s positive class consists of component failures for a specific component of the APS system.  The negative class consists of trucks with failures for components not related to the APS. The data consists of a subset of all available data, selected by experts.     

##	2. Attributes ##
The attribute names of the data have been anonymized for proprietary reasons. It consists of both single numerical counters and histograms consisting of bins with different conditions
. Typically the histograms have open-ended conditions at each end. For example if we are measuring the ambient temperature "T" then the histogram could be defined with 4 bins where: 
* bin 1 collect values for temperature T < -20.
* bin 2 collect values for temperature T >= -20 and T < 0.    
* bin 3 collect values for temperature T >= 0 and T < 20.  
* bin 4 collect values for temperature T > 20.
	
bin 1  | bin 2 | bin 3  | bin 4
------------- | ------------- |------------- | -------------
T < -20  | T >= -20 and T < 0 | T >= 0 and T < 20 | T > 20

The attributes are as follows: class, then anonymized operational data. The operational data have an identifier and a bin id, like "Identifier_Bin".- In total there are 171 attributes, of which 7 are histogram variables. Missing values are denoted by "na".
##	3. Data characteristics ##
The data comes in two files, one training set and a test set. Both sets are sampled from the same source with stratification regarding the class, hence they should contain roughly the same distribution of faulty and non-faulty components.  The training set contains 60000 examples in total in which 59000 belong to the negative class and 1000 positive class. The test set contains 16000 examples.
##	4. Challenge metric  ##
The contestants will be measure according to the following  cost-metric of miss-classification:

Predicted class | True class |	|
------------- | ------------- | ------------- |
 |  | Positive |  Negative 
 | Positive |  |  Cost_1
 | Negative | Cost_1 |  

Cost_1 = 10 and Cost_2= 500
The total cost of a prediction model the sum of "Cost_1” multiplied by the number of Instances with type 1 failure  and "Cost_2" with the number of instances with type 2 failure,  resulting in a "Total_cost". In this case Cost_1 refers to the cost that an unnecessary check needs to be done by an mechanic at an workshop, while Cost_2 refer to the cost of missing a faulty truck,  which may cause a breakdown.
**Total_cost = Cost_1*No_Instances + Cost_2*No_Instances.**
