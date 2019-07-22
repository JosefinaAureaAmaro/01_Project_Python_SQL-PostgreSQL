# Team 18 Proposal (Greyson & Josefina):

We plan on using 17 datasets from Fec.Gov due to .csv export limit of 500,000 rows per csv. We will be extracting data from CSVs into
Jupyter Notebooks. Using Python's Panda library, we will transform the csv files to have them ready to load into our PostgreSQL database. 

Our datasets will be focus on expenditure and contributions by campaign regarding the Presidential  Candidates for the 2016 election. 

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
#### Extract
**Data Source:** https://www.fec.gov/data/
The Fec provides a few options for acquiring data from it's data page. 
 1. Download an export of the table via their interactive portal
 2. Bulk download uncategorized data
 3. Call their OpenFEC API

*Bulk Download Notes:*
The Bulk Download was not used due to it's lack of data details and organization.
Also, it did not appear to contain the details related to the categories in our objective. 
Thus we stuck with the direct approach of exporting from the table via their interactive portal. 


*API Notes:*
The API was not used due to the size of the data we were collecting. 
It would not have been practical to use their API due to their API limit of 100,000 max results per day.
Per their API documentation, https://api.open.fec.gov/developers/, each user is only allowed 1,000 API calls per day and each call is  
limited to 100 results each.
Thus, with our Expenses and Contributed Funds datasets comprising of 365,000 and 4,400,000 results, respectively, it was not considered 
as an option. 

#### Transform

Due to our choice to export the data manually by the FEC's interactive table portal, our data was categorized and labeled appropriately. 
Thus our main concerns for cleaning the data were filtering the data by candidate, dropping empty or uneccesary columns, and ensure that 
both tables had a candidate_id that was unique by candidate. 

Since our objective for this database was to compare the two candidates, as long as the candidates could be easily identified per table 
then we felt that summary data by candidate would be easily aggregated through a PostgreSQL query. 

*Challenges*: Due to the large data for contributions regarding the Hillary Clinton candidate, it became my objective to find an 
efficient way to iterate through the csv files. I tried a few methods to complete this task, however the final order was such:
   1. Create a dictionary with the keys numbered chronologically starting at 0. Then for the values to contain the name of df used when 
   the csvs were read using pd.read_csv(). 
   
   *A 'dictionary' was used because dictionaries maintain the 'type' of the value, which was imperative for iterating through the data 
   itself, rather than the file name.*
   
   2. I had the keys numbered chronologically because I also wanted to provide the developer feedback on which dataframe was being 
   concatenated for debugging. Thus I created a list that mirrored the chronological order of the dictionary to be used in the 
   iteration. The list contained the names of the dataframes which was to be printed in the order the request was being processed.
   
   3. Lastly, in order to combine the dataframes I found that treating the data as a list and concatenating them was
   the method that worked for me. 
   
   4. Make the list into a dataframe. When the concat function was used, I ignored the index so that the dataframe could assign its own
   index values to produce a proper new dataframe. 
   
   As a note, a great aspect of iterating through dataframes this way is that you can also apply other functions per dataframe 
   in the loop if that would achieve your objective. 

#### Load

**Database Type:** Relational - PostgreSQL

Only two main data tables, candidate_expense and candidate_raised_funds, were needed in the PostgreSQL for the related views to be
populated by the user.

*Screenshots of the database are provided for review*

Depending on how the user created their views from the two main tables would establish the need for updates to be made to the main 
table, such as primary keys etc. 

Thank you reviewing the repo, please have a great day. 
