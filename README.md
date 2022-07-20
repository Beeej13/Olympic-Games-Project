# Olympic-Games-Project
Graphical representation of Olympic Games over 120 years
Explore a dataset on the modern Olympic Games, including all the Games from Athens 1896 to Rio 2016. 

# First of all, import the different libraries.

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px

# Importing dataframe
mydata = pd.read_csv("C:\\Users\\BenjaminJones\\Documents\\Datasets\\120 Years O\\athlete_events.csv")

pd.set_option('display.max_rows', None, 'display.max_columns', None)

# creating gold medal dataframes 
goldMedals = mydata[(mydata.Medal == 'Gold')]

# creating Silver medal dataframes
silverMedals = mydata[(mydata.Medal == 'Silver')]

# creating Bronze medal dataframes
bronzeMedals = mydata[(mydata.Medal == 'Bronze')]

# Display of Gold Medals against age over time
plt.figure(figsize=(20, 10))
plt.title('Distribution of Gold Medals')
sns.countplot(goldMedals['Age'])
plt.show()

![Distribution of Gold Medals](https://user-images.githubusercontent.com/107674973/179981836-a88dd426-f581-43c8-844f-7f0a9ba90f21.png)

# Display of Silver Medals against age over time
plt.figure(figsize=(20, 10))
plt.title('Distribution of Silver Medals')
sns.countplot(silverMedals['Age'])
plt.show()

![Distribution of Silver Medals](https://user-images.githubusercontent.com/107674973/179982028-5dc5e78d-feb7-417c-856c-f8cd6a2058c2.png)

# Display of Bronze Medals against age over time
plt.figure(figsize=(20, 10))
plt.title('Distribution of Bronze Medals')
sns.countplot(bronzeMedals['Age'])
plt.show()

![Distribution of Bronze Medals](https://user-images.githubusercontent.com/107674973/179982138-81ab1ce9-5e45-414a-bc28-1252f49015fe.png)

# Creating an index on the left to determine the count of gold medals per country
TotalMedals = goldMedals.Team.value_counts().reset_index(name='Medal')

# Of these countries with Gold Medals, which are the top 10
TotalMedals10 = mydata.Team.value_counts().reset_index(name='Medal').head(10)
g = sns.catplot(x="index", y="Medal", data=TotalMedals10,
                height=13, kind="bar", palette="muted")
g.despine(left=True)
g.set_xlabels("Top 10 countries")
g.set_ylabels("Number of Medals")
plt.title('Total Medals per Country')
plt.show()

![Total Medals per country](https://user-images.githubusercontent.com/107674973/179982639-1c9472f4-2452-41b8-9343-77d34f7e9520.png)

# In the USA, which sports do they seem to be good at?

USASport = mydata['Sport'][mydata['Team'] == 'United States']
plt.figure(figsize=(30, 10))
plt.tight_layout()
sns.countplot(USASport)
plt.title('Medal Distribution for USA')
plt.xticks(rotation='90')
plt.show()

![USA Medals](https://user-images.githubusercontent.com/107674973/179982725-c4d4cbc1-cc19-463e-9445-2653153add72.png)

# Are men/women getting more athletic and physical as time goes on?
#First create a male dataframe, then female

MaleOverTime = mydata[(mydata.Sex == 'M')]
FemaleOverTime = mydata[(mydata.Sex == 'F')]

# Variation of Male Weight and Height over Time
plt.figure(figsize=(20, 10))
sns.boxplot('Year', 'Weight', data=MaleOverTime)
plt.title('Variation of Weight for Male Athletes over time')
# Now Height
plt.figure(figsize=(20, 10))
sns.boxplot('Year', 'Height', data=MaleOverTime)
plt.title('Variation of Height for Male Athletes over time')
![Variation of Weight for Male Athletes over time](https://user-images.githubusercontent.com/107674973/180006654-11cd7ed1-9caf-4e07-9d68-c09474ac5fc8.png)
![Variation of Height for Male Athletes over time](https://user-images.githubusercontent.com/107674973/180006619-fcba5878-cc67-4723-8aed-fd701e6a4024.png)

# Variation of Female Weight and Height over Time
plt.figure(figsize=(20, 10))
sns.boxplot('Year', 'Weight', data=FemaleOverTime)
plt.title('Variation of Weight for Female Athletes over Time')
plt.figure(figsize=(20, 10))
sns.boxplot('Year', 'Height', data=FemaleOverTime)
plt.title('Variation of Height for Female Athletes over Time')
![Variation of Weight for Female Athletes over Time](https://user-images.githubusercontent.com/107674973/180006856-a4f63a52-7d37-4efe-a4a3-21545cc78c88.png)
![Variation of Weight for Male Athletes over time](https://user-images.githubusercontent.com/107674973/180006871-c081bf95-44ba-4a6f-813a-88447bcb17db.png)

# Which sport has the heaviest athlete for?

mydata[['Weight']].max()
Weight    214.0
mydata[['Weight']].idxmax()
Weight    23155
HeavyAth = mydata.iloc[23155,:]
HeavyAth
ID                         12177
Name           Ricardo Blas, Jr.
Sex                            M
Age                         21.0
Height                     183.0
Weight                     214.0
Team                        Guam
NOC                          GUM
Games                2008 Summer
Year                        2008
Season                    Summer
City                     Beijing
Sport                       Judo
Event     Judo Men's Heavyweight
Medal                        NaN

# We see that Judo has had the heaviest athlete at 214 kgs! (Lord he heavy) Lets see the variation of Judo athletes over time

JudoAth = mydata[(mydata.Sport == 'Judo')]

plt.figure(figsize=(20, 10))
sns.stripplot('Year', 'Weight', data=JudoAth, palette='Set2')
plt.title('Variation of Weight for Athletes in Judo over time')
![Variation of Weight for Athletes in Judo over time](https://user-images.githubusercontent.com/107674973/180007346-38dc36ec-ca0a-4b01-ae86-ffa04dd9c854.png)



