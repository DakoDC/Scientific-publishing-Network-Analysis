# Scientific-publishing-Network-Analysis
Analysis of scientific publishing data to investigate how scientific keywords are associated with gender and how those keywords form meaningful structures in scientific writing.

## Overview

This project investigates two main questions:

1. Do scientific keywords show different gender associations?
2. Are keywords connected according to how they are used in scientific writing?

Rather than examining individual papers in isolation, we analyze **keyword-level structures** to identify groups of related scientific concepts and investigate how those structures relate to gender associations, agency, communion, and scientific writing.

## Approach

The analysis consists of four main steps:

1. **Extract keywords** from scientific abstracts.
2. **Measure agency and communion** associated with each keyword.
3. **Measure gender bias** of keywords based on their distribution across male-only and female-only papers.
4. **Build, compare, and analyze two keyword networks.**

## Dataset

The dataset contains two groups of scientific papers:

* **Male-only papers:** approximately 372,000 papers
* **Female-only papers:** approximately 50,000 papers

The dataset is therefore strongly imbalanced, with roughly seven times as many male-only papers as female-only papers.

### Keyword Extraction

When papers already contained keywords, those keywords were used directly.

For papers without keywords but with an available abstract, up to **10 keywords** were extracted using **KeyBERT**.

Abstracts were also split into individual sentences because the semantic scoring models operate at the sentence level.

### Missing Data

| Data      | Male-only papers | Female-only papers |
| --------- | ---------------: | -----------------: |
| Abstracts |            7.64% |             10.88% |
| Keywords  |           14.27% |             15.91% |

## Measuring Agency, Communion, and Gender Bias

### Agency

Agency is measured using **BERTAgent**.

For each keyword:

1. Identify the sentences in which the keyword appears.
2. Score those sentences using BERTAgent.
3. Calculate the mean agency score across the relevant sentences.

### Communion

Communion is measured using the **ContentCoder Agency-Communion Dictionary**.

The same sentence-level procedure is applied:

1. Identify sentences containing the keyword.
2. Calculate communion scores.
3. Average the scores for each keyword.

### Gender Bias

Gender bias measures how frequently a keyword occurs in male-only versus female-only papers, normalized by the number of papers in each group.

The resulting score can be interpreted as:

| Score | Interpretation               |
| ----: | ---------------------------- |
|  `+1` | Only male-only papers        |
|   `0` | Balanced after normalization |
|  `-1` | Only female-only papers      |

The gender-bias score represents differences in the **distribution of keywords between the two datasets**. It should not be interpreted as evidence that a scientific topic is inherently male or female.

## Example Gender-Bias Results

Some keywords with higher positive and negative gender-bias scores include:

| More male-leaning      | Score | More female-leaning | Score |
| ---------------------- | ----: | ------------------- | ----: |
| Reinforcement learning | +0.46 | Higher education    | -0.74 |
| 5G                     | +0.39 | Technology          | -0.63 |
| Neural networks        | +0.37 | Education           | -0.58 |
| Simulation             | +0.25 | Social media        | -0.57 |
| Optimization           | +0.24 | Data mining         | -0.40 |

These values describe differences in keyword distributions between the two groups rather than intrinsic characteristics of the topics.

## Network Analysis

Two complementary keyword networks are constructed.

### Network 1 — Co-occurrence Network

* **Nodes:** keywords
* **Edges:** two keywords appearing in the same paper
* **Edge weight:** number of papers in which the two keywords occur together

This network captures relationships based on **co-occurrence in scientific papers**.

### Network 2 — Semantic Correlation Network

* **Nodes:** keywords
* **Edges:** positive correlation in both agency and communion
* **Edge weight:** agency correlation
* **Minimum overlap:** 5 papers

This network captures relationships based on **similar patterns of agency and communion**.

## Network Results

The two networks produce different structural patterns.

| Metric              | Network 1 | Network 2 |
| ------------------- | --------: | --------: |
| Nodes               |    23,201 |    11,815 |
| Louvain communities |        93 |        40 |
| Modularity          |     0.606 |     0.717 |
| Average Ncut        |     0.199 |     0.129 |
| Louvain–InfoMap NMI |     0.554 |     0.714 |

Network 1 has a larger number of keywords and communities, while Network 2 has fewer but more cohesive communities. Network 2 also shows stronger agreement between the Louvain and InfoMap community-detection methods.

## Communities

The detected communities correspond to recognizable scientific areas rather than being purely mathematical groupings.

Examples include:

### Network 1

* Social media, health & education
* Hardware & HPC
* Other large topical clusters

### Network 2

* Social media, health & education
* Robotics & autonomous navigation
* More compact semantic structures

The main distinction between the networks is:

> **Network 1** groups keywords according to what appears together in papers, while **Network 2** groups keywords according to similar patterns of agency and communion.

Overall, the analysis suggests that scientific vocabulary has a strong, non-random network structure and that gender associations can be studied alongside this structure rather than only at the individual-keyword level.


## Key Takeaways

* Scientific keywords form substantial network structures.
* Co-occurrence and semantic relationships produce different community structures.
* The semantic network contains fewer and more cohesive communities.
* Keyword gender-bias scores reveal differences in keyword distributions between male-only and female-only papers.
* Gender-bias measurements should be interpreted as **distributional differences**, not as inherent gender characteristics of scientific topics.
* Network analysis provides a way to study gender associations together with the broader structure of scientific vocabulary.

## Authors

**Calori Dakota Davide**
**Gigli Andrea**








