# customer_churn_data
# this is my code to identify the reason for customer churn(deactivating)
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sb
df = pd.read_csv("C:/Users/Mahesh/Downloads/customer churn.csv")
print(df.info())
#replacing blanks with a 0 and no total charges are recorded
df['TotalCharges'] = df['TotalCharges'].replace(" ","0")
df['TotalCharges'] = df['TotalCharges'].astype('float')
print(df.info())
print(df.isnull().sum())
print(df.describe())
print(df.duplicated().sum())
print(df['customerID'].duplicated().sum())
def conv(value):
    if value == 1:
        return 'yes'
    else:
        return 'no'

df['SeniorCitizen'] = df['SeniorCitizen'].apply(conv)
print(df.info())
#converted 0 and 1 values of senior citizen to yes/no to make it easier to understand
ax = sb.countplot(x = df['Churn'],data=df)
ax.bar_label(ax.containers[0])
plt.title('Count of customers by churn')
plt.show()
gb = df.groupby('Churn').agg({'Churn':'count'})
print(gb)
plt.pie(gb['Churn'],labels=gb.index,autopct= "%1.2f%%")
plt.title('percentage of churn')
plt.show()
#from the given charts we can conslude that this numbers of customers are churned out
# now lets explore the reason behind it
sb.countplot(x = df['gender'],data=df,hue='Churn')
plt.title("churn by gender")
plt.show()
#it is for gender
sb.countplot(x = df['SeniorCitizen'],data=df,hue='Churn')
plt.title("churn by seniorcitizen")
plt.show()
# Assuming 'df' is your DataFrame
# Creating a crosstab for 'SeniorCitizen' and 'Churn'
rosstab_data = pd.crosstab(df['SeniorCitizen'], df['Churn'])

# Plotting a stacked bar chart
crosstab_data.plot(kind='bar', stacked=True, color=['skyblue', 'orange'], figsize=(8, 6))
plt.title("Churn by SeniorCitizen", fontsize=14)
plt.xlabel("Senior Citizen", fontsize=12)
plt.ylabel("Count", fontsize=12)
plt.legend(title="Churn", labels=["No", "Yes"])
plt.xticks(rotation=0)
plt.show()
# #comparative a greated percentage of people in senior citizen category have churned out
sb.histplot(x= 'tenure',data=df,hue='Churn')
plt.show()
#people who have used our services for a llong time and who used for 1 month they have churned
plt.figure(figsize=(4,4))
ax1 = sb.countplot(x = 'Contract',data=df,hue="Churn")
ax1.bar_label(ax1.containers[0])
plt.title("Contract")
plt.show()
#people who have month to month contract are likely to churn then from those who have 1 or 2 years or contract
print(df.columns.values)
# List of columns to plot
columns = [
    'PhoneService', 'MultipleLines', 'InternetService', 'OnlineSecurity',
    'OnlineBackup', 'DeviceProtection', 'TechSupport', 'StreamingTV',
    'StreamingMovies'
]

# # Number of rows and columns for subplots
n_rows = 3  # Adjust this based on preference
n_cols = 3  # Adjust this based on preference

# # Create the figure and axes
fig, axes = plt.subplots(n_rows, n_cols, figsize=(15, 10))
axes = axes.flatten()

# # Iterate through each column and create a countplot
for i, col in enumerate(columns):
    sb.countplot(x=df[col], ax=axes[i], palette='Set2',hue=df['Churn'])
    axes[i].set_title(f"Count of {col}", fontsize=10)
    axes[i].set_xlabel("")
    axes[i].set_ylabel("Count")

# Remove any empty subplots (if there are more axes than columns)
for i in range(len(columns), len(axes)):
    fig.delaxes(axes[i])
#
# # Adjust layout
plt.tight_layout()
plt.show()
#service attributes (e.g., PhoneService, InternetService) and their relationship with churn (Yes or No). Key observations include higher churn rates for customers with Fiber Optic internet, and lower churn rates for those without internet services or additional features (e.g., TechSupport, DeviceProtection). The charts highlight clear patterns in service usage and churn behavior.
plt.figure(figsize=(4,4))
ax3 = sb.countplot(x='PaymentMethod',data=df,hue='Churn')
ax3.bar_label(ax3.containers[0])
plt.title('by payment method')
plt.show()
#customer is likely to churn when he is using electronic check as a payment menthod
