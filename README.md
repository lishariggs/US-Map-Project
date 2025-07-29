# 🗺️ Abortion Restrictions by US State (2018)
This R Markdown document demonstrates how to clean, classify, and visualize geographic data. The map highlights how abortion restrictions varied across US states in 2018,
categorized into tertiles for ease of interpretation.

**Overview**
- Goal: Map and visually compare abortion policy restrictiveness across US states.
- Approach: Classify states into tertiles (Low, Moderate, High restriction levels) and visualize using usmap and ggplot2.

# 📦 Requirements
The script installs and loads the following R packages if not already present:

usmap: For plotting US maps.

ggplot2: For custom plotting.

dplyr: For data manipulation.

`
library(usmap)
library(ggplot2)
library(dplyr)
`

# 🧮 Data
First I will manually define a data frame named state_data that includes: 

state: Full US state name

score: Numeric score indicating restrictiveness (higher = more restrictive)

category: Tertile classification (Low, Moderate, High)


<pre lang="markdown"> 
```r 
state_data <- data.frame(
state = c("District of Columbia", "Vermont", "New Hampshire", "Oregon", "Colorado", "Hawaii", "Washington", "California", "Delaware", "Nevada", "New Mexico", "Connecticut", "New York", "Maryland",

"Maine", "Massachusetts", "Montana", "New Jersey", "Wyoming", "Alaska", "Illinois", "Minnesota", "South Dakota", "West Virginia", "Georgia", "Ohio", "Tennessee", "Iowa", "Michigan", "Nebraska", "Rhode Island", "Utah", "Wisconsin",
"Alabama", "Arizona", "Arkansas", "Florida", "Idaho", "Kentucky", "Louisiana", "North Carolina", "Pennsylvania", "Virginia", "Mississippi", "Kansas", "Missouri", "North Dakota", "South Carolina", "Oklahoma", "Indiana", "Texas"),

score = c(0, 0, 0.5, 1, 1.5, 2, 2, 2.5, 2.5, 2.5, 2.5, 3, 3, 3.5,

4.5, 4.5, 4.5, 4.5, 4.5, 5.5, 5.5, 5.5, 5.5, 5.5, 6.5, 6.5, 6.5, 7.5, 7.5, 7.5, 7.5, 7.5, 7.5,
8.5, 8.5, 8.5, 8.5, 8.5, 8.5, 8.5, 8.5, 8.5, 8.5, 8.5, 9.5, 9.5, 9.5, 9.5, 10.5, 11.5, 11.5),

category = c(rep("Low", 14), rep("Moderate", 19), rep("High", 18)),
stringsAsFactors = FALSE
)
``` </pre>

To allow the usmap package to match states correctly, we can add state
abbreviations using built-in vectors and special handling for Washington, D.C.

<pre lang="markdown"> 
```r 
state_data$abbr <- state.abb[match(state_data$state, state.name)]
state_data$abbr[state_data$state == "District of Columbia"] <- "DC"
``` </pre>


# Setting Category as an Ordered Factor

Now we need to convert the category column into an ordered factor so that the legend and color scale follow
a logical “High → Moderate → Low” order.

<pre lang="markdown"> 
```r 
state_data$category <- factor(state_data$category, levels = c("High", "Moderate", "Low"))
``` </pre>

# 🗺️ Visualization

A choropleth map is created using the plot_usmap() function:

Color codes:
High: Dark Blue
Moderate: Light Blue
Low: Light Green


<pre lang="markdown"> 
```r 
plot_usmap(data = state_data, values = "category", regions = "states") +
scale_fill_manual(values = c("Low" = "#b2df8a", "Moderate" = "#a6cee3", "High" = "#1f78b4")) +
labs(
title = "2018 US States by Abortion Restriction Tertiles",
fill = "Abortion Tertile Category"
) +
theme_minimal() +
theme(
panel.grid = element_blank(),
axis.text = element_blank(),
axis.ticks = element_blank(),
axis.title = element_blank()
)
``` </pre>


<img width="1103" height="574" alt="2018Map2" src="https://github.com/user-attachments/assets/50d922e2-c7b5-465d-ab41-c274ea8303b9" />















