---
# the default layout is 'page'
icon: fas fa-info-circle
order: 0
math: true
---
Inspired by a youtube video I saw once, this project is to play with genetic algothrims. It is also a sandbox for playing with different design patterns and language features.

[Sources](#Sources) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[Development](#Development) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[Useful Links](#Useful-Links)

#### Fitness Function:

$$W_{1}log(\sqrt{C_{1}})+ W_{2}\frac{1}{(H_{1}-M_{1})}+W_{3}\frac{D_{1}}{D_{T}}*log(W_{4}O_{1})$$

#### Simulation Snapshot:
[Simulation 3 : Grass (4x zoom)](https://github.com/ADifferentLuke/Genetics/blob/main/notes/simulation_3_800x400) <br/>
![Simulation Grass](https://github.com/ADifferentLuke/Genetics/blob/main/misc/Grass.gif?raw=true)


#### Sources
* Asexual Versus Sexual Reproduction in Genetic Algorithms
  * [https://carleton.ca/cognitivescience/wp-content/uploads/2006-09.pdf](https://carleton.ca/cognitivescience/wp-content/uploads/2006-09.pdf)
* A simple algorithm for optimization and model fitting
  * [https://www.aanda.org/articles/aa/full_html/2009/27/aa11740-09/aa11740-09.html](https://www.aanda.org/articles/aa/full_html/2009/27/aa11740-09/aa11740-09.html)
* Using Genetic Algorithms with Asexual Transposition
  * [https://dl.acm.org/doi/pdf/10.5555/2933718.2933761](https://dl.acm.org/doi/pdf/10.5555/2933718.2933761)


#### Development 


    <dependency>
        <groupId>net.lukemcomber</groupId>
        <artifactId>genetics</artifactId>
        <version>v0.2.2</version>
    </dependency>

#### Useful Links 
[Javadocs](https://www.javadoc.io/doc/net.lukemcomber/genetics/latest/index.html)<br/>
[Source Code](https://github.com/ADifferentLuke/Genetics/)<br/>
[Example Configuration](https://github.com/ADifferentLuke/Genetics/blob/main/src/main/java/net/lukemcomber/genetics/universes/FlatFloraUniverse.java) <br />
[Example CLI](https://github.com/ADifferentLuke/Genetics/blob/main/src/main/java/net/lukemcomber/genetics/utilities/SimpleSimulator.java) <br />
[Example UI](https://github.com/ADifferentLuke/Oracle)<br />
<br />
<br />
[Back to Top](#top)
