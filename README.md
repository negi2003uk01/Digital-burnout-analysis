# Digital-burnout-analysis
📋 Project Overview
This project analyzes digital burnout patterns across 99,999 users, exploring the relationships between screen time, sleep quality, productivity, mental health, and work environment. The goal is to identify key burnout risk factors and provide actionable insights through an interactive Power BI dashboard.

📁 Dataset
PropertyDetailsFiledigital_burnout.xlsxRows99,999 usersColumns35 featuresSourceDigital Burnout Survey Data
Key Columns

user_id — Unique identifier
burnout_risk — Burnout risk score (0–100)
productivity_score — Productivity score (0–100)
daily_screen_time — Daily screen time in hours
sleep_hours — Average sleep hours
stress_level — Stress level score (0–10)
motivation_level — Motivation score (0–10)
work_satisfaction — Work satisfaction score (0–10)
mental_fatigue — Mental fatigue score (0–10)
workspace_quality — Workspace quality score (0–10)
occupation — Job role of user
work_mode — Remote / Hybrid / On-site


🧹 Data Cleaning
Data cleaning was performed inside Power BI using Power Query Editor before loading into the data model.
Steps Performed in Power Query
1. Changed Data Types
Selected each column → Transform → Data Type
→ burnout_risk       : Whole Number
→ productivity_score : Whole Number
→ daily_screen_time  : Decimal Number
→ sleep_hours        : Decimal Number
→ age                : Whole Number
3. Handled Null Values
All columns containing null values were replaced with the median value of that column to avoid skewing results with outliers.
Columns cleaned:

deep_work_hours → replaced nulls with median
social_media_hours → replaced nulls with median
motivation_level → replaced nulls with median
sleep_hours → replaced nulls with median
physical_activity → replaced nulls with median

How to replace with median in Power Query:
1. Select column
2. Transform → Statistics → Median
   (note the median value)
3. Right click column → Replace Values
4. Replace null with median value
4. Renamed Columns
Renamed columns to be clean and readable
Example:
daily_screen_time → Daily Screen Time
burnout_risk      → Burnout Risk
5. Trimmed Text Columns
Selected text columns (occupation, work_mode, mental_state)
Transform → Format → Trim
Removed extra spaces from text values

📊 Power BI Dashboard
Dashboard Pages
PageTitleFocusPage 1Executive OverviewOverall burnout summaryPage 2Productivity Deep DiveWork output analysisPage 3Sleep, Lifestyle & Mental HealthWellness analysisPage 4Motivation & Work EnvironmentMotivation analysisPage 5–8Tooltip Pages (Hidden)Custom chart tooltips

Page 1 — Executive Overview
KPI Cards:

Total Users
Avg Burnout Risk Score
Avg Productivity Score
Total High Burnout Users 
Avg Sleep Hours
Avg Daily Screen Time

Charts:

Burnout Risk by Occupation (Clustered Bar)
Productivity Category Distribution (Donut)
Burnout Risk by Work Mode (Clustered Column)
Burnout Risk vs Screen Time (Scatter)
Mental State Distribution (Treemap)


Page 2 — Productivity Deep Dive
KPI Cards:

Total High Productivity Users
Total Low Productivity Users
Avg Deep Work Hours
Avg Task Completion Rate
Avg Focus Sessions
Avg Concentration Score
Avg Distraction Frequency Score

Charts:

Productivity by Occupation (Horizontal Bar)
Task Completion by Work Mode (Clustered Column)
Deep Work vs Productivity (Scatter)
Focus Sessions by Age Group (Clustered)
Meeting Hours vs Productivity (Scatter)


Page 3 — Sleep, Lifestyle & Mental Health
KPI Cards:

Avg Stress Score
Avg Mental Fatigue Score
Avg Emotional Exhaustion Score
Avg Work Satisfaction Score
Avg Physical Activity Hours
Avg Caffeine Intake
Late Night Device Users Score

Charts:

Sleep Quality by Occupation (Clustered )
Stress by Work Mode (Clustered Column)
Caffeine vs Sleep Hours (Scatter)
Physical Activity vs Burnout (Scatter)
Late Night Usage vs Sleep Quality (Clustered Bar)


Page 4 — Motivation & Work Environment
KPI Cards:

Avg Motivation Score
Avg Work Satisfaction Score
Avg Workspace Quality Score
Avg Internet Stability Score
Avg Remote Work Days
High Motivation Users %
Low Satisfaction Users %

Charts:

Motivation Level by Occupation (Horizontal Bar)
Work Satisfaction by Work Mode (Clustered Column)
Motivation vs Burnout Risk (Scatter)
Workspace Quality vs Productivity (Clustered Column)

🧮 DAX Measures
Calculated Columns
dax-- Burnout Risk Category
Burnout Risk Category = 
SWITCH(
    TRUE(),
    digital_burnout[burnout_risk] >= 70, "High",
    digital_burnout[burnout_risk] >= 40, "Medium",
    "Low"
)

-- Age Group
Age Group = 
SWITCH(
    TRUE(),
    digital_burnout[age] <= 25, "Gen Z (≤25)",
    digital_burnout[age] <= 35, "Millennial (26-35)",
    digital_burnout[age] <= 45, "Mid Career (36-45)",
    "Senior (46+)"
)

-- Sleep Status
Sleep Status = 
SWITCH(
    TRUE(),
    digital_burnout[sleep_hours] < 6, "Sleep Deprived",
    digital_burnout[sleep_hours] <= 8, "Normal",
    "Well Rested"
)

-- Screen Time Category
Screen Time Category = 
SWITCH(
    TRUE(),
    digital_burnout[daily_screen_time] >= 10, "Excessive",
    digital_burnout[daily_screen_time] >= 6, "Moderate",
    "Low"
)

-- Sort Orders (to fix alphabetical sorting)
Burnout Sort Order = 
SWITCH(
    TRUE(),
    digital_burnout[burnout_risk] >= 70, 1,
    digital_burnout[burnout_risk] >= 40, 2,
    3
)

Age Sort Order = 
SWITCH(
    TRUE(),
    digital_burnout[age] <= 25, 1,
    digital_burnout[age] <= 35, 2,
    digital_burnout[age] <= 45, 3,
    4
)
Key Measures
dax-- Page 1
Total Users = COUNTROWS(digital_burnout)

Avg Burnout Risk = AVERAGE(digital_burnout[burnout_risk])

Avg Productivity Score = AVERAGE(digital_burnout[productivity_score])

-- Page 2
Avg Deep Work Hours = AVERAGE(digital_burnout[deep_work_hours])

Avg Task Completion Rate = AVERAGE(digital_burnout[task_completion_rate])

-- Page 3
Avg Stress Level = AVERAGE(digital_burnout[stress_level]) * 10

Avg Motivation Level = AVERAGE(digital_burnout[motivation_level]) * 10

Total Late Night Device Users  = 
        COUNTROWS(FILTER(digital_burnout, digital_burnout[late_night_device_usage] = 1))
        
-- Page 4
Avg Workspace Quality = AVERAGE(digital_burnout[workspace_quality]) * 10

 Total High Motivation Users % = 
        COUNTROWS(FILTER(digital_burnout, digital_burnout[motivation_level] >= 7))
        

🎨 Dashboard Theme
ElementColorPage Background#050D1ACard Background#0A1628Chart Background#0D1F3CPrimary Accent#00B4D8Secondary Accent#FF6B35High Risk#FF4D6DMedium Risk#FFD166Low Risk#00E5A0White Text#FFFFFFSoft Label#A0B4C8

⚙️ Tools Used
ToolPurposeMicrosoft ExcelRaw data source (.xlsx)Power Query (Power BI)Data cleaning & transformationPower BI DesktopDashboard, DAX & visualization



📌 Key Insights

Sleep deprived users score on average 30% lower on productivity
Remote workers report lower stress levels compared to on-site workers
Deep work hours have the strongest positive correlation with productivity score
Late night device usage directly reduces sleep quality scores


👤 Author
shrestha mohan negi



📄 License
This project is licensed under the MIT License.
