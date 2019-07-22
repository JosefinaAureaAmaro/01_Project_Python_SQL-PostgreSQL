# Team 18 Proposal (Greyson & Josefina):

We plan on using 17 datasets from Fec.Gov due to .csv export limit of 500,000 rows per csv. We will be extracting data from CSVs into
Jupyter Notebooks. Using Python's Panda library, we will tranform the csv files to have them ready to load into our PostgreSQL database. 

Our datasets will be focus on expedenture and contributions by campaign regarding the Presidental Candidates for the 2016 election. 

Examples of tables that the database can produce is as follows:
1. Contributions to Candidates from Individuals
2. Contributions to Candidates from Committees
4. Contributions to Candidates by State
3. Total Expenditures by Candidate
4. Total Expenditure by Candidate per Operation Category

Also, our hope is that this resulting database can be used for quickly finding and visualizing information about the (a) sources of 
funds raised and (b) recipients of disbursements by each major party candidate in the 2016 election and (c) how the categorical funds 
and spending varies by candidate.


## Project Report
### Data Analysis and Cleaning

**Data Source:** https://www.fec.gov/data/
The Fec provides a few options for aquiring data from it's data page. 
 1. Download an export of the table via their interactive portal
 2. Bulk download uncategorized data
 3. Call an API

Bulk Download Notes:
The Bulk Download was not used due to it's lack of data details and organizination.
Also, it did not appear to contain the details related to the categories in our objective. 
Thus we stuck with the direct approach of exporting from the table via their interactive portal. 


API Notes:
The API was not used due to the size of the data we were collecting. 
It would not have been practical to use thier API due to their API limit of 100,000 max results per day.
Per their API documentation, https://api.open.fec.gov/developers/, each user is only allowed 1,000 API calls per day and each call is  
limited to 100 results each.

Thus, with our Expenses and Contributed Funds datasets comprising of 365,000 and 4,400,000 results, respectively, it was not considered 
as an option. 



**Data Transform techniques used:**
Contribution Data
 1. Filtering 
 2. Aggregating

Expense Data

**Database Type:** Relational - PostgreSQL

An ERD Diagram is provided to review source data tables and examples of final tables that can be reviewed from the database. 
