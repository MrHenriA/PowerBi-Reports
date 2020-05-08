# HIPPA Data Breach Project
### [Github Repo](https://github.com/MrHenryA/HippaBreach)

# Data Breach Project
### [Live Demo](https://mrhenrya.github.io/HippaBreach/)

## Beginning Research
- [Retrieved data from kaggle](https://www.kaggle.com/forgotyourpassword/hipaa-data-breaches)
- [Retrieved additional recent data from HHS](https://ocrportal.hhs.gov/ocr/breach/breach_report.jsf)
- Data Schema layouts notes![Data Schema](https://i.imgur.com/oQS01eO.png)


## Using Pandas to handle data files


```python
import pandas as pd
import os
```

### Merging 3 different data sets to 1 single files


```python
df = pd.read_csv("/data/hipaa-data-breaches/recent-breach_report.csv")

files = [file for file in os.listdir('/data/hipaa-data-breaches')]

all_breaches_data = pd.DataFrame()

for file in files:
    df = pd.read_csv("/data/hipaa-data-breaches/"+file)
    all_breaches_data = pd.concat([all_breaches_data,df])

all_breaches_data.to_csv("all_breaches.csv",index=False)

```

### Read  updated dataframe


```python
all_breaches = pd.read_csv("all_breaches.csv")
all_breaches.head()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name of Covered Entity</th>
      <th>State</th>
      <th>Covered Entity Type</th>
      <th>Individuals Affected</th>
      <th>Breach Submission Date</th>
      <th>Type of Breach</th>
      <th>Location of Breached Information</th>
      <th>Business Associate Present</th>
      <th>Web Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Baystate Health</td>
      <td>MA</td>
      <td>Healthcare Provider</td>
      <td>11658.0</td>
      <td>04/05/2019</td>
      <td>Hacking/IT Incident</td>
      <td>Email</td>
      <td>No</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Health Recovery Services, Inc.</td>
      <td>OH</td>
      <td>Healthcare Provider</td>
      <td>20485.0</td>
      <td>04/05/2019</td>
      <td>Unauthorized Access/Disclosure</td>
      <td>Network Server</td>
      <td>No</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>OB Pharmacy</td>
      <td>CA</td>
      <td>Healthcare Provider</td>
      <td>3241.0</td>
      <td>04/03/2019</td>
      <td>Hacking/IT Incident</td>
      <td>Desktop Computer</td>
      <td>No</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Oregon Endodontic Group\t</td>
      <td>OR</td>
      <td>Healthcare Provider</td>
      <td>2952.0</td>
      <td>04/02/2019</td>
      <td>Hacking/IT Incident</td>
      <td>Email</td>
      <td>No</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Myriad Genetic Laboratories, Inc.</td>
      <td>UT</td>
      <td>Healthcare Provider</td>
      <td>1719.0</td>
      <td>04/01/2019</td>
      <td>Unauthorized Access/Disclosure</td>
      <td>Email</td>
      <td>No</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

- Renamed and removed some columns and ended up with this

| Business | State | Organization | People Affected | Breach  Date | Type of Breach | Breach Attack |
| -------- | ----- | ------------ | --------------- | ------------ | -------------- | ------------- |


- Tried to figure out a data schema that will best suite this data. I used http://www.databaseanswers.org/data_models to look through and find some, I found this software issue data model.
  Seems like a good one http://www.databaseanswers.org/data_models/tracking_software_problems/index.htm
 ![software issue](http://www.databaseanswers.org/data_models/tracking_software_problems/images/tracking_software_problems_dezign.gif) 





## I came up with a data model of such:
   ![model](https://i.imgur.com/Ng1KpW7.png)
- I believe this accomplished what I needed to do. This allowed to show breach dates in a broader date range. It allowed me to show regions and states with most breaches/people affected. What type of  data the breach exposed and most common breach type. What organizations were hit harder / what businessess and quite a bit more.
## Visualization 
- Now I try to figure out best visualizations / insights that I can come up with using this data
 ![model](https://i.imgur.com/GRF2Kub.gif)

### Result:
- At the end of the day I was able to come up with this [Report](https://mrhenrya.github.io/HippaBreach/)
