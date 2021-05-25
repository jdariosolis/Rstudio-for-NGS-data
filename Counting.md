Contents

1. [Hierarchical cluster](#1-hierarchical-clustering)
2. [Log transform (scaling)](#2-log-transform-(scaling))
3. [MDS (Multi-Dimensional Scaling) plot (by ezRun)](#3-mds-(multi-dimensional-scaling)-plot-(by-ezRun))

Note
* This is Tab-Separated-Value, text file.
* This is the result coming from the cufflinks command for all samples.
* RSudio server at FGCZ is available once you get a B-Fabric account.

Go to RStudio server
* http://fgcz-genomics.uzh.ch/
* and start a new project
	* [File]-[New Project], select *Existing Directory*, and select the *bio373_2020/* folder.

Load data (in R environment)
```R
 > data <- read.table("kam_fpkm.tsv", header=T, row.names=1)
 > head(data)
```

Correlation matrix
```R
 > cor(data)
```

Scatter plot
```R
 > plot(data$H1, data$H2)
 > plot(data$H1, data$L1)
 > plot(data$H1, data$H2, log="xy", xlim=c(0.001,100000), ylim=c(0.001, 100000))
 > plot(data$H1, data$L1, log="xy", xlim=c(0.001,100000), ylim=c(0.001, 100000))
```

Note
* plot(x-axis data, y-axis data)
* log="xy": scaling logarithmically in x- and y-axis
* xlim: plot region of x-axis
* ylim: plot region of y-axis

Boxplot
```R
 > data <- read.table("kam_fpkm.tsv", header=T, row.names=1)
 > head(data)
 > hal <- t(data["AT5G16980",1:2])
 > lyr <- t(data["AT5G16980",3:4])
 > tb <- cbind(hal, lyr)
 > colnames(tb) <- c("H", "L")
 > boxplot(tb, ylab="FPKM", main="AT5G16980")
```

![box.png](https://raw.githubusercontent.com/masaomi/Bio373_2020/master/png/box.png)

Scatter plot matrix
```R
 > pairs(data)
```

Plot scatter matrix and correlation matrix together
```R
 > library(psych)
 > pairs.panels(data)
```

![corr.png](https://raw.githubusercontent.com/masaomi/Bio373_2020/master/png/corr.png)

# 1. Hierarchical Clustering

Load data (in R environment)
```R
 > data <- read.table("kam_fpkm.tsv", header=T, row.names=1)
 > head(data)
 > distance <- dist(t(data))
 > distance
 > clustering <- hclust(distance)
 > plot(clustering)
```

![clustering1.png](https://raw.githubusercontent.com/masaomi/Bio373_2020/master/png/clustering1.png)

# 2. Log transform (scaling)

```R
 > data.log2 <- log2(data+1)
 > distance <- dist(t(data.log2))
 > clustering <- hclust(distance)
 > plot(clustering)
```

**Question4**
* What is the difference with and without scaling?

# 3. MDS (Multi-Dimensional Scaling) plot (by ezRun)

```R
 > library(ezRun)
 > ezMdsPlot(data, sampleColors = c("red", "blue", "green", "yellow"), main="MDS plot")
```

![mds.png](https://raw.githubusercontent.com/masaomi/Bio373_2020/master/png/mds.png)

Reference
* ezRun: https://github.com/uzh/ezRun/
