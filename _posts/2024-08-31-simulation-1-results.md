---
layout: post
title: Genesis Simulation 1 Results
date: '2024-08-31 19:50:17 -0400'
categories: [Genesis, Results]
tags: [simulation1]     # TAG names should always be lowercase
---
#### Results
Most organisms starve themselves rapidly. Occasionally hyper-root organisms delevelop and starve seeds by collision detection. Leaf nodes rarely get higher than 1 stem node. Heavy root development.

#### Thoughts
- Fitness function needs to be rebalanced
	- Top heavy energy efficiency ratings are skewing  the function
- Perhaps add a energy toxicity level
- Environmental Resources need to be rebalanced
- Cell Metabolisms need to be rebalanced
- Metadata system needs improvement for higher load
- Output for environment resources / heat map

#### Most fit organism
``` json
{
  "name": "4d411cc7-c079-436c-ab37-1e3ce6ffa0d0",
  "parentId": "bb00c04f-6efa-4c91-93de-f22fb2f5bff7",
  "dna": "985241faa188c38c0cfeb8e0e28317ae5a696de3f589eb23f483807aa7dd872436320f4b3182f8fc3299ff23344460b58900fef01a00f93f00ba35417052a59a4e4042b55502e7ad93acd3eeed2e868d",
  "age": 1010,
  "birthTick": 5490,
  "offspring": 9,
  "cells": 1072,
  "totalEnergyHarvested": 831448,
  "totalEnergyMetabolized": 482016,
  "causeOfDeath": "Organism 4d411cc7-c079-436c-ab37-1e3ce6ffa0d0 died from old age.",
  "deathEnergy": 161943,
  "deathTick": 6500,
  "fitness": 99922.77564089025
}
```

#### Configuration

<pre>daily.solar.property: 10
initial.soil.property: 100
initial.plant.energy: 5
death.plant.age-limit-days: 100
death.plant.starvation-limit-energy: 0
death.plant.stagnation-limit-days: 10
cell.leaf.max-energy-production: 3
cell.leaf.metabolic-rate: 1
cell.seed.max-energy-production: 0
cell.seed.metabolic-rate: 0
cell.stem.max-energy-production: 0
cell.stem.metabolic-rate: 1
cell.root.max-energy-production: 2
cell.root.metabolic-rate: 1
action.leaf.grow: 1
action.root.grow: 2
action.seed.grow: 10
action.seed.eject: 1
genome.transpose.probability: 5
genome.mutate.probability: 5
metadata.ttl: 86400
metadata.Genealogy.enabled: true
metadata.Genome.enabled: true
metadata.Performance.enabled: true
</pre>


#### Starting Biology

>(204,138,000),a4d5b12a0e41f68c9d2a1b6d7e8f1c0a1b2d3e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b1c2d3e4f
>(050,079,000),b7e8f1c0a1b2d3e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5e6
>(130,059,000),c1d2e3f4a5b6c7d8e9f0a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2c3d4e5f6a7b8c9d0
>(201,175,000),d2e3f4a5b6c7d8e9f0a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2c3d4e5f6a7b8c9d0e1
>(075,224,000),e3f4a5b6c7d8e9f0a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2c3d4e5f6a7b8c9d0e1f2
>(302,099,000),f4a5b6c7d8e9f0a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2c3d4e5f6a7b8c9d0e1f2a3
