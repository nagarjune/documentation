---
title: Adding Dropdowns
name: Dropdown Events
permalink: r/dropdowns/
description: How to add dropdowns to R plots
layout: base
thumbnail: thumbnail/dropdown.jpg
language: r
page_type: example_index
has_thumbnail: true
display_as: controls
order: 2
output:
  html_document:
    keep_md: true
---


### New to Plotly?

Plotly's R library is free and open source!<br>
[Get started](https://plot.ly/r/getting-started/) by downloading the client and [reading the primer](https://plot.ly/r/getting-started/).<br>
You can set up Plotly to work in [online](https://plot.ly/r/getting-started/#hosting-graphs-in-your-online-plotly-account) or [offline](https://plot.ly/r/offline/) mode.<br>
We also have a quick-reference [cheatsheet](https://images.plot.ly/plotly-documentation/images/r_cheat_sheet.pdf) (new!) to help you get started!

### Version Check

Version 4 of Plotly's R package is now [available](https://plot.ly/r/getting-started/#installation)!<br>
Check out [this post](http://moderndata.plot.ly/upgrading-to-plotly-4-0-and-above/) for more information on breaking changes and new features available in this version.

```r
library(plotly)
packageVersion('plotly')
```

```
## [1] '4.5.2'
```
### Simple Dropdown Menu Example


```r
library(plotly)
library(MASS)

covmat <- matrix(c(0.8, 0.4, 0.3, 0.8), nrow = 2, byrow = T)
df <- mvrnorm(n = 10000, c(0,0), Sigma = covmat)
df <- as.data.frame(df)

colnames(df) <- c("x", "y")
p <- plot_ly(df, x = ~x, y = ~y, alpha = 0.3) %>%
  add_markers(marker = list(line = list(color = "black", width = 1))) %>%
  layout(
    title = "Drop down menus - Plot type",
    xaxis = list(domain = c(0.1, 1)),
    yaxis = list(title = "y"),
    updatemenus = list(
      list(
        y = 0.8,
        buttons = list(

          list(method = "restyle",
               args = list("type", "scatter"),
               label = "Scatter"),

          list(method = "restyle",
               args = list("type", "histogram2d"),
               label = "2D Histogram")))
    ))

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = api_create(p, filename="dropdown-simple")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/3294.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Add Two Dropdown Menus to Restyle Graph


```r
library(plotly)

x <- seq(-2 * pi, 2 * pi, length.out = 1000)
df <- data.frame(x, y1 = sin(x), y2 = cos(x))

p <- plot_ly(df, x = ~x) %>%
  add_lines(y = ~y1, name = "A") %>%
  add_lines(y = ~y2, name = "B", visible = F) %>%
  layout(
    title = "Drop down menus - Styling",
    xaxis = list(domain = c(0.1, 1)),
    yaxis = list(title = "y"),
    updatemenus = list(
      list(
        y = 0.8,
        buttons = list(

          list(method = "restyle",
               args = list("line.color", "blue"),
               label = "Blue"),

          list(method = "restyle",
               args = list("line.color", "red"),
               label = "Red"))),

      list(
        y = 0.7,
        buttons = list(
          list(method = "restyle",
               args = list("visible", list(TRUE, FALSE)),
               label = "Sin"),

          list(method = "restyle",
               args = list("visible", list(FALSE, TRUE)),
               label = "Cos")))
    )
  )

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = api_create(p, filename="dropdown-2")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/3323.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
