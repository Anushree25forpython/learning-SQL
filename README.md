**SQL DATA ANALYSIS**

# 📍 Title of the project - Rule-Based Incident Management and Analyst Efficacy

---

## 🧠 Overview

**Data Summary and Composition** - The data analyzed in this project is from an operational dataset from a business involved in gaming, regulated activities. It comprises of column names like 'TICKET', 'RULENAME' (e.g., Blacklist, Deposit Limits exceeded), 'STATUS', 'INCIDENTCOUNT', 'ANALYST' (Handling the tickits). It focuses on tracking and managing incidents or events reported via a ticketing system across different geographic locations along with deatils of analyst query handling and managment.

---

## 🎯Key Analysis & Queries Executed:

## 🛠️Data Preparation: 
The initial steps involved loading the data, checking for duplicates (none found ), handling null values (minimal, primarily in ANALYST, NOTES, and SEARCH columns ), and converting the SUMMARYDATE column to datetime objects. Object type columns were stripped of whitespace and converted to uppercase.


## 📝Text Analysis:
Counted the occurrences of the word "Blacklist" in the NOTES column (result: 221).
Found the latest SUMMARYDATE in which the word "Italian" appears in the NOTES column (result: 2024-01-15).


## ⚖️Geographic & Rule Analysis:
Produced a pivot table showing the count of RULENAME by COUNTRY. The top countries by count were ONTARIO (689), DENMARK (583), and SPAIN (514).
Calculated the time difference in days between the first and last entry for each RULENAME within each COUNTRY using the SQLite julianday() function.
Identified RULENAMEs that do not appear in all countries (i.e., less than the total count of distinct countries).
Identified RULENAMEs that appear in only one country (Count of distinct country =1) .


## 📈Time-Series & Incident Analysis:
Calculated the Rolling Count of Incidents (Rolling_incident_count) by summing INCIDENTCOUNT partitioned by COUNTRY and RULENAME and ordered by SUMMARYDATE .


## 🧑‍💻Analyst Efficiency:
Determined the "most efficient analyst" based on three criteria: Total Tickets Handled (distinct TICKET count), Total Incident Count (sum of INCIDENTCOUNT), and Total Closed Tickets (STATUS = 'CLOSED') . The results were sorted in descending order based on these metrics.


## 📊Ranking Analysis:
Found the second most common rule name by country using the RANK() window function to partition by COUNTRY and order by the count of RULENAME .


## 📝Advanced Text Processing:
Used a Recursive Common Table Expression (CTE) to find the 5th word in the NOTES column for all entries and produced a pivot table showing the occurrence count of each 5th word . The top 5th words were "NO" (81), "CHIPS" (50), "THE" (28), "ALL" (28), and "IN" (27).


## 💡Interesting Finding:
The analysis revealed a significant discrepancy in the Total Incident Count across different analysts. While analysts like Angelo and Paul handled the most tickets, Sarah had an exceptionally high Total Incident Count (273,723) compared to others. This finding suggests the tickets Sarah handles are significantly more numerous or complex in their associated incidents, warranting further investigation into the nature of these specific high-incident tickets or differences in incident attribution.

