# INTRODUCTION 
 ## Python Api and automation project 
in this project i used coinmrketcap API to pull crypto currency Data , the analysis mainly foucesed on the most famous cryptos 
- Bitcoin
- Tether (usdt)
- Etheruem
- BNB Samrt chain

# TOOLS and lIBRARES I USED 
- PYTHON  
- Jupyter Notebook
- API
- REQUESTS 
- PANDAS : Data manipulation library
- MATPLOTLIB : Data Visualization library
- SEABORN  : For Complex Visuals

# THE ANLYSIS :

- The analysis process started by Generating an API key from Coinmarketcap.com to pull the data
- Then used Requests ibrary to specify the parameters  to get 
specific data 
- then created a fuction for the pull request code
 ### The Script 
 ``` python
 from requests import Request, Session
from requests.exceptions import ConnectionError, Timeout, TooManyRedirects
import json

url = 'https://pro-api.coinmarketcap.com./v1/cryptocurrency/listings/latest'
parameters = {
  'start':'1',
  'limit':'15',
  'convert':'USD'
}
headers = {
  'Accepts': 'application/json',
  'X-CMC_PRO_API_KEY': '0d329fba-1910-4e7d-8ed3-7689bb45be33',
}

session = Session()
session.headers.update(headers)

try:
    response = session.get(url, params=parameters)
    data = json.loads(response.text)
    print(data)
except (ConnectionError, Timeout, TooManyRedirects) as e:
     print(e)
```
## The Function 
``` py
def api_call () :
    global df 
    url = 'https://pro-api.coinmarketcap.com./v1/cryptocurrency/listings/latest'
    parameters = {
     'start':'1',
     'limit':'15',
     'convert':'USD'
    }
    headers = {
      'Accepts': 'application/json',
      'X-CMC_PRO_API_KEY': '0d329fba-1910-4e7d-8ed3-7689bb45be33',
    }

    session = Session()
    session.headers.update(headers)

    try:
        response = session.get(url, params=parameters)
        data = json.loads(response.text)
        print(data)
    except (ConnectionError, Timeout, TooManyRedirects) as e:
            print(e)
            
    df2=pd.json_normalize(data['data'])
    df2['timestamp']=pd.to_datetime('now')
    df=df.append(df2)
    ## Creatin a csv file to Store The data
    
    if not os.path.isfile(r'F:\DATA ANALYSIS\portfolio projects\Python project\Api and automation project') :
        df.to_csv(r'F:\DATA ANALYSIS\portfolio projects\Python project\Api and automation project',header='column names')
    else :
        df.to_csv(r'F:\DATA ANALYSIS\portfolio projects\Python project\Api and automation project',mode='a',header=False)
  ```
    # the Automation Code 

 ``` py
 from time import sleep
for i in range(100):
    api_call()
    sleep(20)
exit()
``` 

## The analysis approaches are 
## 1. Descriptive Analysis

   #### Objective: To understand basic statistics and trends in the data.
   #### Key Metrics: 
  -   Price 
  -    Market capitalization
   -   Volume
   -   Circulating and total supply
    
### Analysis Techniques:
 -  Summary statistics  for each coin.
  -    Historical price trends: Line plots to visualize price movements over time.
   -   Market dominance: Percentage of market capitalization by a specific coin (e.g., Bitcoin dominance).
## 2. Time Series Analysis
   Objective: To analyze trends and patterns in cryptocurrency prices and volume over time.
   - Key Metrics: Historical prices, volumes, and market cap.
 #### Analysis Techniques:
  - patterns over specific time frames (daily, weekly, monthly).
## 3. Correlation Analysis
   Objective: To examine relationships between different cryptocurrencies or between cryptocurrencies and traditional financial markets (stocks, commodities).
  - Key Metrics: Prices of multiple cryptocurrencies.
### Analysis Techniques:
  - Correlation matrix: Compute correlation coefficients between different cryptocurrencies to see which coins move together.

  #

# Conclusion :



 

