# DPRank

The main contributors: Elizaveta Stavinova, Ilyas Varshavskiy, Petr Chunaev, Ivan Derevitskii and Alexander Boukhanovsky.

## About
This repository provides an implementation of algorithmic support for dynamic pricing based on surrogate ticket demand modeling for a passenger rail company on open data.

The data for this study was collected by our team from open-source online rail ticket sales. Since our study contains, among other things, incremental learning of a surrogate model, the [data](https://github.com/AlgoMathITMO/DPRank/tree/main/Datasets "Datasets") was divided into two datasets, [old](https://github.com/AlgoMathITMO/DPRank/blob/main/Datasets/data.zip "Old dataset") and [new](https://github.com/AlgoMathITMO/DPRank/blob/main/Datasets/new_data.zip "New dataset").

The [Experiments folder](https://github.com/AlgoMathITMO/DPRank/tree/main/Experiments "Folder with experiments results") contains separate directories for research [without incremental learning](https://github.com/AlgoMathITMO/DPRank/tree/main/Experiments/Surrogate%20Modeling "Data for experiments without incremental learning") and [with incremental learning](https://github.com/AlgoMathITMO/DPRank/tree/main/Experiments/Incremental%20Learning "Data for experiments with incremental learning"). Each of the directories contains a Data folder, which contains data files obtained because of experiments, and a Figure folder, which contains illustrative materials obtained because of experiments.

Algorithmic support for dynamic pricing without incremental learning is divided into two notebooks, the [first](https://github.com/AlgoMathITMO/DPRank/blob/main/DPRank_preprocessing.ipynb "Preprocessing") notebook contains preprocessing, the [second](https://github.com/AlgoMathITMO/DPRank/blob/main/DPRank_surrogate_modeling.ipynb "Surrogate modeling and optimization problem solution") one contains surrogate modeling and optimization problem solution. Similarly for dynamic pricing with incremental learning. Some of the functions, methods, and classes for both tasks are contained in the [Utilities](https://github.com/AlgoMathITMO/DPRank/blob/main/Utilities.py "Utilities") file.

### Description of data files: 

* data.csv (data.zip) - Old data
* prices.csv - Not average prices
* places.csv - Number of empty seats in train cars
* demand.csv - Ticket demand
* prices_cons.csv - Data used to obtain price bounds
* new_data.csv (new_data.zip)- New data
* mean_prices.csv - Average prices
* mean_demand.csv - Average demand
* r2_df.csv – Values of the coefficient of determination of the linearized model
* pred_demand_df.csv - linearized demand obtained from the simulation
* relined_demand_df.csv - demand received because of simulation
* A_df.csv - *a* coefficients of models
* B_df.csv - *b* model coefficients
* *Train number* _ *Day of week* _ *popsize*.npy – the data obtained from the optimization contains the optimal prices, model errors generated, and revenue generated by the optimization.
* new_*file_name*.csv – files obtained because of incremental learning.

The structure of the collected and used [data](https://github.com/AlgoMathITMO/DPRank/tree/main/Datasets "Data structure") is shown in table 1.

Table 1: The structure of the data collected and used.
<p align="center">
  <img src="https://github.com/AlgoMathITMO/DPRank/blob/main/Tables/data_file_info.jpg">
</p>

## Experimental results

### Obtaining a Model of Price Elasticity of Demand

As a result of approximation by a power function of the existing price elasticity of demand, its description is formed, as shown in Figure 1.

<p align="center">
  <img src="https://github.com/AlgoMathITMO/DPRank/blob/main/Experiments/Surrogate%20Modeling/Figure/A_752A/A%20Surrogate%20model%20of%20price%20elasticity%20of%20demand.jpg" width=100% height=100%>
</p>
<p align="center">
  Figure 1. Price elasticity of demand for Type A train.
</p>

The parameters of this model are represented by the coefficients a and b, as well as the absolute and relative errors.

The model parameters are shown in Figure 2.

<p align="center">
  <img src="https://github.com/AlgoMathITMO/DPRank/blob/main/Experiments/Surrogate%20Modeling/Figure/A_752A/A%20Model_parameters.jpg" width=60% height=60%>
</p>
<p align="center">
  Figure 2. Parameters of the linearized model of price elasticity of demand for a Type A train.
</p>

The histogram of the distribution of model errors is shown in Figure 3.

<p align="center">
  <img src="https://github.com/AlgoMathITMO/DPRank/blob/main/Experiments/Surrogate%20Modeling/Figure/A_752A/A%20Histogram%20of%20distribution%20of%20errors.jpg" width=100% height=100%>
</p>
<p align="center">
  Figure 3. Model errors distribution histogram for Type A train.
</p>

### Getting bounds for optimization

The distribution of prices by service classes and their boundaries are shown in Figure 4.

<p align="center">
  <img src="https://github.com/AlgoMathITMO/DPRank/blob/main/Experiments/Surrogate%20Modeling/Figure/A_752A/A%20Price%20histogram%20with%20price%20ranges%20of%20classes.jpg" width=80% height=80%>
</p>
<p align="center">
  Figure 4. Distribution of prices by class of service for a Type A train.
</p>

Service classes provided:
* B1 — First;
* B2 — Economy+;
* C1 — Business;
* C2 — Economy.

Since the real price boundaries of the classes are unknown, the lines in this figure represent the price boundaries that we obtained. The dashed line shows the real average prices by class of service. These bounds are further used for optimization.

### Optimization

The optimization results are shown in the [Figures](https://github.com/AlgoMathITMO/DPRank/blob/main/Experiments/Surrogate%20Modeling/Figure/A_752A "A Type train Figures") below. In these figures, the line shows the corresponding average values of the quantities, the semi-transparent area indicates the confidence interval.

#### Prices

The prices obtained as a result of the optimization and the prices of the passenger railway company are shown in Figure 5.

<p align="center">
  <img src="https://github.com/AlgoMathITMO/DPRank/blob/main/Experiments/Surrogate%20Modeling/Figure/A_752A/A%20Average%20prices%2Bconfidence%20interval.jpg" width=55% height=55%>
</p>
<p align="center">
  Figure 5. Comparison of prices based on optimization results for Type A train.
</p>

#### Demand

The demand calculated from the prices received from the optimizer and the demand of the passenger railway company is shown in Figure 6.

<p align="center">
  <img src="https://github.com/AlgoMathITMO/DPRank/blob/main/Experiments/Surrogate%20Modeling/Figure/A_752A/A%20Average%20demand%2Bconfidence%20interval.jpg" width=55% height=55%>
</p>
<p align="center">
  Figure 6. Comparison of the demand obtained by optimization and the demand of a passenger railway company for Type A train.
</p>

The limits on the demand of the passenger railway company and the demand achieved as a result of optimization are shown in Table 2.

Table 2: otal demand for tickets received by the optimizer by class of service for τ =
2, . . . , 14.
<p align="center">
  <img src="https://github.com/AlgoMathITMO/DPRank/blob/main/Tables/optimizer_demand.jpg">
</p>

#### Revenue

The revenue received as a result of optimization and the revenue of the passenger railway company is shown in Figure 7.

<p align="center">
  <img src="https://github.com/AlgoMathITMO/DPRank/blob/main/Experiments/Surrogate%20Modeling/Figure/A_752A/A%20Average%20revenue%2Bconfidence%20interval.jpg" width=55% height=55%>
</p>
<p align="center">
  Figure 7. Comparison of the revenue obtained by optimization and the revenue of a passenger railway company for a Type A train.
</p>

Numerical optimization results obtained from the [data](https://github.com/AlgoMathITMO/DPRank/tree/main/Experiments/Surrogate%20Modeling/Data/Optim "Optimization results for different trains") are shown in Table 3.

Table 3: Summarized revenue (as the sum of revenue random variables for τ = 2, . . . , 14)
obtained via simulation and from the real-world Railways Company data (m and s stand
for the sample mean and sample standard deviation, correspondingly). The amounts in
rubles and percents are rounded to the nearest integer. The revenue changes comparable with
or more than the standard deviation of both the simulation and Railways Company data
samples are shown in magenta.
<p align="center">
  <img src="https://github.com/AlgoMathITMO/DPRank/blob/main/Tables/revenue_update.jpg">
</p>

Some other graphical results are presented at the [link](https://github.com/AlgoMathITMO/DPRank/tree/main/Experiments/Surrogate%20Modeling/Figure "Graphic results for experiments without incremental learning") and at the [link](https://github.com/AlgoMathITMO/DPRank/tree/main/Experiments/Incremental%20Learning/Figure "Graphic results for experiments with incremental learning").

The study was funded in 2021-2022 by RFBR, Sirius University of Science and Technology, JSC Russian Railways and Educational Fund “Talent and success”, project number 20-37-51006.
