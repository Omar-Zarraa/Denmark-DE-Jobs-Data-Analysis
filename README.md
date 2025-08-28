# Overview

Welcome to my Data Analysis project. This project analyses many aspects of the Data Engineering role in Denmark. It shows some relevant and important information about the Dane job market for Data Engineers. This project was made as the final project for [Luke Barousse's Python for Data Analytics course](https://www.youtube.com/watch?v=wUSDVGivd-8&t=35072s). Many thanks go to him and his amazing teaching skills for the tools used in this project.

# The Questions

These are the questions I aimed to answer in my project:

- What are the most demanded skills for the top 3 most popular data roles?
- How are in-demand skills trending for Data Engineers?
-How well do jobs and skills pay for Data Analytics?
- How well do jobs and skills pay for Data Engineers?

# Tools I used

- Python:
    - Pandas: essential for data manipulation and cleaning.
    - Matplotlib: the base for all the plots in this project.
    - Seaborn: extra utilities for making the plots more readable.
- Jupyter Notebooks: very useful tool when it comes to using Python for data analytics, streamlines the process by a lot.

# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles I first filtered for the data roles in Denmark. Then I filtered for the 3 most popular ones and found the top 5 skills for these 3 roles. This Query highlights the most popular job titles and the skills they require.

View my notebook with detailed steps here:
[Skill Demand](./Skills_Demand.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc["job_title_short"] == job_title].head(5)
    sns.barplot(
        data=df_plot,
        x="skills_percent",
        y="job_skills",
        ax=ax[i],
        hue="skill_count",
        palette="flare",
    )
    ax[i].set_title(job_title)
    ax[i].set_ylabel("")
    ax[i].set_xlabel("")
    ax[i].get_legend().remove()
    ax[i].set_xlim(0, 70)

    for n, value in enumerate(df_plot["skills_percent"]):
        ax[i].text(value +1, n, f'{value:.0f}%',va='center')

fig.suptitle("Likelihood of Skills Required in Job Postings", fontsize=15)
fig.tight_layout(h_pad=0.5)
plt.show()
```

### Results

![Visualization](./images/Liklihood%20of%20Skills%20Required%20in%20Job%20Postings.png)

### Insights

- SQL is a very important skill to learn for any data role with it taking the top place in 2 of the 3 roles.
- Python is as valuable as SQL due to its versatility and wide adoptation across many different data and software roles.

## 2. How are in-demand skills trending for Data Engineers?

### Visualize Data

```python
df_DE_DK_percent = df_DE_DK_pivot.div(DE_totals / 100, axis=0)

df_DE_DK_percent = df_DE_DK_percent.reset_index()
df_DE_DK_percent["job_posted_month"] = df_DE_DK_percent["job_posted_mo"].apply(
    lambda x: pd.to_datetime(x, format="%m").strftime("%b")
)
df_DE_DK_percent = df_DE_DK_percent.set_index("job_posted_month")
df_DE_DK_percent = df_DE_DK_percent.drop(columns="job_posted_mo")

df_DE_DK_percent
```

### Results

![Visualization](./images/Trending%20Top%20Skills%20for%20Data%20Engineers%20in%20Denmark.png)

### Insights

- Python and SQL always fight for the top spot showing their incredible importance for anyone aspiring to be a Data Engineer in Denmark.
- AWS, Azure, and Databricks remain on the lower side of demand but they are very important still.
- Azure has lost popularity over time while AWS is growing in demand.

## 3. How well do jobs and skills pay for Data Analytics?

### Salary Analysis for Data Nerds

### Visualize data
```python
sns.boxplot(data=df_DK_top6, x='salary_year_avg', y='job_title_short',order=job_order)
sns.set_theme(style='ticks')

plt.title('Salary Distributions in Denmark')
plt.xlabel('Yearly Salary (USD)')
plt.ylabel('')
plt.xlim(0, 250000) 
ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```

### Results

![Visualization](./images/Salary%20Distributions%20in%20Denmark.png)

### Insights

- Machine Learning Engineers have the most pay on average while Data Scientists have a much more varied pay distribution which could indicate companies hiring more Data Scientists than ML Engineers.

## 4. How well do jobs and skills pay for Data Engineers?

### Visualize Data

```python
ax=plt.gca()

sns.set_theme(style='ticks')

sns.barplot(data=df_DE_top_pay, x='median', y=df_DE_top_pay.index, hue='median', ax=ax, palette='flare')
ax.legend().remove()

ax.set_title('Top 10 Highest Paid Skills for Data Engineers')
ax.set_ylabel('')
ax.set_xlabel('')
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))

plt.tight_layout()
plt.show()
```

### Results

![Visualization](./images/Highest%20Paid%20Skills%20for%20DE.png)

### Insights

- Less required and popular skills such as jenkins and oracle tend to pay more than the more popular skills such as sql and python.
- The pay gap between them indicates a gap in the market for people proficient in these more paid skills.

# What I learned

- I learned a lot about data analysis, from data cleaning to data plotting and everything in between.
- **Data Analysis skills:** finding the data to support what you intend to show, extracting insights from that data, and finding more data to further support those insights.
- **Python data analysis tools:** Pandas, Matplotlib, Seaborn. All very important and useful tools for data analysis.

# Conclusion 

This project and by extension the [course](https://www.youtube.com/watch?v=wUSDVGivd-8&t=35072s) has taught me a lot about data analysis in general and using Python for it as well. It was a very fun and informative course and I enjoyed myself a lot when it came to actually putting those learned skills to the test. I'm looking forward to using these skills more as I continue to learn and dive deeper into Machine Learning and Data Analytics.