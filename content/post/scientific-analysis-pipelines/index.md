---
date: "2019-07-12"
diagram: true
image:
  caption: 'Image credit: [**John Moeses Bauan**](https://miro.medium.com/max/3500/0*JM8DmN3dQTHvVJzg.png)'
  placement: 3
markup: mmark
math: true
title: Scientific Data Analysis Pipelines and Reproducibility
---

*originally posted at [medium.com](https://towardsdatascience.com/scientific-data-analysis-pipelines-and-reproducibility-75ff9df5b4c5)*

## What do pipelines do? Why do we need them?
Pipelines are computational tools of convenience. Data analysis usually requires data acquisition, quality check, clean up, exploratory analysis and hypothesis driven analysis. Pipelines can automate these steps. They process raw data to a suitable format and analyze it with statistical tools or machine learning models in a streamlined way. In practical terms, a data analysis pipeline executes a chain of command-line tools and custom scripts. This usually provides processed data sets and a human readable report covering topics such as data quality, exploratory analysis etc.

In our field, raw data comes as text files containing sequencing reads. The reads have a 4-letter code (ACGT) and they originate from specific locations of the genome. We need to quality check the reads, align them to the genome, quantify them and run statistical/machine-learning models on them. Different command-line tools and custom scripts have to be run in sequence to achieve these tasks. If there is a problem in quality check or alignments, parts or all the steps need to be re-run with different parameters depending on the nature of the problem observed with the data. We may have to run this for hundreds of times, so automating at least part of these tasks via pipelines is beneficial.

## What is reproducibility? Why is it important ?
Pipelines can be a great help when you have to process a dataset repeatedly with some changes in parameters or when you process multiple datasets. Since basic data processing and analysis tasks can take a lot of hands-on time, automating certain parts of these saves time. Researchers can then spend more time on visualization, communication of results or tailor made statistical/machine-learning analysis. Because of this convenience many researchers are creating pipelines and sharing them with the community via publications. Normally, when you share the pipeline you would like to make sure that your pipeline will produce the same output for other users when provided with the same input data. How can one install the exact same pipeline with the exact dependencies its creator using and make sure it produces the same output? Although it sounds like a trivial question, reports regarding “reproducibility crisis in science” shows that it is not very easy to achieve this. Other researchers repeatedly fail to reproduce published experiments. This “reproducibility crisis” is not limited to fields such as biology or psychology. Computational fields also suffer from this.

There are a couple of criteria for reproducible data analysis.

**Data and metadata availability:** Data and metadata should be available without question. Without these, there is a no way you can reproduce an analysis. In our research domain, data and metadata usually deposited to public databases after publication.

**Transparency:** There should be complete transparency of the code you are using and the dependencies you need to run the code. This also extends to source code availability of your dependencies. It is undesirable to have a tool whose behaviour crucially depends on a proprietary binary blob / black box. In addition, you need to know exact versions and configurations of the dependencies to have a shot at reproducing the data analysis pipeline. Preferably, the installation procedure keeps track of the different dependency structures and installs everything you need, see the point below.

**Ease of installation (installability):** Computational analysis tools and pipelines should make the effort to be easily installable. I think many of us will be deterred if the pipeline has many dependencies that have to be installed separately. This will remain so even if we are promised to get a working pipeline that reproduces the authors version after we go through installation of each dependency diligently. The more dependencies a pipeline has, the more it is likely that at least one of them will be a problem during installation. Many published scientific software can not be installed. Studies claim at least 50% of the published software is uninstallable [see here & here]. I suspect that for the pipelines, many with more complicated dependencies, the situation is worse. People who have gone through poorly written readme files and tried to install all the dependencies know very well why “ease of installation” is important.

**Runtime environment reproducibility:** The installed software should behave the same in every machine, in the sense that we need to install the very same software in every machine. Achieving this is not straightforward because the software depends on many different things from compilers, to system libraries to 3rd-party software and libraries needed. You need to control this complex system of dependencies if you want to build software exactly the same way on different machines and get the same software. The version of dependencies and how they are built will have an effect on the software you are trying to install. For example if the software you are trying to install requires Boost C++ library, having Boost version 1.68 might produce differences compared to having version 1.38. There might be bug fixes or improvements that could change the behaviour of the software we are trying to install. Therefore, this software can behave differently even though same version is installed on two different machines because of dependency differences.

If you can install the same exact software, built the same way with exactly the same dependencies down to the compiler, you have good chances at reproducing the runtime environment across different machines and therefore the analysis with the same input data. Only exception here is that if the software has some stochastic component that you can not control then it will not be possible to reproduce the analysis. For example, k-means clustering algorithm might produce different clustering results every time depending a random initialization procedure. If we are not able to control that behavior by setting random seed we won’t be able to reproduce the results.

Essential ingredients of data analysis reproducibility. Reproducibility requires availability of data and being able to use the same exact software.




