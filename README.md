1 a) Data cleaning process
```
import pandas as pd
df=pd.read_csv("SAMPLEDS - Sheet1 (2).csv")
*
df.shape
*
df.dropna(how='any').shape
*
df.head()
*
df.tail()
*
x=df.dropna(how='any')
x
*
df.dropna(how='any').shape
*
df.dropna(how='all').shape
*
tot=df.dropna(subset=['TOTAL'],how='any')
tot
*
tot=df.dropna(subset=['M1','M2','M3','M4'],how='any')
tot
*
df.fillna(0)
*
df.fillna(method='ffill')
*
df.fillna(method='bfill')
*
m=df.TOTAL.mean()
m
*
df.TOTAL.fillna(m,inplace=True)
df
*
df.duplicated()
*
df.drop_duplicates(inplace=True)
df
*
df['cd']=pd.to_datetime(df['DOB'])
df
*
for x in df.index:
  if df.loc[x,"AVG"]>100:
    df.drop(x,inplace=True)
df
*
import seaborn as sns
sns.heatmap(df.isnull(),yticklabels=False,annot=True)


1 b) Multivariate analysis
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
*
dt = pd.read_csv("/content/titanic_dataset.csv")
dt
*
dt.set_index("PassengerId",inplace=True)
dt.describe()
*
dt.info()
*
dt["Survived"].value_counts()
*
per=(dt["Survived"].value_counts()/dt.shape[0]*100).round(2)
per
*
sns.catplot(x="Age",col="Survived",kind="count",data=dt)
*
fig,ax1=plt.subplots(figsize=(8,5))
graph = sns.countplot (ax=ax1,data=dt,x="Survived",hue="Pclass",palette="rainbow")
graph.set_xticklabels(graph.get_xticklabels())
for p in graph.patches:
  height = p.get_height()
  graph.text(p.get_x()+p.get_width()/2,height+20.8,height ,ha="left")
*
dt.boxplot(column="Age",by="Survived")
*
sns.scatterplot(x=dt["Age"],y=dt["Fare"])
*
sns.jointplot(x="Age",y="Fare",data=dt)
*
fig,ax1=plt.subplots(figsize=(8,5))
pt=sns.boxplot(ax=ax1,x='Pclass',y='Age',hue='Parch',data=dt)
*
sns.catplot(data=dt,col="Survived",x="Parch",hue='Pclass',kind="count")
*
g=sns.catplot(data=dt,col="Survived",x="Parch",hue="Pclass",kind ="count",legend=True)
g.fig.set_size_inches(8,5)
g.fig.subplots_adjust(top=0.81,right=0.86)
ax=g.facet_axis(0,0)
for p in ax.patches:
  ax.text(p.get_x()-0.01,p.get_height()*1.02,'{0:.1f}'.
  format(p.get_height()),color='red',rotation="horizontal",size="small")
*
corr = dt.corr()
sns.heatmap(corr,annot=True)
*
sns.pairplot(dt)


2 a) Outline removal
import pandas as pd
import seaborn as sns
*
age = [1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
*
sns.boxplot(data=af)
*
sns.scatterplot(data=af)
*
q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)
iqr=q3-q1
irq=af.quantile(0.5)
*
low=q1-1.5*iqr
low
*
high=q3+1.5*iqr
high
*
aq=af[((af>=low)&(af<=high))]
aq.dropna()
*
af=af[((af>=low)&(af<=high))]
af.dropna()
*
sns.boxplot(data=af)
*
sns.boxplot(data=af)
*
sns.scatterplot(data=af)
*
sns.scatterplot(data=af)


2 b) Univariate analyais
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
*
df=pd.read_csv("/content/iris (1).csv")
*
df.nunique()
*
df.head()
*
df.tail()
*
df.iloc[:,4].value_counts()
*
for i in range(0,df.shape[1]):
  print("-----------",df.columns[i],"------------")
  print(df.iloc[:,i].value_counts())
  print("---------------------------------------")
*
sns.countplot(x='species',data=df)
*
dfv=df.loc[df['species']=='virginica']

plt.plot(dfv['sepal_length'],np.zeros_like(dfv['sepal_length']),'*')
plt.xlabel('sepal length')
plt.show()
plt.plot(df_setosa['sepal_length'],np.zeros_like(df_setosa['sepal_length']),'o')
*
dfv=df.loc[df['species']=='virginica']

plt.plot(dfv['sepal_length'],np.zeros_like(dfv['sepal_length']),'*')
plt.xlabel('sepal length')
plt.show()
##plt.plot(df_setosa['sepal_length'],np.zeros_like(df_setosa['sepal_length']),'o')
*
dfs=df.loc[df['species']=='setosa']
dfc=df.loc[df['species']=='versicolor']

plt.plot(dfs['sepal_length'],np.zeros_like(dfs['sepal_length']),'*')
plt.plot(dfc['sepal_length'],np.zeros_like(dfc['sepal_length']),'X')
*
plt.plot(dfv['sepal_length'],np.zeros_like(dfv['sepal_length']),'o')
plt.plot(dfs['sepal_length'],np.zeros_like(dfs['sepal_length']),'*')
plt.plot(dfc['sepal_length'],np.zeros_like(dfc['sepal_length']),'X')
plt.xlabel('petal_length')
plt.show()
*
plt.plot(dfv['sepal_length'],np.zeros_like(dfv['sepal_length']),'o')
plt.plot(dfs['sepal_length'],np.zeros_like(dfs['sepal_length']),'+')
plt.plot(dfc['sepal_length'],np.zeros_like(dfc['sepal_length']),'-')
plt.xlabel('SEPALLENGTH')
plt.show()


3 a) Z score 

import pandas as pd
import numpy as np
import seaborn as sns
import pandas as pd
from scipy import stats
*
data = {'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
df=pd.DataFrame(data)
df
*
sns.boxplot(data=df)
*
z=np.abs(stats.zscore(df))
print(df[z['weight']>3])
*
val=[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,69,202,72,75,78,81,84,232,87,90,93,96,99,258]
df=pd.DataFrame(data)
*
out=[]
def d_o(val):
  ts=3
  m=np.mean(val)
  sd=np.std(val)
  for i in val:
    z=(i-m)/sd
    if np.abs(z)>ts:
      out.append(i)
  return out
*
op=d_o(val)
op
*
from scipy import stats
*
id=pd.read_csv("iris.csv")
id
*
sns.boxplot(x='sepal_width',data=id)
*
c1=id.sepal_width.quantile(0.25)
c3=id.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
*
rid=id[((id.sepal_width<(c1-1.5*iq))|(id.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
*
delid=id[~((id.sepal_width<(c1-1.5*iq))|(id.sepal_width>(c3+1.5*iq)))]
delid
*
sns.boxplot(x='sepal_width',data=delid)


3 b) feature generation
i) standard scaler:
import pandas as pd
from scipy import stats
import numpy as np
*
df=pd.read_csv("/content/bmi.csv")
*
from sklearn.preprocessing import StandardScaler
sc=StandardScaler()
df[['Height','Weight']]=sc.fit_transform(df[['Height','Weight']])
df.head(10)
*
ii) onehot encoder:
from sklearn.preprocessing import OneHotEncoder
*
ohe=OneHotEncoder(sparse=False)
ohe.fit_transform(df[["nom_0"]])
*
iii) robust scaler:
from sklearn.preprocessing import RobustScaler
rs=RobustScaler()
df=pd.DataFrame(rs.fit_transform(df),columns=['Height','Weight','Index'])
df


4 Data transformation
i) 2 methods in func transformation:
import pandas as pd
from scipy import stats
import numpy as np
*
df=pd.read_csv("/content/Data_to_Transform.csv")
df
*
df.skew()
*
np.log(df["Highly Positive Skew"])
*
np.reciprocal(df["Moderate Negative Skew"])
*
np.sqrt(df["Highly Positive Skew"])
*
np.square(df["Highly Positive Skew"])
*
df["Highly Positive Skew_boxcox"],parameter=stats.boxcox(df["Highly Positive Skew"])
df
*
df["Moderate Negative Skew_yeojohnson"],parameters=stats.yeojohnson(df["Moderate Negative Skew"])
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal')
*
df["Moderate Negative Skew_1"]=qt.fit_transform(df[["Moderate Negative Skew"]])
df
*
import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.api as sm
import scipy.stats as stats
*
sm.qqplot(df['Moderate Negative Skew'],line='45')
plt.show()
*
sm.qqplot(df['Moderate Negative Skew_1'],line='45')
plt.show()
*
df['Highly Negative Skew_1']=qt.fit_transform(df[["Highly Negative Skew"]])
sm.qqplot(df['Highly Negative Skew'],line='45')
plt.show()
*
sm.qqplot(df['Highly Negative Skew_1'],line='45')
plt.show()


5 Data visualization 1
i) bar chart in matplot and seaborn
import matplotlib.pyplot as plt
height=[10,24,36,40,5]
names=["one","two","three","four","five"]
c1=["red","green"]
c2=["b","g"]
plt.bar(names,height,width=0.8,color=c1)
plt.xlabel("x-axis")
plt.ylabel("y-axis")
plt.title("My Bar chart!!!!!!!!!!!!")
*
import seaborn as sns
tips= sns.load_dataset("tips")
avg_total_bill = tips.groupby("day")['total_bill'].mean()
avg_tip =tips.groupby('day')['tip'].mean()
plt.figure(figsize=(8, 6))
p1 = plt.bar(avg_total_bill.index, avg_total_bill, label='Total Bill')
p2 = plt.bar(avg_tip.index, avg_tip, bottom=avg_total_bill, label='Tip')
plt.xlabel('Day of the Week')
plt.ylabel('Amount')
plt.title("Average total bil and tip by day")
plt.legend()

ii) KDE plot:
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
*
mart = pd.read_csv("")
mart
*
mart = mart[['Gender','Payment','Unit price','Quantity','Total','gross income']]
mart.head(10)
*
sns.kdeplot(data=mart, x='Total')
*
sns.kdeplot(data=mart, x='Unit price')
*
sns.kdeplot(data=mart)
*
sns.kdeplot(data=mart,x='Total',hue='Payment',multiple='stack')



iii) violin plot:
sns.violinplot (x="day", y="total_bill", hue="smoker", data= tips, linewidth=2, width=0.6,)

iv) Heatmap:
data = np.random.randint(low = 1,high = 100,size = (10,10))
print("The data to be plotted:\n")
print(data)
*
hm = sns.heatmap(data = data)

6 Data visualization 2
i) Histogram:
import matplotlib.pyplot as plt
ages=[2,5,70,40,30,45,50,45,43,40,44,60,7,13,57,18,90,77,32,21,20,40]
range=(0,100)
bins=10
plt.hist(ages,bins,range,color="green",histtype="bar",rwidth=0.8)
plt.xlabel("age")
plt.ylabel("No.of.People")
plt.title("My Histogram")


ii) Scatter plot:
import matplotlib.pyplot as plt
x_values = [0,1,2,3,4,5]
y_values = [0,1,4,9,16,25]
plt.scatter (x_values, y_values, s=30, color="blue")
plt.show()
*
import seaborn as sns
tips = sns.load_dataset('tips')
sns.scatterplot(x= 'total_bill', y='tip', hue='sex',data=tips)
plt.xlabel('Total Bill')
plt.ylabel('Tip Amount')
plt.title('Scatter Plot of Total Bill vs. Tip Amount')

iii)Barplot:
import seaborn as sns
dt=sns.load_dataset("tips")
sns.barplot(x="day",y="total_bill",hue="sex",data=dt,palette="Set1")
plt.xlabel('Day of the Week')
plt.ylabel('Total bill')
plt.title("Total bill by day and gender")
