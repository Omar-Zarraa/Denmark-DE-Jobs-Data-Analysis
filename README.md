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