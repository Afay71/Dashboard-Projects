---
title: "Plot"
author: "Arif_Furkan"
date: "2024-06-23"
output:
  html_document: default
  pdf_document: default
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

### Loading Port Data

In this area we load the dataset

```{r}
require(dplyr)
url.world_ports <-
url("http://sharpsightlabs.com/wp-content/datasets/world_ports.RData")
load(url.world_ports)
glimpse(df.world_ports)
```

#### Creating a Theme

```{r}
require(ggplot2)
theme.porttheme <-
theme(text = element_text(color = "#444444")) +
theme(plot.title = element_text(size = 18)) +
theme(plot.subtitle = element_text(size = 16)) +
theme(axis.title = element_text(size = 14)) +
theme(axis.title.y = element_text(angle = 0, vjust = .5,
margin = margin(r = 15))) +
theme(axis.text = element_text(size = 10)) +
theme(axis.title.x = element_text(margin = margin(t = 20))) +
theme(legend.title = element_blank())
```

## Chart of the 25 Busiest Ports by Volume

```{r pressure, echo=FALSE}
df.world_ports %>%
filter(year == 2014, rank <= 25) %>%
ggplot(aes(x = reorder(port, volume), y = volume)) +
geom_bar(stat = "identity", fill = "dark red") +
geom_text(aes(label = volume), hjust = 1.1, color = "#FFFFFF") +
scale_y_continuous(labels = scales::comma_format()) +
coord_flip() +
labs(title = "25 Busiest Ports") +
labs(x="", y = "Shipment Volume (1000 TEUs)") +
theme.porttheme
```
