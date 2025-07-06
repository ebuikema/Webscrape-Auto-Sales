!pip install bs4
!pip install pandas
!pip install seaborn
!pip install requests
!pip install matplotlib

from bs4 import BeautifulSoup
import requests

url='https://en.wikipedia.org/wiki/List_of_automotive_manufacturers_by_production'

requests.get(url)

response=requests.get(url)

html=response.text

soup=BeautifulSoup(html,'html.parser')
print(html[:500])

soup.find('table')
soup.find_all('table')[7]
table_1=soup.find_all('table')[7]
table_1.find_all('th')
table_1.find_all('tr')

car_sales20_titles=table_1.find_all('th')
car_sales20_titles=[title.text.strip() for title in car_sales20_titles]

print(car_sales20_titles)

import pandas as pd

df=pd.DataFrame(columns=car_sales20_titles)
df

table_1.find_all('tr')

column_data = table_1.find_all('tr')
all_data = []
for row in column_data[1:]:
    row_data = row.find_all('td')
    ind_row_data = [data.text.strip() for data in row_data]
    if len(ind_row_data) == len(car_sales20_titles):
        all_data.append(ind_row_data)

df = pd.DataFrame(all_data, columns=car_sales20_titles)
df
