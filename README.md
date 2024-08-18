For my analysis, I am using [lukebarousse/data_jobs](https://huggingface.co/datasets/lukebarousse/data_jobs) Dataset.

# Import & Clean Up Data

I use Kaggle platform, and uploaded the above mentioned dataset as .csv file on Kaggle platform.
I start by importing necessary libraries and loading the .csv file, and cleaned the data
    
    import pandas as pd

    import ast

    import matplotlib.pyplot as plt

    import seaborn as sns

    df = pd.read_csv("/kaggle/input/data-jobs-by-lukebarousse/data_jobs.csv")

    #convert string type "job_posted_date" to datetime object
    df["job_posted_date"] = pd.to_datetime(df.job_posted_date)

    #convert string type "job_skills" to list, with apply()
    df["job_skills"] = df.job_skills.apply(lambda skill: ast.literal_eval(skill) if pd.notna(skill) else skill)


# How are in-demand skills trending for Data Analysts

I first filtered out from the original dataframe, to only include data about India. 

`india_df = df[df["job_country"] == "India"]`

Then I found out the 3 top most jobs in India, and grouped the data on the top 5 skills from those top 3 jobs.

For detailed steps, here is the notebook: [01. Top 5 Most In-Demand Skills from The Top 3 Data Jobs in India](https://github.com/WandererFakeer/Python_Data_Science_Basic_Projects/blob/main/01.%20Top%205%20Most%20In-Demand%20Skills%20from%20The%20Top%203%20Data%20Jobs%20in%20India.ipynb)


## Visualize Data
       

    
    fig, ax = plt.subplots(len(top_3_roles), 1, figsize = (8, 6))

    #loop through the "top_3_roles" to get the dataframe containing only the job roles in each index
    for idx, job_title in enumerate(top_3_roles):

         top_job_with_top_5_demanded_skills = top_3_roles_and_skills_group_with_cents[top_3_roles_and_skills_group_with_cents["job_title_short"] == job_title].head()

         sns.barplot(data = top_job_with_top_5_demanded_skills, x = "skills_percentage", y = "job_skills", hue = "skills_count", palette = "dark:green_r", dodge = False, ax = ax[idx])
    plt.show()



## Results

![01. Top 5 Most In-Demand Skills from The Top 3 Data Jobs in India](https://github.com/user-attachments/assets/47cd71a8-84c5-4f3b-86e1-4f5d8f6c54aa)

_Bar graph visualizing the job counts percentages for the top 5 skills, associated with the top 3 data roles in India_


## Insights:

● SQL is the most requested skill for Data Analysts and Data Engineers, with over half the job postings for both roles. For Data Scientists, Python is the most sought-after skill, appearing in 70% of job postings.

● Python is one of the most important skill, highly demanded across all three roles, but most prominently for Data Scientists (70%) and Data Engineers (61%).
