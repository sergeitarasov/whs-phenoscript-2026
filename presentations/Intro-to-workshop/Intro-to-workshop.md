---
marp: true
theme: default
paginate: true
html: true
style: |
  section { font-size: 1.3rem; }
  h1 { color: #2c5f8a; }
  h2 { color: #2c5f8a; }
  h3 { color: #2c5f8a; }
  code { background: #f0f4f8; border-radius: 3px; padding: 0 4px; }
  pre { font-size: 0.8rem; }
  table { font-size: 1.1rem; }
  .columns { display: grid; grid-template-columns: 1fr 1fr; gap: 2rem; }
  .note { background: #f0f8ff; border-left: 4px solid #2c5f8a; padding: 0.5rem 1rem; margin-top: 1rem; font-size: 1.1rem; }
---

<div style="display:flex; align-items:center; justify-content:space-between; height:80%; gap:2rem">
<div style="flex:1">

# Welcome to the Workshop

**From Species Descriptions to Computable Phenotypes: An Introduction to Phenoscript and Ontologies**

<br>

WHS Methodological Pills


</div>
<div style="flex:0 0 230px; text-align:center">

![w:120](../../icons/images.png)

![w:120](../../icons/phenoscript.png)

</div>
</div>

---

# Organizers and Instructors

## Organizers

- [Willi Hennig Society](https://cladistics.org/)
- Amrita Srivathsan (WHS)
- Santiago Catalano (WHS)
- Ambrosio Torres Galvis (WHS)



## Instructors

- [Sergei Tarasov](https://www.tarasovlab.com/team) (Finnish Museum of Natural History)
- [Giulio Montanaro](https://www.researchgate.net/profile/Giulio-Montanaro) (Finnish Museum of Natural History)
- [Jennifer Girón](https://sites.google.com/view/jcgiron/home) (Museum at Texas Tech University)


<center><strong>Post in the Zoom chat the organisms you are working with 🦋</strong></center>

---

# Goals and Schedule

**Aims:**
- Demonstrate how to use (insect) ontologies and Phenoscript to make traits and descriptions computable
  - We focus on species descriptions
  - The approach can be applied to matrices
- Grow and engage the community
- We want your feedback on what can be improved

**Material:**

[https://github.com/sergeitarasov/whs-phenoscript-2026](https://github.com/sergeitarasov/whs-phenoscript-2026)

---
## Schedule

- 12:00-12:10 **[Introduction to the Workshop]()** *(Sergei)*
- 12:10-12:40 **[Introduction to Insect Ontologies]()** *(Jennifer)*
- 12:40-13:00 **[Phenoscript Workflow]()** *(Sergei)*
- 13:00-13:40 **[Encoding Traits using Phenoscript]()** *(Giulio)*
- 13:40-13:50 **[Querying Phenoscript Descriptions]()** *(Sergei)*
- 13:50-14:00 **Break**
- 14:00-15:00 **Practical Exercises** *(Giulio, Sergei, Jennifer)*
    - Make at least 5 Phenoscript statements about your favorite species. Check if they are correctly translated into OWL and natural text.

---


## Prerequisites


- **Install required software** (all free):
  - [VS Code](https://code.visualstudio.com) — for writing Phenoscript
  - [Docker](https://www.docker.com/products/docker-desktop/) — to run the necessary software
  - [Protégé](https://protege.stanford.edu) — ontology editor

- **Install the Phenoscript extension for VS Code** — follow the [installation instructions](https://github.com/sergeitarasov/whs-phenoscript-2026/wiki/install)

- **Get an [ORCID ID](https://orcid.org)** if you do not have one

- **Prepare trait data** — identify five traits of your favorite species that you would like to code using Phenoscript during the workshop and have them available


---

## Highly recommended before the workshop

- **Join OntoTraits Slack** for discussion (link privately shared)

- **Complete the [Pizza Ontology tutorial](https://www.michaeldebellis.com/post/new-protege-pizza-tutorial)** — understand what an ontology is (approximately half a day)

- **Important reading:**
  - Insect Anatomy Ontology — <https://doi.org/10.1093/sysbio/syad025>
  - Phenoscript and semantic descriptions — <https://bdj.pensoft.net/article/121562/>



<center><strong>If you did the Pizza Ontology tutorial, post "I like pizza" in the Zoom chat 🍕</strong></center>


---

# Let's start


