# Telco Customer Churn Analysis Power BI virtual case experience - Customer Risk Analysis
![dashboard](https://github.com/FatmaNabilEbrahim/Customer-risk-analysis/assets/105246862/bb89c5f1-203f-4e0d-8084-558b14453304)


# Problem Statement

The purpose of this analysis is to: 
- Define proper KPIs
- Create a dashboard for the retention manager that reflects all relevant Key Performance indicators(KPIs)
and metrics in the dataset.
- Based on your findings, recommend suggestions as to what needs to be changed

Here are some inputs:
- Customers who left within the last month
- Services each customer has signed up for: phone, multiple lines, internet, online security, online backup, device protection, tech 
support, and streaming TV and movies
- Customer account information: how long as a customer, contract, payment method, paperless billing, monthly charges, total charges 
and number of tickets opened in the categories administrative and technical
- Demographic info about customers – gender, age range, and if they have partners and dependents

---

# Data Sourcing

The Dataset used for this analysis was presented by [telco-customer-churn](https://www.kaggle.com/datasets/ylchang/telco-customer-churn-1113) and available at:




---

# Data Preparation

Data transformation was done in Power Query and the dataset was loaded into Microsoft Power BI Desktop for modeling.

The customer retention dataset is given by a table named:

- `churn` , `status` , `services` ,`demographics` which has `30 columns and 7043 rows` of observation


The tabulation below shows the `churn` table with its column names and their description:
| Column Name | Description |
| ----------- | ----------- |
| customerID |   Represents the unique number of the customer in the dataset|
| gender | Describes the gender of the customer |
| SeniorCitizen | Describes if the customer is a senior citizen |
| Partner | Describes if the customer has a partner |
| Dependents | Describes if the customer has a dependent |
| tenure | Describes how long as a customer |
| PhoneService | Describes if the customer has registered a phone service |
| MultipleLines | Describes if the customer has registered multiple lines |
| InternetService | Describes if the customer has registered for internet service |
| OnlineSecurity | Describes if the customer has registered for online security  |
| OnlineBackup | Describes if the customer has registered for online backup |
| DeviceProtection | Describes if the customer has registered for device protection |
| TechSupport | Describes if the customer has registered for tech support |
| StreamingTV | Describes if the customer has registered  to stream tv|
| StreamingMovies | Describes if the customer has registered to stream movies |
| Contract | Describes if the length of the contract of the customer |
| PaperlessBilling | Describes if the customer has registered for paperless billing |
| PaymentMethod | Describes the payment method of the customer |
| MonthlyCharges | Represents the monthly charge incurred by the customer |
| TotalCharges | Represents the total charge incurred by the customer |
| numAdminTickets | Represents the number of admin tickets opened by the customer |
| numTechTickets | Represents the number of tech tickets opened by the customer |
| Churn | Describes if the customer is at risk of churn |

Data Cleaning for the dataset was done in power query as follows:

A new table named `churn - unpivot groups` was created by duplicating the `churn` table and unpivoting unnecessary columns.
In the new table, 2 additional conditional columns were added using M-formula:


- Loyalty (which describes how long as a customer): ` Table.AddColumn(#"Added Conditional Column", "Loyalty", each if [tenure] < 12 then "< 1 year" else if [tenure] < 24 then "< 2 years" else if [tenure] < 36 then "< 3 years" else if [tenure] < 48 then "< 4 years" else if [tenure] < 60 then "< 5 years" else "< 6 years")` 


- Risk category: ` Table.AddColumn(#"Changed Type", "Risk category", each if [tenure] < 24 then "Risk 1" else if [tenure] < 48 then "Risk 2" else "Risk 3Table.AddColumn(#"Changed Type", "Risk category", each if [tenure] < 24 then "Risk 1" else if [tenure] < 48 then "Risk 2" else "Risk 3"Table.AddColumn(#"Changed Type", "Risk category", each if [tenure] < 24 then "Risk 1" else if [tenure] < 48 then "Risk 2" else "Risk 3")`

Further cleansing was done as follows:

- Unnecessary columns were removed 
- Each of the columns in the table were validated to have the correct data type 

---

# Data Modeling

After the dataset was cleaned and transformed, it was ready to be modeled.

- A one-to-many (*:1) relationship was created between the `churn` , `demgraphics` , `status` and `services` tables using the customerId column in each of the tables
- The relationship formed in the data model is shown below:


![model](https://github.com/FatmaNabilEbrahim/Customer-risk-analysis/assets/105246862/50532bbc-fea3-494f-b922-20d64e27333b)


---

# Data Visualization

Data visualization for the dataset was done in 2 folds using Microsoft Power BI Desktop:

-  The `Churn` Page: Shows the churn dashboad containing # of customers at risk, # of Tech Tickets, # of Admin Ticket, Yearly Charges, Monthly charges, Demographics, e.t.c 
-  The `Customer Risk Analysis` Page: Shows the # of customers, the churn rate, churn by type of internet service, type of contract, e.t.c


Figure 1 shows visualizations from `Churn` page

| Figure 1 |
| ----------- |
![dashboard](https://github.com/FatmaNabilEbrahim/Customer-risk-analysis/assets/105246862/84ea4332-bd8d-447a-a383-dbcddc67f3c6)

Figure 2 shows visualizations from `Customer Risk Analysis` page

| Figure 2 |
| ----------- |
![risk](https://github.com/FatmaNabilEbrahim/Customer-risk-analysis/assets/105246862/5eaed7a7-90ee-4069-bb17-112af2865b46)

---

# Data Analysis

Measures used in visualization are:

- churn rate % = `DIVIDE (CALCULATE(COUNT(churn[Churn]), churn[Churn] = "yes" ),CALCULATE ( COUNT (churn[Churn]), ALLSELECTED (churn[Churn] ) )
)`


- Count of Churn for Yes =` CALCULATE(COUNTA('churn'[Churn]), 'churn'[Churn] IN { "Yes" })`


- Count of DeviceProtection for Yes = 
`CALCULATE(
	COUNTA('churn'[DeviceProtection]),
	'churn'[DeviceProtection] IN { "Yes" }
)`


- Count of MultipleLines for Yes = 
`CALCULATE(
	COUNTA('churn'[MultipleLines]),
	'churn'[MultipleLines] IN { "Yes" }
)`


- Count of OnlineBackup for Yes = 
`CALCULATE(
	COUNTA('churn'[OnlineBackup]),
	'churn'[OnlineBackup] IN { "Yes" }
)`


- Count of OnlineSecurity for Yes = 
`CALCULATE(
	COUNTA('churn'[OnlineSecurity]),
	'churn'[OnlineSecurity] IN { "Yes" }
)`


- Count of PhoneService for Yes = 
`CALCULATE(
	COUNTA('churn'[PhoneService]),
	'churn'[PhoneService] IN { "Yes" }
)`


- Count of StreamingMovies for Yes = 
`CALCULATE(
	COUNTA('churn'[StreamingMovies]),
	'churn'[StreamingMovies] IN { "Yes" }
)`


- Count of StreamingTV for Yes = 
`CALCULATE(COUNTA('churn'[StreamingTV]), 'churn'[StreamingTV] IN { "Yes" })`


- Count of TechSupport for Yes = 
`CALCULATE(COUNTA('churn'[TechSupport]), 'churn'[TechSupport] IN { "Yes" })`


- Dependents in % = `DIVIDE(CALCULATE(COUNT(churn[Dependents]), churn[Dependents]="Yes", churn[Churn]= "Yes"), CALCULATE(COUNT(churn[Dependents]), churn[Churn]="Yes"),0)`


- Device protection in % = `DIVIDE(CALCULATE(COUNT(churn[DeviceProtection]), churn[DeviceProtection]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(churn[DeviceProtection]),churn[Churn]="Yes"),0)`


- Multiple lines no in % =` DIVIDE(CALCULATE(COUNT(churn[MultipleLines]), churn[MultipleLines]="No", churn[Churn]="Yes"),CALCULATE(COUNT(churn[MultipleLines]),churn[Churn]="Yes", churn[MultipleLines] <> "No phone service"),0)`


- Multiple Lines yes in % =` DIVIDE(CALCULATE(COUNT(churn[MultipleLines]), churn[MultipleLines]="Yes", churn[Churn]= "Yes"), CALCULATE(COUNT(churn[MultipleLines]), churn[Churn]="Yes", churn[MultipleLines] <> "No phone service"),0)`


- Online Bacup in % = `DIVIDE(CALCULATE(COUNT(churn[OnlineBackup]), churn[OnlineBackup]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(churn[OnlineBackup]),churn[Churn]="Yes"),0)`


- Online Sec. in % =` DIVIDE(CALCULATE(COUNT(churn[OnlineSecurity]), churn[OnlineSecurity]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(churn[OnlineSecurity]),churn[Churn]="Yes"),0)`


- Partner in % =` DIVIDE(CALCULATE(COUNT(churn[Partner]), churn[Partner]="Yes", churn[Churn]= "Yes"), CALCULATE(COUNT(churn[Partner]), churn[Churn]="Yes"),0)`


- Phone Service in % = `DIVIDE(CALCULATE(COUNT(churn[PhoneService]), churn[PhoneService]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(churn[PhoneService]),churn[Churn]="Yes"),0)`


- SeniorCitizen in % =` DIVIDE(CALCULATE(COUNT(churn[SeniorCitizen]), churn[SeniorCitizen]=1, churn[Churn]= "Yes"), CALCULATE(COUNT(churn[SeniorCitizen]), churn[Churn]="Yes"),0)`


- Streaming Movies in % = `DIVIDE(CALCULATE(COUNT(churn[StreamingMovies]), churn[StreamingMovies]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(churn[StreamingMovies]),churn[Churn]="Yes"),0)`


- Streaming TV in % = `DIVIDE(CALCULATE(COUNT(churn[StreamingTV]), churn[StreamingTV]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(churn[StreamingTV]),churn[Churn]="Yes"),0)`


- Tech Support in % = `DIVIDE(CALCULATE(COUNT(churn[TechSupport]), churn[TechSupport]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(churn[TechSupport]),churn[Churn]="Yes"),0)`


As shown from [Data Visualization](https://github.com/globalsmile/Customer-Risk-Analysis#Data-Visualization), It can be deduced that:

- `7043` customers are at risk of churn 
- The churn rate is `26.54%` 
- The yearly charges is `$16.06M` 

---

# Insights

As shown by the figures It can be deduced that:

- `2955` tech tickets were opened
- `3632` admin tickets were opened
- The monthly charges is `$456.12K` 
- more insights can be detected too 

---

# Recommendation

- Increase tech support   capacity for Fiber Optic customers and lower tech tickets per customer to 0.5

- Increase sale of 1 and 2 year contracts by 5% each

- Yearly increase of automatic payments by 5%

