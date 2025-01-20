---
layout: post
title: Genesis Simulation 5 Results
date: '2025-01-20 12:09:49 -0400'
categories: [Genesis, Results]
tags: [simulation5]     # TAG names should always be lowercase
---
#### Results
Simulation 5 ran for 1000 Epochs with a starting population of 1000 organisms. Population growth slowly ramped up over the first 100ish epochs before plateauing and them slowly decreasing. By the 300th epoch, the top 100 most fit organisms have been selected and further epochs provide no value. Maximum fitness does not rise above a normalized .4 which is extremely low.


#### Changes
- Now runs multiple epochs
- Roots harvest from surrounding soil
- Seeds cost less
- Leaves harvest more to account for stem growth / efficiency
- Configurable sampling rate
- Allows customizable ecosystems

#### Thoughts

Reincarnated organisms shouldn't be directly added to the next epoch. Instead, we should mutate the reincarnated organisms before adding to the simulations to provide better heterogeneity.

#### Run settings
```
Ticks Per Day: 24
Maximum Days: 750
Tick Delay: 1ms
Initial Population: 1000
Width: 360
Height: 240
Depth: 0
Epochs: 1000
Reincarnation Size: 100
```
#### Configuration
```
{
  "ecosystems" : [
    {
      "name": "FlatFlora",
      "configuration": {
        "terrain.type" : "FLAT_WORLD",
        "daily.solar.property" : 10,
        "initial.soil.property" : 100,
        "initial.plant.energy" : 5,
        "death.plant.age.limit.days" : 100,
        "death.plant.starvation.limit.energy" : 0,
        "death.plant.stagnation.limit.days" : 10,
        "death.plant.germination.limit.ticks" : 10,
        "cell.leaf.max-energy-production" : 3,
        "cell.leaf.metabolic-rate" : 1,
        "cell.seed.max-energy-production" : 0,
        "cell.seed.metabolic-rate" : 0,
        "cell.stem.max-energy-production" : 0,
        "cell.stem.metabolic-rate" : 1,
        "cell.root.max-energy-production" : 2,
        "cell.root.metabolic-rate" : 4,
        "action.leaf.grow" : 3,
        "action.root.grow" : 2,
        "action.seed.grow" : 10,
        "action.seed.eject" : 15,
        "genome.transpose.probability" : 5,
        "genome.mutate.probability" : 3,
        "metadata.ttl" : 600,
        "metadata.export" : true,
        "metadata.export.path" : "./output/",
        "metadata.Performance.enabled" : true,
        "metadata.Environment.enabled" : true,
        "metadata.Performance.export" : true,
        "metadata.Environment.export" : true,
        "metadata.Environment.sampling-rate": 10
      }
    }

  ]
}
```
