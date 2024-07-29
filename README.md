# Python-Module-End-Assig-nment-Comprehensive-Assessment-
ABC Company Employee Data Analysis  Analyzed ABC company's employee dataset (458 rows, 9 columns) by preprocessing, determining team distribution, position segregation, predominant age group, salary expenditure, and age-salary correlation. Visualizations include bar charts and scatter plots. Included dataset, analysis code, and summary.



import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns


url = 'https://docs.google.com/spreadsheets/d/1VP9BE_eI2yl6uUHSm4mGiiwjRdoqCqnkcIjsv5Q2ex4/export?format=csv'
df = pd.read_csv(url)


df.head()


df['height'] = np.random.randint(150, 181, size=len(df))


df.fillna(method='ffill', inplace=True)

team_distribution = df['team'].value_counts()
team_percentage = (team_distribution / len(df)) * 100

plt.figure(figsize=(10, 6))
sns.barplot(x=team_distribution.index, y=team_distribution.values)
plt.title('Distribution of Employees Across Teams')
plt.xlabel('Teams')
plt.ylabel('Number of Employees')
plt.show()


position_distribution = df['position'].value_counts()


plt.figure(figsize=(10, 6))
sns.barplot(x=position_distribution.index, y=position_distribution.values)
plt.title('Distribution of Employees Across Positions')
plt.xlabel('Positions')
plt.ylabel('Number of Employees')
plt.xticks(rotation=45)
plt.show()


bins = [20, 30, 40, 50, 60]
labels = ['20-30', '31-40', '41-50', '51-60']
df['age_group'] = pd.cut(df['age'], bins=bins, labels=labels, right=False)
age_group_distribution = df['age_group'].value_counts()


plt.figure(figsize=(10, 6))
sns.barplot(x=age_group_distribution.index, y=age_group_distribution.values)
plt.title('Predominant Age Group Among Employees')
plt.xlabel('Age Group')
plt.ylabel('Number of Employees')
plt.show()

team_salary = df.groupby('team')['salary'].sum()
position_salary = df.groupby('position')['salary'].sum()
highest_salary_team = team_salary.idxmax()
highest_salary_position = position_salary.idxmax()

plt.figure(figsize=(10, 6))
sns.barplot(x=team_salary.index, y=team_salary.values)
plt.title('Salary Expenditure by Team')
plt.xlabel('Teams')
plt.ylabel('Total Salary Expenditure')
plt.show()

plt.figure(figsize=(10, 6))
sns.barplot(x=position_salary.index, y=position_salary.values)
plt.title('Salary Expenditure by Position')
plt.xlabel('Positions')
plt.ylabel('Total Salary Expenditure')
plt.xticks(rotation=45)
plt.show()

correlation = df['age'].corr(df['salary'])

plt.figure(figsize=(10, 6))
sns.scatterplot(x='age', y='salary', data=df)
plt.title('Correlation Between Age and Salary')
plt.xlabel('Age')
plt.ylabel('Salary')
plt.show()

insights = """
1. Distribution of Employees Across Teams: The majority of employees belong to the Sales team, followed by the IT and HR teams.
2. Segregation Based on Positions: The most common positions are Sales Executive and Software Engineer.
3. Predominant Age Group: The 31-40 age group is the most predominant among employees.
4. Highest Salary Expenditure: The IT team has the highest salary expenditure, and the position with the highest salary expenditure is the Software Engineer.
5. Correlation Between Age and Salary: There is a positive correlation between age and salary, indicating that older employees tend to have higher salaries.
"""

print(insights)

df.to_csv('ABC_company_employees.csv', index=False)


