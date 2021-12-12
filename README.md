# Telco Customer Churn
Telco Customer Churn data is used to predict behavior to retain customers.

## EDA Process

### Initial EDA
Find any unique value in each column
```
for col in df.columns:
    print(f"Column: {col}")
    print(df[col].unique())
    print("="*10)
```
Change the value & data type of each column
```
df['TotalCharges']= df['TotalCharges'].apply(lambda x:0 if x==' ' else x)
df['TotalCharges']= df['TotalCharges'].astype(float)
```
Describe the statistics of each column
```
df.describe()
```

### Drop Column
```
df = df.drop(columns = ['customerID'])
```

### Target Feauture Analysis
```
df['Churn'].value_counts().plot(kind='bar')
plt.title('Churn Distribution')
plt.show()
```
```
df['Churn'].value_counts(True).plot(kind='bar')
plt.title('Churn Distribution')
plt.show()
```

### Correlation Analysis
```
df_corr = df.corr()
df_corr
```
Making heatmap using Pearson Correlation Heatmap
```
df_corr = df.corr()
mask = np.zeros_like(df_corr)
mask[np.triu_indices_from(mask)] = True

fig, ax = plt.subplots(figsize=(15, 12))
ax = sns.heatmap(df_corr,mask=mask, 
                 annot=True, annot_kws={'size':10}, fmt=".2f")
plt.title("Telco Customer Churn (Pearson Correlation Heatmap)")
plt.show()
```

### TotalCharges Outlier Analysis
```
df['TotalCharges'].plot(kind='box',figsize=(10,8))
plt.title("TotalCharges Boxplot")
plt.show()
```

### Services Analysis
Grouping InternetService column
```
df.groupby(['InternetService'])[['Churn']].agg({'count','mean'})
```
Grouping all the services that using internet service
```
df_services_analysis = df.copy()
df_services_analysis['services'] = df_services_analysis.apply(lambda x: 'OS' if x['OnlineSecurity']==1 else
                                                    'OB' if x['OnlineBackup']==1 else
                                                    'DP' if x['DeviceProtection']==1 else
                                                    'TS' if x['TechSupport']==1 else
                                                    'ST' if x['StreamingTV']==1 else
                                                    'SM'
                                        ,axis=1)
```
```
df_services_analysis.groupby(['services'])[['Churn']].agg({'count','mean'})
```

### Demographic Analysis
Grouping SeniorCitizen & Partner column
```
df.groupby(['SeniorCitizen','Partner'])[['Churn']].agg({'count','mean'})
```
Grouping SeniorCitizen & Dependents column
```
df.groupby(['SeniorCitizen','Dependents'])[['Churn']].agg({'count','mean'})
```

### Customer Account Analysis
Grouping all the services that using internet service by Contract & Churn column
```
df_services_analysis.groupby(['Contract'])[['Churn']].agg({'count','mean'})
```
Grouping all the services that using internet service by PaperlessBilling, PaymentMethod & Churn column
```
df_services_analysis.groupby(['PaperlessBilling','PaymentMethod'])[['Churn']].agg({'count','mean'})
```

## Source
[Data Telco Customer Churn](https://www.kaggle.com/blastchar/telco-customer-churn)
