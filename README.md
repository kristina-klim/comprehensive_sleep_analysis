 # **Sleep Tracking Analysis: Patterns Before and After Lockdown**
*This project is a revisited and expanded version of the original analysis, which can be found [here](https://github.com/kristina-klim/Sleeping-project-general-analysis/blob/main/sleep_analysis_2021.ipynb). This project intends to build upon the original work and add insights using different data analysis techniques.*

The project analyzes sleep patterns using data from a sleep-tracking ring worn for 447 days. The objective is to understand the changes in sleep patterns Before and After Lockdown measures due to the COVID-19 pandemic.

The project uses Python for data manipulation, visualization, and analysis. Libraries used include Pandas, Matplotlib, and Seaborn.

## **Project Overview**

The project observed the sleep data collected by a sleep-tracking ring, weaving an insightful narrative about sleep patterns and how it affected by the Lockdown. The ultimate goal of the analysis is not just to analyze sleep patterns but also to offer strategies for improving sleep quality.

## **Dataset**

In total, the dataset comprises 447 rows and 11 columns, which are as follows:

| Column | Dtype | Description |
| --- | --- | --- |
| weekdays | object | Day of the week |
| sleep_starts | object | Sleep start time |
| sleep_ends | object | Sleep end time |
| sleep_duration_min | int64 | Duration of sleep in minutes |
| light_sleep_min | int64 | Duration of light sleep in minutes |
| rem_sleep_min | int64 | Duration of REM sleep in minutes |
| deep_sleep_min | int64 | Duration of deep sleep in minutes |
| readiness | int64 | Readiness score |
| sleep_score | int64 | Sleep score |
| activity_score | int64 | Activity score |
| steps | int64 | Number of steps taken |

## **Installation**

The code is written in Python 3. To install the necessary libraries, run the following command:

```
shCopy code
pip install -r requirements.txt

```

## **Usage**

To run the analysis, follow the instructions in the Jupyter Notebook titled comprehensive_sleep_analysis**`.ipynb`**

## **Code Samples**

****Loading and Preprocessing Data****

```sql
# Load dataset. Set index to date column
df = pd.read_csv("sleeping_tracking_.csv",
                 index_col=["date"],
                 parse_dates=["date"])
```

****Exploratory Data Analysis****

```sql
# Get correlation matrix
df_corr = df.corr()

sns.heatmap(df_corr, annot=True, annot_kws={"size": 15})

# Fix ticklabel directions and size
plt.xticks(size = 14, rotation=0)
plt.yticks(size = 14,rotation=0)

# Fits plot area to the plot, "tightly"
plt.tight_layout()
```
<img width="983" alt="Corr" src="https://github.com/kristina-klim/comprehensive_sleep_analysis/assets/84743536/1c29aad3-885d-4760-914d-2a2de84c170c">




****Statistical Analysis****

```sql
# Shapiro-Wilk test for normality
_, p_value_before = stats.shapiro(df_before_lockdown["sleep_duration_min"])
_, p_value_after = stats.shapiro(df_after_lockdown["sleep_duration_min"])

# Histogram
plt.hist(df_before_lockdown["sleep_duration_min"], bins="auto", color=color[1], alpha=0.7, label="Before Lockdown")
plt.hist(df_after_lockdown["sleep_duration_min"], bins="auto", color=color[2], alpha=0.7, label="After Lockdown")

# Set labels
plt.ylabel("Frequency", fontsize = 16)
plt.title("Shapiro-Wilk Test", fontsize=20, fontweight='bold')

# Fix ticklabel directions and size
plt.xticks(size = 14, rotation=0)
plt.yticks(size = 14,rotation=0)
plt.legend(fontsize = 16)

plt.show()

# Print Shapiro-Wilk test p-values
print(f"Shapiro-Wilk Test p-values:\n"
      f"Before Lockdown: {p_value_before}\n"
      f"After Lockdown: {p_value_after}")
```

<img width="976" alt="Shapiro-Wilk Test Hist" src="https://github.com/kristina-klim/comprehensive_sleep_analysis/assets/84743536/8d3e1596-ebc3-41be-a8b7-a7238bc8eb75">


****Average Sleep By Weekdays****

```sql
# Plot the average steps duration by weekdays before and after lockdown
ax = sleep_weekdays_merge.plot.line(marker='o', markersize=7, linewidth=2)

# Set labels and legend
ax.set_xticks(range(len(sleep_weekdays_merge)))
ax.set_xticklabels(sleep_weekdays_merge.index, rotation=0, fontsize=14)
ax.set_xlabel("Weekdays", fontsize=16)
ax.set_ylabel("Avg Sleep", fontsize=16)
ax.set_title("Average Sleep By Weekdays", fontsize=20)

ax.legend(loc='best')
plt.rc('legend', fontsize=13)

# Add labels to the data points
for i, col in enumerate(sleep_weekdays_merge.columns):
    for x, y in enumerate(sleep_weekdays_merge[col]):
        label_text = f"{converting_minutes_to_hours(y)}"

        ax.annotate(label_text, (x, y), textcoords='offset points', 
                    xytext=(1,12), ha='center', fontsize=13)

plt.show()
```
<img width="986" alt="Average Sleep By Weekdays" src="https://github.com/kristina-klim/comprehensive_sleep_analysis/assets/84743536/cee9a071-eafc-4c36-9ff8-1f621520449e">



## 

## **Key Findings**

1. **Sleep Duration**: The analysis showed that the average sleep duration was slightly below the recommended guidelines of 7-9 hours. However, the Lockdown showed increased sleep duration, possibly due to the lack of commute and a more flexible work-from-home schedule.
   
2. **Correlations**: A significant positive correlation was found between Sleep duration and Readiness scores. It suggests a longer sleep duration could lead to a higher daily readiness score.
   
3. **Day of the Week Impact:** The data suggests that the sleep duration and activity levels vary with the day of the week. The most active day is Sunday, which potentially correlates to extended sleep during that day. However, the correlation between Activity Score and Sleep Duration is relatively low at 0.058, indicating that other factors might influence these two variables beyond the scope of this analysis.
   
4. **Impact of Lockdown on Activity Levels: T**here was an increase in the average number of Steps taken daily After the Lockdown.
   
5. **Sleep Stage Shifts:** While the total Sleep duration increased After the Lockdown, an exciting shift was observed in the Sleep stages. REM sleep duration increased, suggesting a potential change in sleep quality, whereas deep sleep duration decreased. It could affect cognitive and physical recovery processes during different sleep stages.
   
