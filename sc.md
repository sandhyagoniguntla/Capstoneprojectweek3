```python
##**Assignment: Segmenting and Clustering Neighborhoods in Toronto webscraping the data**
```


```python
import sys
!{sys.executable} --version
```

    Python 3.6.7



```python
!pip --version
```

    pip 19.1.1 from /home/jupyterlab/conda/envs/python/lib/python3.6/site-packages/pip (python 3.6)



```python
## installing beautifulsoup
```


```python
!pip install beautifulsoup4
```

    Collecting beautifulsoup4
    [?25l  Downloading https://files.pythonhosted.org/packages/cb/a1/c698cf319e9cfed6b17376281bd0efc6bfc8465698f54170ef60a485ab5d/beautifulsoup4-4.8.2-py3-none-any.whl (106kB)
    [K     |████████████████████████████████| 112kB 28.3MB/s eta 0:00:01
    [?25hCollecting soupsieve>=1.2 (from beautifulsoup4)
      Downloading https://files.pythonhosted.org/packages/81/94/03c0f04471fc245d08d0a99f7946ac228ca98da4fa75796c507f61e688c2/soupsieve-1.9.5-py2.py3-none-any.whl
    Installing collected packages: soupsieve, beautifulsoup4
    Successfully installed beautifulsoup4-4.8.2 soupsieve-1.9.5



```python
# *importing packages bs4,beautifulSoup,requests and pandas*
```


```python
import bs4
from bs4 import BeautifulSoup
import requests
import pandas as pd
```


```python
# *web scraing the table data  from the website link using BeautifulSoup*
```


```python
source=requests.get('https://en.wikipedia.org/wiki/List_of_postal_codes_of_Canada:_M').text
soup= BeautifulSoup(source,'html5lib')
table=soup.find('table',class_='wikitable sortable')
table_rows=table.find_all('tr')
# assigning columns
d_key=['name','borough','neighborhood']
da=[]
for tr in table_rows :
    t_row = {}
    for td, th in zip(tr.find_all("td"), d_key):
            t_row[th] = td.text.replace('\n', '').strip()
    da.append(t_row)

```


```python
len(da)
```




    288




```python
da.pop(0)
```




    {}




```python
# total no.of rows from data is 287
```


```python
len(da)
```




    287




```python
# *ignoring the rows  where borough='not assigned'*
```


```python
my_list=[i for i in da if not(i['borough']=='Not assigned')]
print(my_list)
```

    [{'name': 'M3A', 'borough': 'North York', 'neighborhood': 'Parkwoods'}, {'name': 'M4A', 'borough': 'North York', 'neighborhood': 'Victoria Village'}, {'name': 'M5A', 'borough': 'Downtown Toronto', 'neighborhood': 'Harbourfront'}, {'name': 'M6A', 'borough': 'North York', 'neighborhood': 'Lawrence Heights'}, {'name': 'M6A', 'borough': 'North York', 'neighborhood': 'Lawrence Manor'}, {'name': 'M7A', 'borough': 'Downtown Toronto', 'neighborhood': "Queen's Park"}, {'name': 'M9A', 'borough': "Queen's Park", 'neighborhood': 'Not assigned'}, {'name': 'M1B', 'borough': 'Scarborough', 'neighborhood': 'Rouge'}, {'name': 'M1B', 'borough': 'Scarborough', 'neighborhood': 'Malvern'}, {'name': 'M3B', 'borough': 'North York', 'neighborhood': 'Don Mills North'}, {'name': 'M4B', 'borough': 'East York', 'neighborhood': 'Woodbine Gardens'}, {'name': 'M4B', 'borough': 'East York', 'neighborhood': 'Parkview Hill'}, {'name': 'M5B', 'borough': 'Downtown Toronto', 'neighborhood': 'Ryerson'}, {'name': 'M5B', 'borough': 'Downtown Toronto', 'neighborhood': 'Garden District'}, {'name': 'M6B', 'borough': 'North York', 'neighborhood': 'Glencairn'}, {'name': 'M9B', 'borough': 'Etobicoke', 'neighborhood': 'Cloverdale'}, {'name': 'M9B', 'borough': 'Etobicoke', 'neighborhood': 'Islington'}, {'name': 'M9B', 'borough': 'Etobicoke', 'neighborhood': 'Martin Grove'}, {'name': 'M9B', 'borough': 'Etobicoke', 'neighborhood': 'Princess Gardens'}, {'name': 'M9B', 'borough': 'Etobicoke', 'neighborhood': 'West Deane Park'}, {'name': 'M1C', 'borough': 'Scarborough', 'neighborhood': 'Highland Creek'}, {'name': 'M1C', 'borough': 'Scarborough', 'neighborhood': 'Rouge Hill'}, {'name': 'M1C', 'borough': 'Scarborough', 'neighborhood': 'Port Union'}, {'name': 'M3C', 'borough': 'North York', 'neighborhood': 'Flemingdon Park'}, {'name': 'M3C', 'borough': 'North York', 'neighborhood': 'Don Mills South'}, {'name': 'M4C', 'borough': 'East York', 'neighborhood': 'Woodbine Heights'}, {'name': 'M5C', 'borough': 'Downtown Toronto', 'neighborhood': 'St. James Town'}, {'name': 'M6C', 'borough': 'York', 'neighborhood': 'Humewood-Cedarvale'}, {'name': 'M9C', 'borough': 'Etobicoke', 'neighborhood': 'Bloordale Gardens'}, {'name': 'M9C', 'borough': 'Etobicoke', 'neighborhood': 'Eringate'}, {'name': 'M9C', 'borough': 'Etobicoke', 'neighborhood': 'Markland Wood'}, {'name': 'M9C', 'borough': 'Etobicoke', 'neighborhood': 'Old Burnhamthorpe'}, {'name': 'M1E', 'borough': 'Scarborough', 'neighborhood': 'Guildwood'}, {'name': 'M1E', 'borough': 'Scarborough', 'neighborhood': 'Morningside'}, {'name': 'M1E', 'borough': 'Scarborough', 'neighborhood': 'West Hill'}, {'name': 'M4E', 'borough': 'East Toronto', 'neighborhood': 'The Beaches'}, {'name': 'M5E', 'borough': 'Downtown Toronto', 'neighborhood': 'Berczy Park'}, {'name': 'M6E', 'borough': 'York', 'neighborhood': 'Caledonia-Fairbanks'}, {'name': 'M1G', 'borough': 'Scarborough', 'neighborhood': 'Woburn'}, {'name': 'M4G', 'borough': 'East York', 'neighborhood': 'Leaside'}, {'name': 'M5G', 'borough': 'Downtown Toronto', 'neighborhood': 'Central Bay Street'}, {'name': 'M6G', 'borough': 'Downtown Toronto', 'neighborhood': 'Christie'}, {'name': 'M1H', 'borough': 'Scarborough', 'neighborhood': 'Cedarbrae'}, {'name': 'M2H', 'borough': 'North York', 'neighborhood': 'Hillcrest Village'}, {'name': 'M3H', 'borough': 'North York', 'neighborhood': 'Bathurst Manor'}, {'name': 'M3H', 'borough': 'North York', 'neighborhood': 'Downsview North'}, {'name': 'M3H', 'borough': 'North York', 'neighborhood': 'Wilson Heights'}, {'name': 'M4H', 'borough': 'East York', 'neighborhood': 'Thorncliffe Park'}, {'name': 'M5H', 'borough': 'Downtown Toronto', 'neighborhood': 'Adelaide'}, {'name': 'M5H', 'borough': 'Downtown Toronto', 'neighborhood': 'King'}, {'name': 'M5H', 'borough': 'Downtown Toronto', 'neighborhood': 'Richmond'}, {'name': 'M6H', 'borough': 'West Toronto', 'neighborhood': 'Dovercourt Village'}, {'name': 'M6H', 'borough': 'West Toronto', 'neighborhood': 'Dufferin'}, {'name': 'M1J', 'borough': 'Scarborough', 'neighborhood': 'Scarborough Village'}, {'name': 'M2J', 'borough': 'North York', 'neighborhood': 'Fairview'}, {'name': 'M2J', 'borough': 'North York', 'neighborhood': 'Henry Farm'}, {'name': 'M2J', 'borough': 'North York', 'neighborhood': 'Oriole'}, {'name': 'M3J', 'borough': 'North York', 'neighborhood': 'Northwood Park'}, {'name': 'M3J', 'borough': 'North York', 'neighborhood': 'York University'}, {'name': 'M4J', 'borough': 'East York', 'neighborhood': 'East Toronto'}, {'name': 'M5J', 'borough': 'Downtown Toronto', 'neighborhood': 'Harbourfront East'}, {'name': 'M5J', 'borough': 'Downtown Toronto', 'neighborhood': 'Toronto Islands'}, {'name': 'M5J', 'borough': 'Downtown Toronto', 'neighborhood': 'Union Station'}, {'name': 'M6J', 'borough': 'West Toronto', 'neighborhood': 'Little Portugal'}, {'name': 'M6J', 'borough': 'West Toronto', 'neighborhood': 'Trinity'}, {'name': 'M1K', 'borough': 'Scarborough', 'neighborhood': 'East Birchmount Park'}, {'name': 'M1K', 'borough': 'Scarborough', 'neighborhood': 'Ionview'}, {'name': 'M1K', 'borough': 'Scarborough', 'neighborhood': 'Kennedy Park'}, {'name': 'M2K', 'borough': 'North York', 'neighborhood': 'Bayview Village'}, {'name': 'M3K', 'borough': 'North York', 'neighborhood': 'CFB Toronto'}, {'name': 'M3K', 'borough': 'North York', 'neighborhood': 'Downsview East'}, {'name': 'M4K', 'borough': 'East Toronto', 'neighborhood': 'The Danforth West'}, {'name': 'M4K', 'borough': 'East Toronto', 'neighborhood': 'Riverdale'}, {'name': 'M5K', 'borough': 'Downtown Toronto', 'neighborhood': 'Design Exchange'}, {'name': 'M5K', 'borough': 'Downtown Toronto', 'neighborhood': 'Toronto Dominion Centre'}, {'name': 'M6K', 'borough': 'West Toronto', 'neighborhood': 'Brockton'}, {'name': 'M6K', 'borough': 'West Toronto', 'neighborhood': 'Exhibition Place'}, {'name': 'M6K', 'borough': 'West Toronto', 'neighborhood': 'Parkdale Village'}, {'name': 'M1L', 'borough': 'Scarborough', 'neighborhood': 'Clairlea'}, {'name': 'M1L', 'borough': 'Scarborough', 'neighborhood': 'Golden Mile'}, {'name': 'M1L', 'borough': 'Scarborough', 'neighborhood': 'Oakridge'}, {'name': 'M2L', 'borough': 'North York', 'neighborhood': 'Silver Hills'}, {'name': 'M2L', 'borough': 'North York', 'neighborhood': 'York Mills'}, {'name': 'M3L', 'borough': 'North York', 'neighborhood': 'Downsview West'}, {'name': 'M4L', 'borough': 'East Toronto', 'neighborhood': 'The Beaches West'}, {'name': 'M4L', 'borough': 'East Toronto', 'neighborhood': 'India Bazaar'}, {'name': 'M5L', 'borough': 'Downtown Toronto', 'neighborhood': 'Commerce Court'}, {'name': 'M5L', 'borough': 'Downtown Toronto', 'neighborhood': 'Victoria Hotel'}, {'name': 'M6L', 'borough': 'North York', 'neighborhood': 'Downsview'}, {'name': 'M6L', 'borough': 'North York', 'neighborhood': 'North Park'}, {'name': 'M6L', 'borough': 'North York', 'neighborhood': 'Upwood Park'}, {'name': 'M9L', 'borough': 'North York', 'neighborhood': 'Humber Summit'}, {'name': 'M1M', 'borough': 'Scarborough', 'neighborhood': 'Cliffcrest'}, {'name': 'M1M', 'borough': 'Scarborough', 'neighborhood': 'Cliffside'}, {'name': 'M1M', 'borough': 'Scarborough', 'neighborhood': 'Scarborough Village West'}, {'name': 'M2M', 'borough': 'North York', 'neighborhood': 'Newtonbrook'}, {'name': 'M2M', 'borough': 'North York', 'neighborhood': 'Willowdale'}, {'name': 'M3M', 'borough': 'North York', 'neighborhood': 'Downsview Central'}, {'name': 'M4M', 'borough': 'East Toronto', 'neighborhood': 'Studio District'}, {'name': 'M5M', 'borough': 'North York', 'neighborhood': 'Bedford Park'}, {'name': 'M5M', 'borough': 'North York', 'neighborhood': 'Lawrence Manor East'}, {'name': 'M6M', 'borough': 'York', 'neighborhood': 'Del Ray'}, {'name': 'M6M', 'borough': 'York', 'neighborhood': 'Keelesdale'}, {'name': 'M6M', 'borough': 'York', 'neighborhood': 'Mount Dennis'}, {'name': 'M6M', 'borough': 'York', 'neighborhood': 'Silverthorn'}, {'name': 'M9M', 'borough': 'North York', 'neighborhood': 'Emery'}, {'name': 'M9M', 'borough': 'North York', 'neighborhood': 'Humberlea'}, {'name': 'M1N', 'borough': 'Scarborough', 'neighborhood': 'Birch Cliff'}, {'name': 'M1N', 'borough': 'Scarborough', 'neighborhood': 'Cliffside West'}, {'name': 'M2N', 'borough': 'North York', 'neighborhood': 'Willowdale South'}, {'name': 'M3N', 'borough': 'North York', 'neighborhood': 'Downsview Northwest'}, {'name': 'M4N', 'borough': 'Central Toronto', 'neighborhood': 'Lawrence Park'}, {'name': 'M5N', 'borough': 'Central Toronto', 'neighborhood': 'Roselawn'}, {'name': 'M6N', 'borough': 'York', 'neighborhood': 'The Junction North'}, {'name': 'M6N', 'borough': 'York', 'neighborhood': 'Runnymede'}, {'name': 'M9N', 'borough': 'York', 'neighborhood': 'Weston'}, {'name': 'M1P', 'borough': 'Scarborough', 'neighborhood': 'Dorset Park'}, {'name': 'M1P', 'borough': 'Scarborough', 'neighborhood': 'Scarborough Town Centre'}, {'name': 'M1P', 'borough': 'Scarborough', 'neighborhood': 'Wexford Heights'}, {'name': 'M2P', 'borough': 'North York', 'neighborhood': 'York Mills West'}, {'name': 'M4P', 'borough': 'Central Toronto', 'neighborhood': 'Davisville North'}, {'name': 'M5P', 'borough': 'Central Toronto', 'neighborhood': 'Forest Hill North'}, {'name': 'M5P', 'borough': 'Central Toronto', 'neighborhood': 'Forest Hill West'}, {'name': 'M6P', 'borough': 'West Toronto', 'neighborhood': 'High Park'}, {'name': 'M6P', 'borough': 'West Toronto', 'neighborhood': 'The Junction South'}, {'name': 'M9P', 'borough': 'Etobicoke', 'neighborhood': 'Westmount'}, {'name': 'M1R', 'borough': 'Scarborough', 'neighborhood': 'Maryvale'}, {'name': 'M1R', 'borough': 'Scarborough', 'neighborhood': 'Wexford'}, {'name': 'M2R', 'borough': 'North York', 'neighborhood': 'Willowdale West'}, {'name': 'M4R', 'borough': 'Central Toronto', 'neighborhood': 'North Toronto West'}, {'name': 'M5R', 'borough': 'Central Toronto', 'neighborhood': 'The Annex'}, {'name': 'M5R', 'borough': 'Central Toronto', 'neighborhood': 'North Midtown'}, {'name': 'M5R', 'borough': 'Central Toronto', 'neighborhood': 'Yorkville'}, {'name': 'M6R', 'borough': 'West Toronto', 'neighborhood': 'Parkdale'}, {'name': 'M6R', 'borough': 'West Toronto', 'neighborhood': 'Roncesvalles'}, {'name': 'M7R', 'borough': 'Mississauga', 'neighborhood': 'Canada Post Gateway Processing Centre'}, {'name': 'M9R', 'borough': 'Etobicoke', 'neighborhood': 'Kingsview Village'}, {'name': 'M9R', 'borough': 'Etobicoke', 'neighborhood': 'Martin Grove Gardens'}, {'name': 'M9R', 'borough': 'Etobicoke', 'neighborhood': 'Richview Gardens'}, {'name': 'M9R', 'borough': 'Etobicoke', 'neighborhood': 'St. Phillips'}, {'name': 'M1S', 'borough': 'Scarborough', 'neighborhood': 'Agincourt'}, {'name': 'M4S', 'borough': 'Central Toronto', 'neighborhood': 'Davisville'}, {'name': 'M5S', 'borough': 'Downtown Toronto', 'neighborhood': 'Harbord'}, {'name': 'M5S', 'borough': 'Downtown Toronto', 'neighborhood': 'University of Toronto'}, {'name': 'M6S', 'borough': 'West Toronto', 'neighborhood': 'Runnymede'}, {'name': 'M6S', 'borough': 'West Toronto', 'neighborhood': 'Swansea'}, {'name': 'M1T', 'borough': 'Scarborough', 'neighborhood': 'Clarks Corners'}, {'name': 'M1T', 'borough': 'Scarborough', 'neighborhood': 'Sullivan'}, {'name': 'M1T', 'borough': 'Scarborough', 'neighborhood': "Tam O'Shanter"}, {'name': 'M4T', 'borough': 'Central Toronto', 'neighborhood': 'Moore Park'}, {'name': 'M4T', 'borough': 'Central Toronto', 'neighborhood': 'Summerhill East'}, {'name': 'M5T', 'borough': 'Downtown Toronto', 'neighborhood': 'Chinatown'}, {'name': 'M5T', 'borough': 'Downtown Toronto', 'neighborhood': 'Grange Park'}, {'name': 'M5T', 'borough': 'Downtown Toronto', 'neighborhood': 'Kensington Market'}, {'name': 'M1V', 'borough': 'Scarborough', 'neighborhood': 'Agincourt North'}, {'name': 'M1V', 'borough': 'Scarborough', 'neighborhood': "L'Amoreaux East"}, {'name': 'M1V', 'borough': 'Scarborough', 'neighborhood': 'Milliken'}, {'name': 'M1V', 'borough': 'Scarborough', 'neighborhood': 'Steeles East'}, {'name': 'M4V', 'borough': 'Central Toronto', 'neighborhood': 'Deer Park'}, {'name': 'M4V', 'borough': 'Central Toronto', 'neighborhood': 'Forest Hill SE'}, {'name': 'M4V', 'borough': 'Central Toronto', 'neighborhood': 'Rathnelly'}, {'name': 'M4V', 'borough': 'Central Toronto', 'neighborhood': 'South Hill'}, {'name': 'M4V', 'borough': 'Central Toronto', 'neighborhood': 'Summerhill West'}, {'name': 'M5V', 'borough': 'Downtown Toronto', 'neighborhood': 'CN Tower'}, {'name': 'M5V', 'borough': 'Downtown Toronto', 'neighborhood': 'Bathurst Quay'}, {'name': 'M5V', 'borough': 'Downtown Toronto', 'neighborhood': 'Island airport'}, {'name': 'M5V', 'borough': 'Downtown Toronto', 'neighborhood': 'Harbourfront West'}, {'name': 'M5V', 'borough': 'Downtown Toronto', 'neighborhood': 'King and Spadina'}, {'name': 'M5V', 'borough': 'Downtown Toronto', 'neighborhood': 'Railway Lands'}, {'name': 'M5V', 'borough': 'Downtown Toronto', 'neighborhood': 'South Niagara'}, {'name': 'M8V', 'borough': 'Etobicoke', 'neighborhood': 'Humber Bay Shores'}, {'name': 'M8V', 'borough': 'Etobicoke', 'neighborhood': 'Mimico South'}, {'name': 'M8V', 'borough': 'Etobicoke', 'neighborhood': 'New Toronto'}, {'name': 'M9V', 'borough': 'Etobicoke', 'neighborhood': 'Albion Gardens'}, {'name': 'M9V', 'borough': 'Etobicoke', 'neighborhood': 'Beaumond Heights'}, {'name': 'M9V', 'borough': 'Etobicoke', 'neighborhood': 'Humbergate'}, {'name': 'M9V', 'borough': 'Etobicoke', 'neighborhood': 'Jamestown'}, {'name': 'M9V', 'borough': 'Etobicoke', 'neighborhood': 'Mount Olive'}, {'name': 'M9V', 'borough': 'Etobicoke', 'neighborhood': 'Silverstone'}, {'name': 'M9V', 'borough': 'Etobicoke', 'neighborhood': 'South Steeles'}, {'name': 'M9V', 'borough': 'Etobicoke', 'neighborhood': 'Thistletown'}, {'name': 'M1W', 'borough': 'Scarborough', 'neighborhood': "L'Amoreaux West"}, {'name': 'M4W', 'borough': 'Downtown Toronto', 'neighborhood': 'Rosedale'}, {'name': 'M5W', 'borough': 'Downtown Toronto', 'neighborhood': 'Stn A PO Boxes 25 The Esplanade'}, {'name': 'M8W', 'borough': 'Etobicoke', 'neighborhood': 'Alderwood'}, {'name': 'M8W', 'borough': 'Etobicoke', 'neighborhood': 'Long Branch'}, {'name': 'M9W', 'borough': 'Etobicoke', 'neighborhood': 'Northwest'}, {'name': 'M1X', 'borough': 'Scarborough', 'neighborhood': 'Upper Rouge'}, {'name': 'M4X', 'borough': 'Downtown Toronto', 'neighborhood': 'Cabbagetown'}, {'name': 'M4X', 'borough': 'Downtown Toronto', 'neighborhood': 'St. James Town'}, {'name': 'M5X', 'borough': 'Downtown Toronto', 'neighborhood': 'First Canadian Place'}, {'name': 'M5X', 'borough': 'Downtown Toronto', 'neighborhood': 'Underground city'}, {'name': 'M8X', 'borough': 'Etobicoke', 'neighborhood': 'The Kingsway'}, {'name': 'M8X', 'borough': 'Etobicoke', 'neighborhood': 'Montgomery Road'}, {'name': 'M8X', 'borough': 'Etobicoke', 'neighborhood': 'Old Mill North'}, {'name': 'M4Y', 'borough': 'Downtown Toronto', 'neighborhood': 'Church and Wellesley'}, {'name': 'M7Y', 'borough': 'East Toronto', 'neighborhood': 'Business Reply Mail Processing Centre 969 Eastern'}, {'name': 'M8Y', 'borough': 'Etobicoke', 'neighborhood': 'Humber Bay'}, {'name': 'M8Y', 'borough': 'Etobicoke', 'neighborhood': "King's Mill Park"}, {'name': 'M8Y', 'borough': 'Etobicoke', 'neighborhood': 'Kingsway Park South East'}, {'name': 'M8Y', 'borough': 'Etobicoke', 'neighborhood': 'Mimico NE'}, {'name': 'M8Y', 'borough': 'Etobicoke', 'neighborhood': 'Old Mill South'}, {'name': 'M8Y', 'borough': 'Etobicoke', 'neighborhood': 'The Queensway East'}, {'name': 'M8Y', 'borough': 'Etobicoke', 'neighborhood': 'Royal York South East'}, {'name': 'M8Y', 'borough': 'Etobicoke', 'neighborhood': 'Sunnylea'}, {'name': 'M8Z', 'borough': 'Etobicoke', 'neighborhood': 'Kingsway Park South West'}, {'name': 'M8Z', 'borough': 'Etobicoke', 'neighborhood': 'Mimico NW'}, {'name': 'M8Z', 'borough': 'Etobicoke', 'neighborhood': 'The Queensway West'}, {'name': 'M8Z', 'borough': 'Etobicoke', 'neighborhood': 'Royal York South West'}, {'name': 'M8Z', 'borough': 'Etobicoke', 'neighborhood': 'South of Bloor'}]



```python
# number of rows after ignoring the borough='Not assigned' is 210
```


```python
len(my_list)
```




    210




```python
#*selecting rows where neighborhood='not asssigned 'and changing the value*
```


```python
my_list1=[i for i in my_list if(i['neighborhood']=='Not assigned')]

print(my_list1)
```

    [{'name': 'M9A', 'borough': "Queen's Park", 'neighborhood': 'Not assigned'}]



```python
for list1 in my_list1:
    dic=list1
    for key, value in dic.items():
     if( value == "Not assigned"):
        dic.pop(key,'Not assigned')
        dic[key] =dic['borough']
print (dic)

```

    {'name': 'M9A', 'borough': "Queen's Park", 'neighborhood': "Queen's Park"}



```python
# *appending the changed rows to the list of rows and converting to a dataframe*
```


```python
my_list.append(dic)
```


```python
import pandas as pd
df=pd.DataFrame(my_list)
#df.shape
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>borough</th>
      <th>neighborhood</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M3A</td>
      <td>North York</td>
      <td>Parkwoods</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M4A</td>
      <td>North York</td>
      <td>Victoria Village</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M5A</td>
      <td>Downtown Toronto</td>
      <td>Harbourfront</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M6A</td>
      <td>North York</td>
      <td>Lawrence Heights</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M6A</td>
      <td>North York</td>
      <td>Lawrence Manor</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.shape
```




    (211, 3)




```python
# *checking for duplicate rows in dataframe*
```


```python
print (any(df.neighborhood =="Not assigned"))
       #true if it contains
```

    False



```python
#sorting the dataframe based on name and borough
```


```python
df2=(df.sort_values(by=['name','borough'],inplace=False)).reset_index(drop=True)
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>borough</th>
      <th>neighborhood</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M1B</td>
      <td>Scarborough</td>
      <td>Rouge</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M1B</td>
      <td>Scarborough</td>
      <td>Malvern</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M1C</td>
      <td>Scarborough</td>
      <td>Highland Creek</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M1C</td>
      <td>Scarborough</td>
      <td>Rouge Hill</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M1C</td>
      <td>Scarborough</td>
      <td>Port Union</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>206</th>
      <td>M9V</td>
      <td>Etobicoke</td>
      <td>Mount Olive</td>
    </tr>
    <tr>
      <th>207</th>
      <td>M9V</td>
      <td>Etobicoke</td>
      <td>Silverstone</td>
    </tr>
    <tr>
      <th>208</th>
      <td>M9V</td>
      <td>Etobicoke</td>
      <td>South Steeles</td>
    </tr>
    <tr>
      <th>209</th>
      <td>M9V</td>
      <td>Etobicoke</td>
      <td>Thistletown</td>
    </tr>
    <tr>
      <th>210</th>
      <td>M9W</td>
      <td>Etobicoke</td>
      <td>Northwest</td>
    </tr>
  </tbody>
</table>
<p>211 rows × 3 columns</p>
</div>




```python
# *grouping the dataframe based on name and borough and printing the groups*
```


```python
grouped = df2.groupby(['name', 'borough'], as_index=False)
print(grouped.count())
```

        name      borough  neighborhood
    0    M1B  Scarborough             2
    1    M1C  Scarborough             3
    2    M1E  Scarborough             3
    3    M1G  Scarborough             1
    4    M1H  Scarborough             1
    ..   ...          ...           ...
    98   M9N         York             1
    99   M9P    Etobicoke             1
    100  M9R    Etobicoke             4
    101  M9V    Etobicoke             8
    102  M9W    Etobicoke             1

    [103 rows x 3 columns]



```python
# *converting the groups neighborhood columns with more than one neighborhood and appending it to list*
```


```python
newls=[]
neigh=[]
i=0
newstr=""
while(i<103):

    for key, group in grouped:
         #print("key:",key,"group:",list(group['neighborhood']) )
         neigh=list(group['neighborhood'])
         #print(neigh)
         newstr=','.join(str(x) for x in (list(group['neighborhood'])))
         #print(newstr)
         L1=list(key)
         L1.append(newstr)
         T1=tuple(L1)
         #print(T1)
         newls.append(T1)
    if (len(newls)==103):
           break;
    i=i+1
print(newls)

```

    [('M1B', 'Scarborough', 'Rouge,Malvern'), ('M1C', 'Scarborough', 'Highland Creek,Rouge Hill,Port Union'), ('M1E', 'Scarborough', 'Guildwood,Morningside,West Hill'), ('M1G', 'Scarborough', 'Woburn'), ('M1H', 'Scarborough', 'Cedarbrae'), ('M1J', 'Scarborough', 'Scarborough Village'), ('M1K', 'Scarborough', 'East Birchmount Park,Ionview,Kennedy Park'), ('M1L', 'Scarborough', 'Clairlea,Golden Mile,Oakridge'), ('M1M', 'Scarborough', 'Cliffcrest,Cliffside,Scarborough Village West'), ('M1N', 'Scarborough', 'Birch Cliff,Cliffside West'), ('M1P', 'Scarborough', 'Dorset Park,Scarborough Town Centre,Wexford Heights'), ('M1R', 'Scarborough', 'Maryvale,Wexford'), ('M1S', 'Scarborough', 'Agincourt'), ('M1T', 'Scarborough', "Clarks Corners,Sullivan,Tam O'Shanter"), ('M1V', 'Scarborough', "Agincourt North,L'Amoreaux East,Milliken,Steeles East"), ('M1W', 'Scarborough', "L'Amoreaux West"), ('M1X', 'Scarborough', 'Upper Rouge'), ('M2H', 'North York', 'Hillcrest Village'), ('M2J', 'North York', 'Fairview,Henry Farm,Oriole'), ('M2K', 'North York', 'Bayview Village'), ('M2L', 'North York', 'Silver Hills,York Mills'), ('M2M', 'North York', 'Newtonbrook,Willowdale'), ('M2N', 'North York', 'Willowdale South'), ('M2P', 'North York', 'York Mills West'), ('M2R', 'North York', 'Willowdale West'), ('M3A', 'North York', 'Parkwoods'), ('M3B', 'North York', 'Don Mills North'), ('M3C', 'North York', 'Flemingdon Park,Don Mills South'), ('M3H', 'North York', 'Bathurst Manor,Downsview North,Wilson Heights'), ('M3J', 'North York', 'Northwood Park,York University'), ('M3K', 'North York', 'CFB Toronto,Downsview East'), ('M3L', 'North York', 'Downsview West'), ('M3M', 'North York', 'Downsview Central'), ('M3N', 'North York', 'Downsview Northwest'), ('M4A', 'North York', 'Victoria Village'), ('M4B', 'East York', 'Woodbine Gardens,Parkview Hill'), ('M4C', 'East York', 'Woodbine Heights'), ('M4E', 'East Toronto', 'The Beaches'), ('M4G', 'East York', 'Leaside'), ('M4H', 'East York', 'Thorncliffe Park'), ('M4J', 'East York', 'East Toronto'), ('M4K', 'East Toronto', 'The Danforth West,Riverdale'), ('M4L', 'East Toronto', 'The Beaches West,India Bazaar'), ('M4M', 'East Toronto', 'Studio District'), ('M4N', 'Central Toronto', 'Lawrence Park'), ('M4P', 'Central Toronto', 'Davisville North'), ('M4R', 'Central Toronto', 'North Toronto West'), ('M4S', 'Central Toronto', 'Davisville'), ('M4T', 'Central Toronto', 'Moore Park,Summerhill East'), ('M4V', 'Central Toronto', 'Deer Park,Forest Hill SE,Rathnelly,South Hill,Summerhill West'), ('M4W', 'Downtown Toronto', 'Rosedale'), ('M4X', 'Downtown Toronto', 'Cabbagetown,St. James Town'), ('M4Y', 'Downtown Toronto', 'Church and Wellesley'), ('M5A', 'Downtown Toronto', 'Harbourfront'), ('M5B', 'Downtown Toronto', 'Ryerson,Garden District'), ('M5C', 'Downtown Toronto', 'St. James Town'), ('M5E', 'Downtown Toronto', 'Berczy Park'), ('M5G', 'Downtown Toronto', 'Central Bay Street'), ('M5H', 'Downtown Toronto', 'Adelaide,King,Richmond'), ('M5J', 'Downtown Toronto', 'Harbourfront East,Toronto Islands,Union Station'), ('M5K', 'Downtown Toronto', 'Design Exchange,Toronto Dominion Centre'), ('M5L', 'Downtown Toronto', 'Commerce Court,Victoria Hotel'), ('M5M', 'North York', 'Bedford Park,Lawrence Manor East'), ('M5N', 'Central Toronto', 'Roselawn'), ('M5P', 'Central Toronto', 'Forest Hill North,Forest Hill West'), ('M5R', 'Central Toronto', 'The Annex,North Midtown,Yorkville'), ('M5S', 'Downtown Toronto', 'Harbord,University of Toronto'), ('M5T', 'Downtown Toronto', 'Chinatown,Grange Park,Kensington Market'), ('M5V', 'Downtown Toronto', 'CN Tower,Bathurst Quay,Island airport,Harbourfront West,King and Spadina,Railway Lands,South Niagara'), ('M5W', 'Downtown Toronto', 'Stn A PO Boxes 25 The Esplanade'), ('M5X', 'Downtown Toronto', 'First Canadian Place,Underground city'), ('M6A', 'North York', 'Lawrence Heights,Lawrence Manor'), ('M6B', 'North York', 'Glencairn'), ('M6C', 'York', 'Humewood-Cedarvale'), ('M6E', 'York', 'Caledonia-Fairbanks'), ('M6G', 'Downtown Toronto', 'Christie'), ('M6H', 'West Toronto', 'Dovercourt Village,Dufferin'), ('M6J', 'West Toronto', 'Little Portugal,Trinity'), ('M6K', 'West Toronto', 'Brockton,Exhibition Place,Parkdale Village'), ('M6L', 'North York', 'Downsview,North Park,Upwood Park'), ('M6M', 'York', 'Del Ray,Keelesdale,Mount Dennis,Silverthorn'), ('M6N', 'York', 'The Junction North,Runnymede'), ('M6P', 'West Toronto', 'High Park,The Junction South'), ('M6R', 'West Toronto', 'Parkdale,Roncesvalles'), ('M6S', 'West Toronto', 'Runnymede,Swansea'), ('M7A', 'Downtown Toronto', "Queen's Park"), ('M7R', 'Mississauga', 'Canada Post Gateway Processing Centre'), ('M7Y', 'East Toronto', 'Business Reply Mail Processing Centre 969 Eastern'), ('M8V', 'Etobicoke', 'Humber Bay Shores,Mimico South,New Toronto'), ('M8W', 'Etobicoke', 'Alderwood,Long Branch'), ('M8X', 'Etobicoke', 'The Kingsway,Montgomery Road,Old Mill North'), ('M8Y', 'Etobicoke', "Humber Bay,King's Mill Park,Kingsway Park South East,Mimico NE,Old Mill South,The Queensway East,Royal York South East,Sunnylea"), ('M8Z', 'Etobicoke', 'Kingsway Park South West,Mimico NW,The Queensway West,Royal York South West,South of Bloor'), ('M9A', "Queen's Park", "Queen's Park,Queen's Park"), ('M9B', 'Etobicoke', 'Cloverdale,Islington,Martin Grove,Princess Gardens,West Deane Park'), ('M9C', 'Etobicoke', 'Bloordale Gardens,Eringate,Markland Wood,Old Burnhamthorpe'), ('M9L', 'North York', 'Humber Summit'), ('M9M', 'North York', 'Emery,Humberlea'), ('M9N', 'York', 'Weston'), ('M9P', 'Etobicoke', 'Westmount'), ('M9R', 'Etobicoke', 'Kingsview Village,Martin Grove Gardens,Richview Gardens,St. Phillips'), ('M9V', 'Etobicoke', 'Albion Gardens,Beaumond Heights,Humbergate,Jamestown,Mount Olive,Silverstone,South Steeles,Thistletown'), ('M9W', 'Etobicoke', 'Northwest')]



```python
#*converting the list back to Dataframe*
```


```python
newdf=pd.DataFrame(newls,columns=d_key)
```


```python
newdf.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>borough</th>
      <th>neighborhood</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M1B</td>
      <td>Scarborough</td>
      <td>Rouge,Malvern</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M1C</td>
      <td>Scarborough</td>
      <td>Highland Creek,Rouge Hill,Port Union</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M1E</td>
      <td>Scarborough</td>
      <td>Guildwood,Morningside,West Hill</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M1G</td>
      <td>Scarborough</td>
      <td>Woburn</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M1H</td>
      <td>Scarborough</td>
      <td>Cedarbrae</td>
    </tr>
    <tr>
      <th>5</th>
      <td>M1J</td>
      <td>Scarborough</td>
      <td>Scarborough Village</td>
    </tr>
    <tr>
      <th>6</th>
      <td>M1K</td>
      <td>Scarborough</td>
      <td>East Birchmount Park,Ionview,Kennedy Park</td>
    </tr>
    <tr>
      <th>7</th>
      <td>M1L</td>
      <td>Scarborough</td>
      <td>Clairlea,Golden Mile,Oakridge</td>
    </tr>
    <tr>
      <th>8</th>
      <td>M1M</td>
      <td>Scarborough</td>
      <td>Cliffcrest,Cliffside,Scarborough Village West</td>
    </tr>
    <tr>
      <th>9</th>
      <td>M1N</td>
      <td>Scarborough</td>
      <td>Birch Cliff,Cliffside West</td>
    </tr>
  </tbody>
</table>
</div>




```python
#*shape of the final dataframe*
```


```python
newdf.shape
```




    (103, 3)
