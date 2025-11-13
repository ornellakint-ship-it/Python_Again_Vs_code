
# The Analysis

## What are the top 3 demanded skills for the 3 most popular Data roles ?
To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my detailled notebook here: [Skills_Counting_Project.ipynb](3_Project\Skills_Counting_Project.ipynb)

### Visualise Data

```python
fig, ax = plt.subplots(len(job_titles), 1) 

sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
    ax[i].set_title(job_title)
    ax[i].invert_yaxis()
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].get_legend().remove()
    ax[i].set_xlim(0, 78)

    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1.5, n, f'{v:.0f}%', va='center')

    if i != len(job_titles) - 1:
        ax[i].set_xticks([])    


fig.suptitle("Likelihood of job requests of Skill per Job Postings")
fig.tight_layout(h_pad=1) #Fixes overlap
plt.show()
```
### Chart
![Visualisation of top skills for data people](3_Project\Images\skill_demand_percentage.png)

### Insights

- SQL is the most requested skill for Data Analysts and Data Scientists, with it in over half the job postings for both roles. For Data Engineers, Python is the most sought-after skill, appearing in 68% of job postings.

- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).

- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%).

## How are in-demand skills trending for Data Analysts?

To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the job postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023

View my notebook with detailled steps here: 
[Skills_Trends.ipynb](3_Project\Skills_Trends.ipynb)

### Methodology
1. Aggregate skill counts monthly
2. Re-analyze based on percentage of total jobs
3. Plot the monthly skill demand

### Visualise  Data

```python
df_plot = df_DA_US_percent.iloc[ :, :5]

sns.lineplot(data=df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()

plt.title('Trending Top Skills For Data Analysts in the US')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('2023')
plt.legend().remove()

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

#for i in range(5):
   # plt.text(11.5, df_plot.iloc[-1, i], df_plot.columns[i])   # This is the original code
    
for i, col in enumerate(df_plot.columns):  #This is C's code to solve overlapping of python and tableau labels
    y = df_plot.iloc[-1, i]
    offset = 2 if col == 'python' else (-0.3 if col == 'tableau' else 0)
    plt.text(11.5, y + offset, col)
```

### Chart
![Visualisation of Top Skills for Data Analysts in the US](3_Project\Images\Top_skills_for_DA.png)

### Insights
- SQL remains the most consistently demanded skill throughout the year, although it shows a gradual decrease in demand.

- Excel experienced a significant increase in demand starting around September, surpassing both Python and Tableau by the end of the year.

- Both Python and Tableau show relatively stable demand throughout the year with some fluctuations but remain essential skills for data analysts. Power BI, while less demanded compared to the others, shows a slight upward trend towards the year's end.