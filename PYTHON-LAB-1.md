## PYTHON-LAB-1
```
ДЛЯ ВЫПОЛНЕНИЯ ДАННОЙ ЛАБ.РАБОТЫ НЕОБХОДИМО:

1. - PYTHON ANACONDA
2. - Файл Lab_Python.ipynb
     (Инструкции по выполнению - написать 8 функций )
3. - Файл Python_materials.zip
     (дополнительные наборы данных)
```
```
import pandas as pd

df = pd.read_csv('olympics.csv', index_col=0, skiprows=1)

for col in df.columns:
    if col[:2]=='01':
        df.rename(columns={col:'Gold'+col[4:]}, inplace=True)
    if col[:2]=='02':
        df.rename(columns={col:'Silver'+col[4:]}, inplace=True)
    if col[:2]=='03':
        df.rename(columns={col:'Bronze'+col[4:]}, inplace=True)
    if col[:1]=='№':
        df.rename(columns={col:'#'+col[1:]}, inplace=True)

names_ids = df.index.str.split('\s\(') # split the index by '('

df.index = names_ids.str[0] # the [0] element is the country name (new index) 
df['ID'] = names_ids.str[1].str[:3] # the [1] element is the abbreviation or ID (take first 3 characters from that)

df = df.drop('Totals')
df.head()

# In[ ]:

GOLD_S = 'Gold'
GOLD_W = 'Gold.1'
GOLD_G = 'Gold.2'
SILVER_G = 'Silver.2'
BRONZE_G = 'Bronze.2'
POINTS = 'Points'
SUMLEV = "SUMLEV"
STNAME = 'STNAME'
CTYNAME = 'CTYNAME'
MIN = 'Min'
MAX = 'Max'
REGION = "REGION"
POPESTIMATE_ARRAY = ["POPESTIMATE2010", "POPESTIMATE2011", "POPESTIMATE2012", "POPESTIMATE2013", "POPESTIMATE2014", "POPESTIMATE2015"]

# In[ ]:
 #1. Which country has won the most gold medals in summer games?
 #This function should return a single string value.
def answer_one():
    return df.loc[df[GOLD_S].idxmax()].name
#In [4]: answer_one()
#Out[4]: 'United States'

# In[ ]:
# 2. Which country had the biggest difference between their summer and winter gold medal counts?
# This function should return a single string value.
def answer_two():    
   return (df[GOLD_S]-df[GOLD_W]).idxmax()
#In [5]: answer_two()
#Out[5]: 'United States'

# In[ ]:
#3.Which country has the biggest difference between their summer gold medal counts and winter gold medal 
#counts relative to their total gold medal count?
#\\frac{Summer~Gold - Winter~Gold}{Total~Gold}
    "Only include countries that have won at least 1 gold in both summer and winter.\n",
    "\n",
    "*This function should return a single string value.*"
def answer_three():
    copy_df = df.copy()
    copy_df = copy_df[(copy_df[GOLD_S]>0) & (copy_df[GOLD_W]>0)]
    return ((copy_df[GOLD_S]-copy_df[GOLD_W])/copy_df[GOLD_G]).idxmax()
# In [6]: answer_three()
# Out[6]: 'Bulgaria'

# In[ ]:
#4.Write a function that creates a Series called \"Points\" which is a weighted value where each gold medal 
#(`Gold.2`) counts for 3 points, silver medals (`Silver.2`) for 2 points, and bronze medals (`Bronze.2`) for 1 point. 
#The function should return only the column (a Series object) which you created.
#This function should return a Series named `Points` of length 146

def answer_four():
    df[POINTS] = df[GOLD_G]*3 + df[SILVER_G]*2 + df[BRONZE_G]
    return df[POINTS]

# In [7]: answer_four()
# Out[7]: 
# Afghanistan                            2
# Algeria                               27
# Argentina                            130
# Armenia                               16
# Australasia                           22
# Australia                            923
# Austria                              569
# Azerbaijan                            43
# Bahamas                               24
# Bahrain                                1
# Barbados                               1
# Belarus                              154
# Belgium                              276
# Bermuda                                1
# Bohemia                                5
# Botswana                               2
# Brazil                               184
# British West Indies                    2
# Bulgaria                             411
# Burundi                                3
# Cameroon                              12
# Canada                               846
# Chile                                 24
# China                               1120
# Colombia                              29
# Costa Rica                             7
# Ivory Coast                            2
# Croatia                               67
# Cuba                                 420
# Cyprus                                 2
#                                     ... 
# Spain                                268
# Sri Lanka                              4
# Sudan                                  2
# Suriname                               4
# Sweden                              1217
# Switzerland                          630
# Syria                                  6
# Chinese Taipei                        32
# Tajikistan                             4
# Tanzania                               4
# Thailand                              44
# Togo                                   1
# Tonga                                  2
# Trinidad and Tobago                   27
# Tunisia                               19
# Turkey                               191
# Uganda                                14
# Ukraine                              220
# United Arab Emirates                   3
# United States                       5684
# Uruguay                               16
# Uzbekistan                            38
# Venezuela                             18
# Vietnam                                4
# Virgin Islands                         2
# Yugoslavia                           171
# Independent Olympic Participants       4
# Zambia                                 3
# Zimbabwe                              18
# Mixed team                            38
# Name: Points, Length: 146, dtype: int64

# In[ ]:

census_df = pd.read_csv('census.csv')
census_df.head()

# In[ ]:
#5.Which state has the most counties in it? (hint: consider the sumlevel key carefully! You'll need this for future questions too...)
#This function should return a single string value.

def answer_five():
    return census_df[census_df[SUMLEV] == 50].groupby(STNAME)[CTYNAME].count().idxmax()

# In [8]: answer_five()
# Out[8]: 'Texas'

# In[ ]:
#6.Only looking at the three most populous counties for each state, what are the three most populous states 
#(in order of highest population to lowest population)? Use `CENSUS2010POP`.
#This function should return a list of string values.

def answer_six():
    return census_df[census_df[SUMLEV] == 50].groupby(STNAME)['CENSUS2010POP'].apply(lambda x: x.nlargest(3).sum()).nlargest(3).index.format()
 
# In [9]: answer_six()
# Out[9]: ['California', 'Texas', 'Illinois']

# In[ ]:
#7.Which county has had the largest absolute change in population within the period 2010-2015? (Hint: population values are 
#stored in columns POPESTIMATE2010 through POPESTIMATE2015, you need to consider all six columns.)
#e.g. If County Population in the 5 year period is 100, 120, 80, 105, 100, 130, then its largest change in the period 
#would be |130-80| = 50.
#This function should return a single string value.

def answer_seven():
    census_df[MIN] = census_df.loc[census_df[SUMLEV] == 50, POPESTIMATE_ARRAY].min(axis=1)
    census_df[MAX] = census_df.loc[census_df[SUMLEV] == 50, POPESTIMATE_ARRAY].max(axis=1)
    census_df["PopGrowth"] = census_df[MAX] - census_df[MIN]
    return census_df.loc[census_df["PopGrowth"] == census_df["PopGrowth"].max(), CTYNAME].max()

# In [10]: answer_seven()
# Out[10]: 'Harris County'

# In[ ]:
#In this datafile, the United States is broken up into four regions using the \"REGION\" column.
#Create a query that finds the counties that belong to regions 1 or 2, whose name starts with 'Washington', 
#and whose POPESTIMATE2015 was greater than their POPESTIMATE 2014.
#This function should return a 5x2 DataFrame with the columns = ['STNAME', 'CTYNAME'] and the same index ID 
#as the census_df (sorted ascending by index).

def answer_eight():
    return census_df.loc[((census_df[REGION] == 1) | (census_df[REGION] == 2)) & (census_df[CTYNAME].str.startswith('Washington')) & (census_df[POPESTIMATE_ARRAY[4]] > census_df[POPESTIMATE_ARRAY[4]]), [STNAME, CTYNAME]]

# In [13]: answer_eight()
# Out[13]: 
#             STNAME            CTYNAME
# 896           Iowa  Washington County
# 1419     Minnesota  Washington County
# 2345  Pennsylvania  Washington County
# 2355  Rhode Island  Washington County
# 3163     Wisconsin  Washington County
```
