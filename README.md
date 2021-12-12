# Telco Customer Churn
Telco Customer Churn data is used to predict behavior to retain customers.

## EDA Process

### Initial EDA
'''
df=pd.read_csv('Telco Customer Churn.csv' ,encoding ='latin')
df.head()
'''
'''
for col in df.columns:
    print(f"Column: {col}")
    print(df[col].unique())
    print("="*10)
'''

