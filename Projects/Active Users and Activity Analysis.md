# Active Users and Activity Analysis 🎮



### Objective:

To analyze user activity data in Google Sheets, calculate key user engagement metrics, identify age outliers, structure activity data, and build cohort-based retention analysis.



### Tools & Methods:

- **Google Sheets** – data organization, calculations, and reporting  

- **Formulas & Functions** – age statistics, outlier detection, lookups, daily/weekly metrics, and forecasting using formulas such as AVERAGE, MEDIAN, MODE, STDEV, QUARTILE, IF, ARRAYFORMULA, VLOOKUP, XLOOKUP, INDEX, MATCH, COUNTUNIQUEIFS, AVERAGEIF, MINIFS, and FORECAST  

- **Charts** – visualization of age distribution, outliers, WAU dynamics, and stickiness  

- **Pivot Tables** – cohort analysis and user retention summary  

- **Conditional Formatting** – highlighting retention patterns and key values  

- **Slicers** – filtering cohort data by game, activity type, and language  



### Data Description:

- **User Data**

  - Sheet: `active users`

  - Contains user-level information, including age and language

  - Used for descriptive statistics and outlier detection



- **Activity Data**

  - Sheet: `activity`

  - Contains user activity records, activity dates, game/activity names, and total time spent

  - Used to calculate DAU, WAU, stickiness, and retention



- **Additional Analytical Sheets**

  - `types_of_activities` – grouped activity categories  

  - `DAU` – daily active users  

  - `WAU` – weekly active users, average DAU, and DAU/WAU  

  - `Cohort` – cohort table and retention rate analysis  



### Results 📈

- Calculated age statistics: average, median, mode, min/max, standard deviation, quartiles, and IQR  

- Identified age outliers using IQR-based limits  

- Analyzed the age distribution and detected right-skewness  

- Transformed activity names into structured fields for further analysis  

- Grouped activities into broader activity types  

- Added user language to activity records using lookup formulas  

- Calculated DAU, WAU, Average DAU, and DAU/WAU stickiness  

- Built a 20-week forecast for weekly user activity  

- Created cohort analysis to evaluate user retention over time  

- Added slicers and conditional formatting to make the analysis easier to explore  



### 🖼️ Example
<img width="1052" height="659" alt="image" src="https://github.com/user-attachments/assets/65545a90-4084-44a4-b4f4-01236c9a2b81" />
<img width="1304" height="536" alt="image" src="https://github.com/user-attachments/assets/3e025120-17a7-4bf2-a545-33fced95c6e0" />
<img width="666" height="445" alt="image" src="https://github.com/user-attachments/assets/f08d7bb9-c956-4c44-a43d-ad34f4982e36" />
<img width="478" height="342" alt="image" src="https://github.com/user-attachments/assets/21d5fb6c-7d37-4b69-812d-a7754428990d" />


### Files 📂

- [Active Users and Activity Analysis (Google Sheets)](https://docs.google.com/spreadsheets/d/172oVD8EJI3Im-Jkr45bZ1ndLC0EOs3hLRSs0lmIAYg0/edit?usp=sharing)



---



> **Tools:** Google Sheets  

> **Skills demonstrated:** descriptive statistics, outlier detection, data transformation, lookup formulas, DAU/WAU analysis, forecasting, cohort analysis, retention analysis, pivot tables, data visualization
