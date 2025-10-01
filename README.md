
# Power BI Project: Banking Transactions & Customer Overview Dashboard 

### Dashboard Link : https://app.powerbi.com/groups/me/reports/6bb3eb30-e991-44d4-91f9-84851c4de40e/2df0cead5baa1ea296e6?experience=power-bi

This Power BI project consists of two main dashboards: Transactions & Branch Performance and Customer & Account Overview. These dashboards analyze key banking metrics, offer actionable insights, and display interactive visuals for executive-level reporting.

## Project Objectives
Analyze and visualize key metrics related to banking transactions, branch performance, customer demography, and account balances.

Provide an interactive report for stakeholders to make informed business decisions.

## Data Preparation & Import
- Step 1: Raw Data Collection:
Import transactional, customer, account, and branch datasets into the sql server.
Merge datasets by applying inner joins to make a Combined Table from these Four Table Datasets.It Was observed that all date column's date formats were not in one single format,so changed them to a single date format like 'mm/dd/yyyy' using sql query. Next Load data into Power BI Desktop from SQL Server.

- Step 2: Cleaning & Handling Missing Data:
i) Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
ii) Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
iii) It was observed that in none of the columns errors & empty values were present except column named "Phone Number" and "Gender".Use Power Query to fill missing fields (e.g., handle missing phone numbers and Gender in customer data).
iv) Standardize column names and data formats (e.g., convert balances to numerical types, date fields to Date ). For changing Datatypes in Date columns used locale and then select datatype 'Date' and Locale is 'English(United States)

- Step 3:Create calculated columns for KPIs, such as total transaction value or customer gender distribution.

## Power BI Report Structure
# 1. Transactions & Branch Performance Dashboard
Key Panels:
Total Transactions & Value:
Shows the aggregate number of transactions (10K) and total transaction value (424.16M)using Card Visuals, calculated as summarized fields in Power BI. 

![Image](https://github.com/user-attachments/assets/7710dd2e-91d5-49d1-81ac-34b04791f5d1)


Transaction Type Breakdown:
Visualized using a column chart to show Debit versus Credit transaction counts.
for creating new measures following DAX expression was written;

      Transaction Count = COUNT(CombinedBankingDataset[TransactionID])
       

Channel Split Pie Chart:
Displays the percentage distribution of Transactions by Channel (Branch, ATM, Online) using calculated DAX fields.
Following DAX expression was written to find Channel Usage %,

      Channel Usage % = DIVIDE(COUNTROWS(CombinedBankingDataset), CALCULATE(COUNTROWS(CombinedBankingDataset), ALL(CombinedBankingDataset)), 0)

![Image](https://github.com/user-attachments/assets/7073ac38-bba3-48d0-87e9-e686fe15c7db)

Top Branch Balances:
Rendered with a horizontal bar chart to compare balances by branch names and Sates, sorted descending by balance.
Following DAX expression was written to find Branch Wise Balance,
      
      Branch Balance = SUMX(FILTER(CombinedBankingDataset, CombinedBankingDataset[BranchID] = MAX(CombinedBankingDataset[BranchID])), CombinedBankingDataset[Balance])

Filter interactions to allow drill-down by Branch Name or State.

Average Transaction Value by Year:
A line chart visualizes the yearly trend in average transaction value, derived with DAX measures summarizing total value divided by count.
Following DAX expression was written to find Average Transaction Value,

     Avg Transaction Value = AVERAGE(CombinedBankingDataset[Amount])  
![Image](https://github.com/user-attachments/assets/69e987a4-4971-4970-934f-5689eae85063)



# 2. Customer & Account Overview Dashboard
Key Panels:
Total Customers & Accounts:
Shows the overall count for customers (1104) and Number of accounts (2875).Visualized it using Card Visuals.

 ![Image](https://github.com/user-attachments/assets/49357d07-051b-4a69-ae53-1bd8343b1e99)

![Accounts](https://github.com/user-attachments/assets/aa95fb89-5f71-4006-90ec-ecf7f95629ed)

Average Account Balance Gauge:
A gauge visual to indicate the mean balance across all accounts.
Following DAX expression was written to find Average Account Balance,

        Avg Account Balance = AVERAGE(CombinedBankingDataset[Balance])
Balance by Account Type:

Pie chart displays the split between Savings and Current Account Balances.By using Value Account Types and Balance column.


Monthly New Customers:
Stacked Column chart tracks new registrations each month, using customer creation date.
Following DAX expression was written to find New Customers Per Month,

       New Customers = CALCULATE(DISTINCTCOUNT(CombinedBankingDataset[CustomerID]), YEAR(DATEVALUE(CombinedBankingDataset[JoinDate])) = YEAR(TODAY()))

![Image](https://github.com/user-attachments/assets/d46c9b36-1c68-4238-b064-3246e0a772c1)

Customer Distribution By Gender:
A donut  chart presents gender segmentation, including Unknown.

Top 5 Customers By Balance:
Horizontal Bar Chart showing leading customers based on Account Balances.

![Image](https://github.com/user-attachments/assets/9fcd42a8-671f-47ed-875d-3de4515cdb68)


 The report was then published to Power BI Service.

![Image](https://github.com/user-attachments/assets/a0add561-7ab3-428c-bf3f-0927cac5939e)

 # Report Snapshot (Power BI DESKTOP)

![Image](https://github.com/user-attachments/assets/1805db15-51bf-4f4b-83fc-e3b89bd97e78)

![Image](https://github.com/user-attachments/assets/ed2a4576-4866-4d24-b301-6006d9f6247e)


How to Use & Extend
Interactive Filtering:
Visuals are cross-filtered for deeper insights; e.g., selecting a branch filters transaction details.


# Conclusion
This Power BI project demonstrates efficient ETL (Extract, Transform, Load) practices, DAX efficiency, and Dashboarding skills for Banking Analytics. It offers an intuitive experience for decision-makers and can be extended to fit larger datasets or new metrics as needed.

