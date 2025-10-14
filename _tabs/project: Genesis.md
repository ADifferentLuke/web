---
# the default layout is 'page'
icon: fas fa-info-circle
order: 0
math: true
---

Inspired by a youtube video I saw once, this project is to play with genetic algothrims. It is also a sandbox for playing with different design patterns and language features.

[Reference Papers](#papers) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[Development](#Development) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[Useful Links](#Useful-Links)

#### Fitness Function:

$$
F = [C>1]\cdot \min\left(\frac{u}{a},\frac{a}{u}\right)\cdot \min\left(1,\max\left(0,\frac{\min(D,A_{\max})-B}{\max(1,A_{\max}-B)}\right)\right)\cdot e^{-\beta\left(\max(0,1-O)+\max(0,O-2)\right)}\cdot \frac{C}{C+k}
$$



#### Simulation Snapshot:
[Simulation 3 : Grass (4x zoom)](/posts/simulation-3-results/) <br />
![Simulation Grass](https://github.com/ADifferentLuke/Genetics/blob/main/misc/Grass.gif?raw=true)
<br />
[Simulation 4 : (4x zoom)](/posts/simulation-4-fitness-analysis/) <br />
![gif](assets/samples/Simulation4-Sample-Epoch3.gif)


#### Reference Papers <a id='papers' href="#"></a>
* Asexual Versus Sexual Reproduction in Genetic Algorithms
  * [https://carleton.ca/cognitivescience/wp-content/uploads/2006-09.pdf](https://carleton.ca/cognitivescience/wp-content/uploads/2006-09.pdf)
* A simple algorithm for optimization and model fitting
  * [https://www.aanda.org/articles/aa/full_html/2009/27/aa11740-09/aa11740-09.html](https://www.aanda.org/articles/aa/full_html/2009/27/aa11740-09/aa11740-09.html)
* Using Genetic Algorithms with Asexual Transposition
  * [https://dl.acm.org/doi/pdf/10.5555/2933718.2933761](https://dl.acm.org/doi/pdf/10.5555/2933718.2933761)


#### Development <a id='Development' href="#"></a>

[Build Artifact](https://mvnrepository.com/artifact/net.lukemcomber/genetics/v0.3.2)<br/>
[Javadocs](https://www.javadoc.io/doc/net.lukemcomber/genetics/latest/index.html)<br/>
[Source Code](https://github.com/ADifferentLuke/Genetics/)<br/>

#### Useful Links <a id='Useful-Links' href="#"></a>

[Simple CLI](https://github.com/ADifferentLuke/Genetics/blob/main/src/main/java/net/lukemcomber/genetics/utilities/SimpleSimulator.java) <br />
[Gstep](https://github.com/ADifferentLuke/Gstep)
[GeneGL](https://github.com/ADifferentLuke/Genegl)
<br />
<br />
[Back to Top](#top)
