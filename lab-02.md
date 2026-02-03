Lab 02 - Plastic waste
================
Kryschelle Fakir
2/2/2026

## Load packages and data

Here we’re loading in tidyverse and then telling R to define the dataset
for this lab as plastic_waste. This will make the data into an object
for us to access when running functions.

``` r
library(tidyverse) 
```

``` r
plastic_waste <- read.csv("data/plastic-waste.csv")
```

## Exercises

### Exercise 1

We’ll begin by looking at the distrbution of plastic waste per capita in
2010. The goal here is to understand what our data are doing and if
there are any major outliers. We will also look at the distribution by
continent using the facet_wrap function. In the second histogram plot
we’re telling R to plot the plastic waste per capita and make multiple
histograms showing the distribution for each continent.

``` r
ggplot(data = plastic_waste, aes(x = plastic_waste_per_cap)) +
  geom_histogram(binwidth = 0.2)
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](lab-02_files/figure-gfm/plastic-waste-continent-1.png)<!-- -->

``` r
plastic_waste %>%
  filter(plastic_waste_per_cap > 3.5)
```

    ##   code              entity     continent year gdp_per_cap plastic_waste_per_cap
    ## 1  TTO Trinidad and Tobago North America 2010    31260.91                   3.6
    ##   mismanaged_plastic_waste_per_cap mismanaged_plastic_waste coastal_pop
    ## 1                             0.19                    94066     1358433
    ##   total_pop
    ## 1   1341465

``` r
ggplot(data = plastic_waste, aes(x = plastic_waste_per_cap))+
  geom_histogram(binwidth = .35) +
  facet_wrap(~continent, nrow = 2)
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](lab-02_files/figure-gfm/plastic-waste-continent-2.png)<!-- -->

### Exercise 2

Now we’ll visualize the data using density plots. First, we’ll make a
basic density plots without mapping for fills. We can see the outlier a
little bit, but it’s hard to detect. Thus, we map the data by the
continent.It’s a little bit easier now but still difficult to follow.
Thus, we’ll fill in the plot by continent. This addition makes it easy
to see which continent has the most plastic waste per capita, and also
shows us the outlier in a visually appealing way. It’s still difficult
to understand with the overlapping colors, so we’ll implore the alpha
command to change the transparency.

``` r
ggplot (
  data = plastic_waste, 
  aes(x = plastic_waste_per_cap)
) + 
  geom_density()
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_density()`).

![](lab-02_files/figure-gfm/plastic-waste-density-1.png)<!-- -->

``` r
ggplot(
  data = plastic_waste, 
  mapping = aes(
    x = plastic_waste_per_cap, 
    color = continent
  )
) + 
  geom_density()
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_density()`).

![](lab-02_files/figure-gfm/plastic-waste-density-2.png)<!-- -->

``` r
ggplot(
  data = plastic_waste, 
  mapping = aes(
    x = plastic_waste_per_cap, 
    color = continent, 
    fill = continent
  )
) + 
  geom_density()
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_density()`).

![](lab-02_files/figure-gfm/plastic-waste-density-3.png)<!-- -->

``` r
ggplot(
  data = plastic_waste, 
  mapping = aes(
    x = plastic_waste_per_cap, 
    color = continent, 
    fill = continent
  )
) +
  geom_density(alpha = 0.7)
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_density()`).

![](lab-02_files/figure-gfm/plastic-waste-density-4.png)<!-- -->

``` r
ggplot(
  data = plastic_waste, 
  mapping = aes(
    x = plastic_waste_per_cap, 
    color = continent, 
    fill = continent
  )
) +
  geom_density(alpha = 0.2)
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_density()`).

![](lab-02_files/figure-gfm/plastic-waste-density-5.png)<!-- -->

``` r
#If we defined the alpha level as a characteristic of the mapping aesthetics.
ggplot(
  data = plastic_waste, 
  mapping = aes(
    x = plastic_waste_per_cap, 
    color = continent, 
    fill = continent, 
    alpha = .2
  )
) +
  geom_density()
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_density()`).

![](lab-02_files/figure-gfm/plastic-waste-density-6.png)<!-- -->

When adding the alpha level onto aes, the fill and the alpha are on the
same layer and, thus, R treats it like a point to plot and adds it onto
the legend. Thus, the alpha becomes another data plot, like the
continent data.

By applying the alpha level to the geom plot instead of mapping aes,
we’re essentially telling R to take the results of the density plot and
change it according to the alpha function. Now, the alpha level is a
function changing the appearance instead of functioning as a data point
to map.

Also, it seems that the alpha isn’t changing the transparency level to
the same degree when used in defining the mapping aesthetics. It could
be that the alpha level is being applied during the process, as opposed
to the look of the entire graph.

### Exercise 3

``` r
ggplot(
  data = plastic_waste, 
  mapping = aes(
    x = continent, 
    y = plastic_waste_per_cap
  )
) + 
  geom_boxplot()
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_boxplot()`).

![](lab-02_files/figure-gfm/plastic-waste-violin-1.png)<!-- -->

``` r
ggplot(
  data = plastic_waste, 
  mapping = aes(
    x = continent, 
    y = plastic_waste_per_cap
  )
) + 
  geom_violin()
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_ydensity()`).

![](lab-02_files/figure-gfm/plastic-waste-violin-2.png)<!-- -->

The violin plot shows a continuous distribution of plastic waste per
capita within the continents. These plots tell us which continents have
more or less plastic waste per capita in each category. For example,
North America has more countries with a plastic waste per capita than
Africa. As such, it shows the density of the distribution whereas the
boxplots show the exact five number distribution that some people may be
interested in knowing, such as the median and IQR. Those numbers are
harder to gauge in the violin plot than in the boxplot.

### Exercise 4

``` r
# insert code here
```

``` r
# insert code here
```

``` r
# insert code here
```

``` r
# insert code here
```

### Exercise 5

Remove this text, and add your answer for Exercise 5 here.

``` r
# insert code here
```
