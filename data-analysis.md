# Splunk (Data Visualisation)
I imported the prepared CSV dataset into Splunk Enterprise and verified that the fields were correctly extracted for analysis. After confirming the data was structured properly, I created multiple visualizations to display the key variables related to fraud activity. These charts included comparisons of fraud versus non-fraud transactions, breakdowns by gender and transaction attributes, and trend-based visualizations to highlight patterns over time. I then combined these visualizations into a single dashboard to provide a clear, interactive view of the data. This dashboard allows the team to quickly identify trends, detect suspicious activity, and support informed decision-making in fraud prevention.
## Count by Category
<img width="1884" height="600" alt="image" src="https://github.com/user-attachments/assets/112c98d6-2e2a-453f-9fce-f9f46a81ef17" />

**Splunk Query**
```splunk
source="prepared_data_cleaned.csv" host="TETEHPC" sourcetype="csvprepared_data.csv"
| stats count by category
| sort - count
```

## Count of Fraudulent Payment
<img width="1884" height="350" alt="image" src="https://github.com/user-attachments/assets/06c67dfc-f296-4bad-8605-5af9bf28cec7" />

**Splunk Query**
```splunk
source="prepared_data_cleaned.csv" host="TETEHPC" sourcetype="csvprepared_data.csv"
| stats count by fraud
```

## Fraudulent Transactions by Category
<img width="1889" height="371" alt="image" src="https://github.com/user-attachments/assets/d59841f1-b031-4a6f-a1f4-6969b5aefc4f" />

**Splunk Query**
```splunk
source="prepared_data_cleaned.csv" host="TETEHPC" sourcetype="csvprepared_data.csv" fraud=1
| stats count by category
| sort - count
```

## Fraudulent Transactions by Gender 
<img width="1889" height="354" alt="image" src="https://github.com/user-attachments/assets/4ddd2ce6-87ae-45e9-8a98-a4e7d93ce9a1" />

**Splunk Query**
```splunk
source="prepared_data_cleaned.csv" host="TETEHPC" sourcetype="csvprepared_data.csv" fraud=1
| stats count as "Fraudulent Transactions" by gender
| sort - "Fraudulent Transactions"
```

## Fraudulent Transactions by Age (Chart)
<img width="532" height="374" alt="image" src="https://github.com/user-attachments/assets/f1a61e49-e1f3-4fba-8aac-a7a2f73b79ca" />

**Splunk Query**
```splunk
source="prepared_data_cleaned.csv" host="TETEHPC" sourcetype="csvprepared_data.csv" fraud=1
| eval age_group=case(
    age==0.0,"<=18",
    age==1.0,"19-25",
    age==2.0,"26-35",
    age==3.0,"36-45",
    age==4.0,"46-55",
    age==5.0,"56-65"
)
| stats count as "Fraudulent Transactions" by age_group
```

