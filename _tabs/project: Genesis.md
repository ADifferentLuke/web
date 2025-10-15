---
# the default layout is 'page'
icon: fas fa-info-circle
order: 0
math: true
---

# 🧬 Genesis: Evolution Simulation Ecosystem

> *Genesis is a sandbox for experimenting with genetic algorithms, biological simulation, and visualization.*

This ecosystem includes:
- **[Genetics](https://github.com/ADifferentLuke/Genetics)** – the core simulation engine implementing biological cells, energy metabolism, reproduction, and configurable fitness functions.  
- **[Gstep](https://github.com/ADifferentLuke/Gstep)** – an interactive application for stepping through genome
- **[GeneGL](https://github.com/ADifferentLuke/Genegl)** – an OpenGL-based visualization app for real-time viewing of evolving organisms.

---

## 🧠 Fitness Function

The primary fitness function used in `BasicV2FitnessFunction` is:

$$
F = [C>1]\cdot \min\left(\frac{u}{a},\frac{a}{u}\right)\cdot \min\left(1,\max\left(0,\frac{\min(D,A_{\max})-B}{\max(1,A_{\max}-B)}\right)\right)\cdot e^{-\beta\left(\max(0,1-O)+\max(0,O-2)\right)}\cdot \frac{C}{C+k}
$$

*(from `BasicV2FitnessFunction`)*

---

## 🌿 Simulation Snapshots

Below are highlights from various simulation runs, illustrating the progression of ecosystem evolution across different epochs.

| Simulation | Description | Preview |
|-------------|--------------|----------|
| [Simulation 3: Grass (4× zoom)](/posts/simulation-3-results/) | Stable grass evolution | ![Grass](https://github.com/ADifferentLuke/Genetics/blob/main/misc/Grass.gif?raw=true) |
| [Simulation 4: Fitness Analysis (4× zoom)](/posts/simulation-4-fitness-analysis/) | Comparative fitness growth | ![Sim 4](assets/samples/Simulation4-Sample-Epoch3.gif) |
| Simulation 6: Complex Organism Development | Early multicellular cooperation and differentiation | ![Sim6 Example 1](assets/samples/Sim6Example1.png) ![Sim6 Example 2](assets/samples/Sim6Example2.png) ![Sim6 Example 3](assets/samples/Sim6Example3.png) |
| Simulation 7: Ecosystem Maturation | Evolutionary stability over time | ![Epoch 14](assets/samples/sim7-epoch-14.png) ![Epoch 20](assets/samples/sim7-epoch-20.png) ![Epoch 40](assets/samples/sim7-epoch-40.png) ![Epoch 49](assets/samples/sim7-epoch-49.png) |

---

## 🧩 Project Components

### [Genetics Library](https://github.com/ADifferentLuke/Genetics)
Core simulation library implementing:
- Hierarchical cell system (`Cell`, `StemCell`, `LeafCell`, `RootCell`, etc.)
- Energy metabolism, mutation, and reproduction logic
- Configurable fitness functions for evolutionary pressure
- Fully documented API ([Javadocs](https://www.javadoc.io/doc/net.lukemcomber/genetics/latest/index.html))

**Build Artifacts:**  
[![Maven Central](https://img.shields.io/maven-central/v/net.lukemcomber/genetics)](https://mvnrepository.com/artifact/net.lukemcomber/genetics/v0.3.2)

---

### [Gstep](https://github.com/ADifferentLuke/Gstep)
Gstep visualizes and simulates genetic ecosystems in real time, allowing users to explore how virtual organisms behave within a digital terrain.

**Features:**
- Real-time simulation and visualization of organism interactions  
- Dynamic terrain rendering and environmental adaptation  
- Seamless integration with the Genetics core library  
- Adjustable simulation parameters for experimentation  

---

### [GeneGL Visualization](https://github.com/ADifferentLuke/Genegl)
An OpenGL-powered front-end for rendering and observing simulations in real-time.

**Features:**
- GPU-accelerated, real-time organism rendering  
- Visualizes energy flow, reproduction, and environmental interaction  
- Cross-platform Java application (Java 17+, OpenGL 3.3+)  
- Includes example configs (`sim.json`, `sim-parameters.json`)

---

## 📚 Reference Papers <a id='papers' href="#"></a>

- [Asexual Versus Sexual Reproduction in Genetic Algorithms](https://carleton.ca/cognitivescience/wp-content/uploads/2006-09.pdf)
- [A Simple Algorithm for Optimization and Model Fitting](https://www.aanda.org/articles/aa/full_html/2009/27/aa11740-09/aa11740-09.html)
- [Using Genetic Algorithms with Asexual Transposition](https://dl.acm.org/doi/pdf/10.5555/2933718.2933761)

---

## ⚙️ Development & Documentation <a id='Development' href="#"></a>

- [Build Artifact (Maven)](https://mvnrepository.com/artifact/net.lukemcomber/genetics/v0.3.2)  
- [Javadocs](https://www.javadoc.io/doc/net.lukemcomber/genetics/latest/index.html)  
- [Source Code](https://github.com/ADifferentLuke/Genetics/)  

---

## 🔗 Useful Links <a id='Useful-Links' href="#"></a>

- [Simple CLI Example](https://github.com/ADifferentLuke/Genetics/blob/main/src/main/java/net/lukemcomber/genetics/utilities/SimpleSimulator.java)  
- [Gstep](https://github.com/ADifferentLuke/Gstep)  
- [GeneGL Viewer](https://github.com/ADifferentLuke/Genegl)  

<br />
[Back to Top](#top)
