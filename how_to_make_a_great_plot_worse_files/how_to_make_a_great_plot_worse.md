---
title: "Untitled"
author: "Abigail Gregory"
date: "3/12/2020"
output:
  html_document:
    keep_md: true
---




### Instructions: Below is a code chunk that shows an effective visualization. First, copy this code chunk into a new code blockk. Then, modify it to purposely make this chart “bad” by breaking the principles of effective visualization above. Your final chart still needs to run/compile and it should still produce a plot.



```r
library("tidyverse")
```

```
## ── Attaching packages ──────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse 1.3.0 ──
```

```
## ✔ ggplot2 3.2.1     ✔ purrr   0.3.3
## ✔ tibble  2.1.3     ✔ dplyr   0.8.4
## ✔ tidyr   1.0.0     ✔ stringr 1.4.0
## ✔ readr   1.3.1     ✔ forcats 0.4.0
```

```
## ── Conflicts ─────────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
ggplot(airquality, aes(`Month`, `Temp`, group = `Month`)) +
    geom_boxplot(outlier.shape = NA) +
    geom_jitter(alpha = 0.3) +
    labs(x = "",
         y = "",
         title="Maximum temperature by month") +
    theme_bw() + 
    scale_x_continuous(breaks = c(5, 6, 7, 8, 9), 
                       labels = c("May", "June", "July", "August", "September")) +
    annotate("text", x = 4.08, y = 95, label="°F", size = 8) +
    coord_cartesian(xlim = c(4.5, 9.5),
                    clip = 'off') +
    theme(panel.grid.minor = element_blank(),
          panel.background = element_blank(), 
          axis.line = element_line(colour = "gray"),
          panel.border = element_blank(),
          text = element_text(size=18)
          )
```

![](how_to_make_a_great_plot_worse_files/figure-html/unnamed-chunk-1-1.png)<!-- -->







## ugly version

```r
ggplot(airquality, aes(`Month`, `Temp`, group = `Month`)) +
    geom_boxplot(outlier.shape = NA) +
    geom_jitter(alpha = 9) +
    scale_x_continuous(breaks = c(5, 6, 7, 8, 9), 
                       labels = c("1", "2", "3", "4", "5")) +
    annotate("text", x = 0, y = 1000, label="°F", size = 20) +
    coord_cartesian(xlim = c(4.5, 9.5),
                    clip = 'off')
```

![](how_to_make_a_great_plot_worse_files/figure-html/unnamed-chunk-2-1.png)<!-- -->
