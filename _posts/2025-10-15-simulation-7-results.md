---
layout: post
title: Genesis Simulation 7 Fitness Analysis
date: '2025-10-15  14:08:39 -0400'
categories: [Genesis, Analysis]
tags: [simulation7]     # TAG names should always be lowercase
---

### Simulation 7 break down

#### Changes

Significant fitness function tuning. 

#### Results

We finally got trees!! This was the main goal for Project Genesis. The average fitness was still trending upwards by the 50th epoch. 



```python
import pandas as pd
import json
import seaborn as sns
import matplotlib.pyplot as plt
import math
import gzip
import os

def compareAvgMetricsByEpoch(dataframe, firstColumn, secondColumn ):
    
    avgFirstColumnDf = dataframe.groupby('epoch', as_index=False)[firstColumn].mean()
    avgSecondColumnDf = dataframe.groupby('epoch', as_index=False)[secondColumn].mean()

    joinedData = pd.merge(avgFirstColumnDf, avgSecondColumnDf, on='epoch')
    avgEpochOverlay = joinedData.melt(id_vars='epoch', var_name='Metric', value_name='Value')

    return sns.lineplot(data=avgEpochOverlay, x='epoch', y='Value', hue='Metric')

def read_files_to_dataframe(basedirectory, metric):
    dataframes = []
    for directory in os.listdir(basedirectory):
        if( directory != 'overview.json' ):
            filepath = os.path.join(os.path.join(basedirectory, directory), metric + '.txt.gz')
            with gzip.open(filepath, 'rb') as f:
                df = pd.read_json(f,lines=True)
                df['epoch'] = int(directory.rsplit('-', 1)[-1])
                dataframes.append(df)
    return pd.concat(dataframes, ignore_index=True)
    
def readPopulationOverTime(file):
    raw_df = pd.read_json(file)
    overview = pd.json_normalize(raw_df['worlds'])
    overview['epoch'] = overview['name'].str.split('-', expand=True)[2].astype(int)

    trimmed = pd.DataFrame(overview, columns=['epoch', 'totalOrganisms'])
    return trimmed.iloc[::2]
```

<pre>Global Variable:</pre>


```python
INPUT_FILE_DIR = '/Users/luke/dev/analysis/data/simulation98'

METRIC='Performance'
EXPANDED_FITNESS_MAGNIFICATION = { 'startIndex': 0, 'count': 50 }
```

<pre>Global Computed Variables:</pre>


```python
fullSimulationDataDf = read_files_to_dataframe( INPUT_FILE_DIR, METRIC)
populationOverTimeDf = fullSimulationDataDf.value_counts('epoch').reset_index(name='totalOrganisms')
```

<pre>Analysis:</pre>


```python
sns.lineplot(x="epoch", y="totalOrganisms", data=populationOverTimeDf ).set_title("Population Over Time")
```




    Text(0.5, 1.0, 'Population Over Time')




    
![png](assets/figures/genesis-sim7-analysis/output_8_1.png)
    



```python
mostFitByEpochDf = fullSimulationDataDf.groupby('epoch')['fitness'].max().reset_index()
plt.figure(figsize=(14, 8))
sns.lineplot(x="epoch", y="fitness", data=mostFitByEpochDf ).set_title("Most Fit Organism Fitness")
```




    Text(0.5, 1.0, 'Most Fit Organism Fitness')




    
![png](assets/figures/genesis-sim7-analysis/output_9_1.png)
    



```python
avgSizeByEpoch = fullSimulationDataDf.groupby('epoch', as_index=False)['cells'].mean()
sns.lineplot(x="epoch", y="cells", data=avgSizeByEpoch ).set_title("Avg Number of Cells per Organism")
```




    Text(0.5, 1.0, 'Avg Number of Cells per Organism')




    
![png](assets/figures/genesis-sim7-analysis/output_10_1.png)
    



```python
fitnessHeritage = (
    fullSimulationDataDf.sort_values(by='fitness', ascending=False)
    .groupby('epoch')
    .head(50)
)

percentages = (
    fitnessHeritage.assign(
        isOrigOrganism =fitnessHeritage['parentId'].eq('GOD')
    )
    .groupby('epoch')['isOrigOrganism']
    .value_counts(normalize=True)
    .unstack(fill_value=0)
    .rename(columns={True: 'Initial Organisms', False: 'Organic Organisms'})
)

percentages.plot(
    kind='area',
    stacked=True,
    figsize=(16, 8),
    colormap='copper',
    title='Most Fit Organisms'
)
plt.ylabel('Percentage')
plt.xlabel('Epoch')
plt.legend(title='Parent Type')
plt.show()
```


    
![png](assets/figures/genesis-sim7-analysis/output_11_0.png)
    



```python
avgFitnessByEpoch = fullSimulationDataDf.groupby('epoch', as_index=False)['fitness'].mean()
sns.lineplot(x="epoch", y="fitness", data=avgFitnessByEpoch ).set_title("Avg Fitness")
```




    Text(0.5, 1.0, 'Avg Fitness')




    
![png](assets/figures/genesis-sim7-analysis/output_12_1.png)
    



```python
linePlt = compareAvgMetricsByEpoch(fullSimulationDataDf, 'fitness', 'offspring')
nothing = linePlt.set_title('Avg Fitness and Avg Offspring')
```


    
![png](assets/figures/genesis-sim7-analysis/output_13_0.png)
    



```python
linePlt = sns.lineplot(x="epoch", y="age", data=fullSimulationDataDf ).set_title("Population Range")
```


    
![png](assets/figures/genesis-sim7-analysis/output_14_0.png)
    



```python
compareAvgMetricsByEpoch(fullSimulationDataDf, 'fitness', 'age').set_yscale('log')
```


    
![png](assets/figures/genesis-sim7-analysis/output_15_0.png)
    



```python

```


```python
trend = (
    fullSimulationDataDf.groupby(['epoch', 'causeOfDeath'])
      .size()
      .reset_index(name='count')
      .pivot(index='epoch', columns='causeOfDeath', values='count')
      .fillna(0)
)
sns.heatmap(trend.T, cmap="viridis", annot=False, fmt="g")
plt.xlabel("Epoch")
plt.ylabel("Cause of Death")
plt.title("Counts by Epoch and Cause of Death")
plt.show()
```


    
![png](assets/figures/genesis-sim7-analysis/output_17_0.png)
    


Death value key is Unknown (0), Stagnation (1), Exhaustion (2), OldAge (3);


```python
trend.plot.area()
plt.xlabel("Epoch")
plt.ylabel("Count")
plt.title("Cause of Death Trends (Stacked)")
plt.show()
```


    
![png](assets/figures/genesis-sim7-analysis/output_19_0.png)
    



```python

```
