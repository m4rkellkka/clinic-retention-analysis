# Clinic Patient No-Show Analysis

## Project Description
**Business Task:** Find the key factors that make patients miss their appointments (drop-off rate) and give recommendations to improve the clinic's schedule and marketing budget.
**Tech Stack:** **Python (Pandas, Matplotlib, Seaborn)**.

## Main Business Insights
1. **Planning Horizon Problem:** The attendance rate for same-day appointments is 95%. However, a waiting time of just 1 day drops the attendance to 75%.
2. **SMS Effectiveness:** Sending SMS reminders does not work well for short-term appointments within a week (only a 0.5% difference). But it is very effective for long-term appointments (1 month or more), saving about 7% of visits.
3. **Profile of a Responsible Patient:** Young adults (18-35 years old) miss appointments the most. Surprisingly, having chronic diseases makes people more disciplined — patients with 2 or 3 diagnoses visit the doctor more often than completely healthy people.
4. **Day of the Week Impact:** Attendance is incredibly stable throughout the regular workweek (Monday to Friday), hovering consistently around 80%. There is a slight drop in attendance on Saturdays (~77%), but no drastic anomalies exist. Actionable insight: The clinic does not need to apply dynamic daily staffing or change its scheduling strategy based on the specific workday.

## Code Example
Here I used multi-level grouping to isolate a confounding variable (waiting time) when checking the real impact of SMS reminders:

```python
# Grouping by waiting period AND SMS status
sms_analysis = df.groupby(['wait_period', 'SMS_received']).agg({
    'patient_id': 'count', 
    'no_show_int': 'mean'
}).reset_index()

# Visualizing data with color separation (hue)
sns.barplot(data=sms_analysis, x='wait_period', y='no_show_int', hue='SMS_received')
