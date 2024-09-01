---
layout: post
title: Genesis Simulation 4 Fitness Analysis
date: '2024-09-01 11:08:39 -0400'
categories: [Genesis, Analysis]
tags: [simulation4]     # TAG names should always be lowercase
---

Fitness, cell count, and offspring counts trend positive over multiple generations and epochs. Currently no organism is reaching old age. Death type tends towards exhaustion over time. 

Energy efficiency may not be a valuable metric. Since there are no selection pressures on energy efficiency other than starvation and exhaustion, it is unclear if there are trends emerging over generations. Energy waste was removed from the fitness function as it's strongly correlated with energy efficiency, essentially doubling the energy efficiency impact on fitness.

[Population](#pop-over-time) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[Death](#death-anal)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[Offspring](#off-anal)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[Energy Efficiency](#off-anal)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[Cells](#cell-anal)
<hr />

```python
import pandas as pd
import json
import seaborn as sns
import matplotlib.pyplot as plt
import math
```


```python
total_epochs = 5
performance_path = '/Users/luke/dev/Genetics/data/Rebalanced-Sim4-Epoch-%d-performance.json'
environment_path = '/Users/luke/dev/Genetics/data/Rebalanced-Sim4-Epoch-%d-environment.json'
metrics = [
    { 
        'metric': 'performance', 
        'path': performance_path 
    },
    {
        'metric': 'environment', 
        'path': environment_path 
    }
]
```


```python
def genetic_data_to_dataframe(path):
    raw_df = pd.read_json(path)
    return pd.json_normalize(raw_df['log'])

def load_simulation_data():
    simulations = {}
    for metric in metrics:
        if not metric['metric'] in simulations:
            simulations[metric['metric']] = {}
        for i in range(total_epochs):
            simulation_instance  = genetic_data_to_dataframe( metric['path'] % i )
            simulation_instance['epoch'] = i
            simulations[metric['metric']][i] = simulation_instance

    return simulations

def merge_epochs(df):
    cat_df = pd.DataFrame();
    for i in range(total_epochs):
        cat_df = pd.concat( [ df[i], cat_df] )
    return cat_df
    
```


```python
sns.set_theme(style="darkgrid")

simulations = load_simulation_data()
```

#### Death ID Mappings

|ID|Death|
|--|-----|
|0|Unknown|
|1|Stagnation|
|2|Exhaustion|
|3|Old Age|

#### Population Over Time <a id="pop-over-time" href="#"></a>


```python
all_environment_data = merge_epochs( simulations['environment'] )
fig = sns.lineplot(x="tickCount", y="totalOrganisms", hue='epoch',
        data=all_environment_data ).set_title("Population Over Time")

```


    
![png](assets/figures/genesis-sim4-analysis/output_8_0.png)
    


#### Fitness Analysis <a id="fit-anal" href="#"></a>


```python
all_organism_data = merge_epochs( simulations['performance'] )

g = sns.relplot(
    data=all_organism_data,
    x="birthTick", y="fitness", hue="epoch"
)
g.set(xlabel="Birth", ylabel="Fitness", title="Organism Fitness")
g.despine(left=True, bottom=True)
g.fig.set_size_inches(15,15)

```


    
![png](assets/figures/genesis-sim4-analysis/output_10_0.png)
    



```python
fitnessPerEpoch = pd.DataFrame(columns=['epoch', 'fitness' ])
for i in range(total_epochs):
    fitnessPerEpoch.loc[ -1 ] = [ i , simulations['performance'][i]['fitness'].mean() ]
    fitnessPerEpoch.index = fitnessPerEpoch.index + 1

g = sns.lineplot(x="epoch", y="fitness", data=fitnessPerEpoch).set_title("Mean Fitness per Epoch")                           
```


    
![png](assets/figures/genesis-sim4-analysis/output_11_0.png)
    


#### Death Analysis <a id="death-anal" href="#"></a>


```python
palette_color = sns.color_palette('bright') 
  
# plotting data on chart 
for i in range(total_epochs):
    
    simulations['performance'][i]['causeOfDeath'].value_counts().plot.pie( autopct='%1.1f%%', shadow=True, figsize=(2,2))
    plt.title("Epoch " + str(i) + " death breakout.")
    plt.show()

```


    
![png](assets/figures/genesis-sim4-analysis/output_13_0.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_13_1.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_13_2.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_13_3.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_13_4.png)
    



```python
causeOfDeathPerEpoch = pd.DataFrame(columns=['Epoch', 'Cause of Death' ])
for i in range(total_epochs):
    simulations['performance'][i]['deathRating'] = simulations['performance'][i]['causeOfDeath'] / 4
    causeOfDeathPerEpoch.loc[ -1 ] = [ i , simulations['performance'][i]['deathRating'].mean() ]
    causeOfDeathPerEpoch.index = causeOfDeathPerEpoch.index + 1
g = sns.lineplot(x="Epoch", y="Cause of Death",
        data=causeOfDeathPerEpoch).set_title("Morbid Rating ")

```


    
![png](assets/figures/genesis-sim4-analysis/output_14_0.png)
    


#### Offspring Analysis <a id="off-anal" href="#"></a>


```python
childrenPerEpoch = pd.DataFrame(columns=['Epoch', 'Avg Children' ])
for i in range(total_epochs):
    childrenPerEpoch.loc[ -1 ] = [ i , math.log(simulations['performance'][i]['offspring'].mean()) ]
    childrenPerEpoch.index = childrenPerEpoch.index + 1
    
sns.histplot( data=all_organism_data, x='offspring', hue='epoch', binwidth=1,
            element="poly" ).set_title('Offspring Count per Epoch')    
plt.show()

g = sns.lineplot(x="Epoch", y="Avg Children",
        data=childrenPerEpoch).set_title("Normalized Average Children")

```


    
![png](assets/figures/genesis-sim4-analysis/output_16_0.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_16_1.png)
    


#### Energy Efficiency Analysis <a id="ee-anal" href="#"></a>


```python
energyEfficiencyPerEpoch = pd.DataFrame(columns=['Epoch', 'Energy Efficiency' ])

for i in range(total_epochs):
    simulations['performance'][i]['differential'] = simulations['performance'][i]['totalEnergyHarvested'] - simulations['performance'][i]['totalEnergyMetabolized']
    simulations['performance'][i]['normalized'] = 1 / simulations['performance'][i]['differential']
    energyEfficiencyPerEpoch.loc[ -1 ] = [ i , 1 / simulations['performance'][i]['differential'].mean() ]
    energyEfficiencyPerEpoch.index = energyEfficiencyPerEpoch.index + 1
    g = sns.displot( data=simulations['performance'][i], x="differential", kind="kde")
    g.figure.subplots_adjust(top=.9);
    g.figure.suptitle( 'Epoch ' + str(i) + ' Energy Efficiency Distribution')
    plt.show()
    



g = sns.lineplot(x="Epoch", y="Energy Efficiency",
        data=energyEfficiencyPerEpoch)
plt.show()

```


    
![png](assets/figures/genesis-sim4-analysis/output_18_0.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_18_1.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_18_2.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_18_3.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_18_4.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_18_5.png)
    


#### Cell Analysis <a id="cell-anal" href="#"></a>


```python
cellsPerEpoch = pd.DataFrame(columns=['Epoch', 'Avg Cells' ])
for i in range(total_epochs):
    cellsPerEpoch.loc[ -1 ] = [ i , math.log(simulations['performance'][i]['cells'].mean()) ]
    cellsPerEpoch.index = cellsPerEpoch.index + 1
    sns.histplot( data=simulations['performance'][i], x='cells', binwidth=1,
                element="poly").set_title('Epoch ' + str(i) + ' Cell Count') 
    plt.show()

    
sns.histplot( data=all_organism_data, x='cells', hue='epoch', binwidth=1,
            element="poly" ).set_title('Cell Count per Epoch Overlay') 
plt.show()
sns.lineplot(x="Epoch", y="Avg Cells",
        data=cellsPerEpoch).set_title("Normalized Organism Size")
plt.show()
```


    
![png](assets/figures/genesis-sim4-analysis/output_20_0.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_20_1.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_20_2.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_20_3.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_20_4.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_20_5.png)
    



    
![png](assets/figures/genesis-sim4-analysis/output_20_6.png)
    



```python

```


```python

```
