Principal Component Analysis and Plotly
================

Outline
-------

We are going to outline the concept of *Principal Component Analysis* (PCA) and use it to reduce the size of the feature space of the Iris data set. We'll then fit a tree based model to both the original Iris data set and the new PCA-transformed data and compare model performance. We'll be using plotly to produce various plots including a Scree plot for our PCA process.

Motivation for PCA
------------------

Why might someone want to use PCA? Consider a dataset where we have a very large number of features, in the thousands or millions perhaps. Fitting a predictive model to such a dataset might be computationally impossible, we can only throw so much computing power at the problem. If we could reduce the number of features while still maintaining **most** of the information from the original feature space then we might take this deal due to the benefits of working with a much smaller number of features. Reducing the feature space of your data can result in a less complicated model and a more reasonable training time.

Outline of PCA
--------------

PCA rebases your data and creates new features called *principal components* that are linear combinations of the current features. These principal components are made by finding lines, or directions in your data cloud where the most variability is present. If we were to fit multiples lines through our data cloud (through the mean of our data) and project our data points onto the lines, then the first principal component would be the line that has the largest sum of square distances from the mean. The other principal componenets would be lines that are orthogonal to the first.

Coding:
-------

Now that we've got a bit of the explanation out of the way, we can start working in R.

### Packages

We'll start by loading all of our packages:

``` r
library(plyr)
library(tidyr)
library(dplyr)
library(plotly)
```

### Iris Data

Now we'll get our data. We're going to use the popular Iris data set to explore PCA. Let's explore it briefly:

``` r
glimpse(iris)
```

    ## Observations: 150
    ## Variables: 5
    ## $ Sepal.Length <dbl> 5.1, 4.9, 4.7, 4.6, 5.0, 5.4, 4.6, 5.0, 4.4, 4.9,...
    ## $ Sepal.Width  <dbl> 3.5, 3.0, 3.2, 3.1, 3.6, 3.9, 3.4, 3.4, 2.9, 3.1,...
    ## $ Petal.Length <dbl> 1.4, 1.4, 1.3, 1.5, 1.4, 1.7, 1.4, 1.5, 1.4, 1.5,...
    ## $ Petal.Width  <dbl> 0.2, 0.2, 0.2, 0.2, 0.2, 0.4, 0.3, 0.2, 0.2, 0.1,...
    ## $ Species      <fct> setosa, setosa, setosa, setosa, setosa, setosa, s...

We have 4 features:

-   Sepal Length
-   Sepal Width
-   Petal Length
-   Petal Width

and a target variable Species:

``` r
unique(iris$Species)
```

    ## [1] setosa     versicolor virginica 
    ## Levels: setosa versicolor virginica

We can produce some plots:

``` r
# Produce long format of data for plotly plots
iris_long <- iris %>%
  gather(key = "Feature",
         value = "Value",
         -Species)

# Create 3 plots for each unqiue response value
p1 <- plot_ly(iris_long %>% filter(Species == "setosa"),
              x = ~Value,
              color = ~Feature,type = "histogram",
              text  = ~paste0(Species,"\n",
                              Feature,"\n"))

p2 <- plot_ly(iris_long %>% filter(Species == "versicolor"),
              x = ~Value,
              color = ~Feature,type = "histogram",
              text  = ~paste0(Species,"\n",
                              Feature,"\n"))

p3 <- plot_ly(iris_long %>% filter(Species == "virginica"),
              x = ~Value,
              color = ~Feature,type = "histogram",
              text  = ~paste0(Species,"\n",
                              Feature,"\n"))

# Use subplots to plot together
subplot(p1,
        style(p2, showlegend = FALSE),
        style(p3, showlegend = FALSE),
        nrows = 3)
```

    ## PhantomJS not found. You can install it with webshot::install_phantomjs(). If it is installed, please make sure the phantomjs executable can be found via the PATH variable.

<!--html_preserve-->

<script type="application/json" data-for="htmlwidget-d56479a3fb7ab6b2b41c">{"x":{"data":[{"x":[1.4,1.4,1.3,1.5,1.4,1.7,1.4,1.5,1.4,1.5,1.5,1.6,1.4,1.1,1.2,1.5,1.3,1.4,1.7,1.5,1.7,1.5,1,1.7,1.9,1.6,1.6,1.5,1.4,1.6,1.6,1.5,1.5,1.4,1.5,1.2,1.3,1.4,1.3,1.5,1.3,1.3,1.3,1.6,1.9,1.4,1.6,1.4,1.5,1.4],"text":["setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />","setosa<br />Petal.Length<br />"],"type":"histogram","name":"Petal.Length","marker":{"color":"rgba(102,194,165,1)","line":{"color":"rgba(102,194,165,1)"}},"error_y":{"color":"rgba(102,194,165,1)"},"error_x":{"color":"rgba(102,194,165,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":[0.2,0.2,0.2,0.2,0.2,0.4,0.3,0.2,0.2,0.1,0.2,0.2,0.1,0.1,0.2,0.4,0.4,0.3,0.3,0.3,0.2,0.4,0.2,0.5,0.2,0.2,0.4,0.2,0.2,0.2,0.2,0.4,0.1,0.2,0.2,0.2,0.2,0.1,0.2,0.2,0.3,0.3,0.2,0.6,0.4,0.3,0.2,0.2,0.2,0.2],"text":["setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />","setosa<br />Petal.Width<br />"],"type":"histogram","name":"Petal.Width","marker":{"color":"rgba(252,141,98,1)","line":{"color":"rgba(252,141,98,1)"}},"error_y":{"color":"rgba(252,141,98,1)"},"error_x":{"color":"rgba(252,141,98,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":[5.1,4.9,4.7,4.6,5,5.4,4.6,5,4.4,4.9,5.4,4.8,4.8,4.3,5.8,5.7,5.4,5.1,5.7,5.1,5.4,5.1,4.6,5.1,4.8,5,5,5.2,5.2,4.7,4.8,5.4,5.2,5.5,4.9,5,5.5,4.9,4.4,5.1,5,4.5,4.4,5,5.1,4.8,5.1,4.6,5.3,5],"text":["setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />","setosa<br />Sepal.Length<br />"],"type":"histogram","name":"Sepal.Length","marker":{"color":"rgba(141,160,203,1)","line":{"color":"rgba(141,160,203,1)"}},"error_y":{"color":"rgba(141,160,203,1)"},"error_x":{"color":"rgba(141,160,203,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":[3.5,3,3.2,3.1,3.6,3.9,3.4,3.4,2.9,3.1,3.7,3.4,3,3,4,4.4,3.9,3.5,3.8,3.8,3.4,3.7,3.6,3.3,3.4,3,3.4,3.5,3.4,3.2,3.1,3.4,4.1,4.2,3.1,3.2,3.5,3.6,3,3.4,3.5,2.3,3.2,3.5,3.8,3,3.8,3.2,3.7,3.3],"text":["setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />","setosa<br />Sepal.Width<br />"],"type":"histogram","name":"Sepal.Width","marker":{"color":"rgba(231,138,195,1)","line":{"color":"rgba(231,138,195,1)"}},"error_y":{"color":"rgba(231,138,195,1)"},"error_x":{"color":"rgba(231,138,195,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":[4.7,4.5,4.9,4,4.6,4.5,4.7,3.3,4.6,3.9,3.5,4.2,4,4.7,3.6,4.4,4.5,4.1,4.5,3.9,4.8,4,4.9,4.7,4.3,4.4,4.8,5,4.5,3.5,3.8,3.7,3.9,5.1,4.5,4.5,4.7,4.4,4.1,4,4.4,4.6,4,3.3,4.2,4.2,4.2,4.3,3,4.1],"text":["versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />","versicolor<br />Petal.Length<br />"],"type":"histogram","name":"Petal.Length","marker":{"color":"rgba(102,194,165,1)","line":{"color":"rgba(102,194,165,1)"}},"error_y":{"color":"rgba(102,194,165,1)"},"error_x":{"color":"rgba(102,194,165,1)"},"xaxis":"x2","yaxis":"y2","frame":null,"showlegend":false},{"x":[1.4,1.5,1.5,1.3,1.5,1.3,1.6,1,1.3,1.4,1,1.5,1,1.4,1.3,1.4,1.5,1,1.5,1.1,1.8,1.3,1.5,1.2,1.3,1.4,1.4,1.7,1.5,1,1.1,1,1.2,1.6,1.5,1.6,1.5,1.3,1.3,1.3,1.2,1.4,1.2,1,1.3,1.2,1.3,1.3,1.1,1.3],"text":["versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />","versicolor<br />Petal.Width<br />"],"type":"histogram","name":"Petal.Width","marker":{"color":"rgba(252,141,98,1)","line":{"color":"rgba(252,141,98,1)"}},"error_y":{"color":"rgba(252,141,98,1)"},"error_x":{"color":"rgba(252,141,98,1)"},"xaxis":"x2","yaxis":"y2","frame":null,"showlegend":false},{"x":[7,6.4,6.9,5.5,6.5,5.7,6.3,4.9,6.6,5.2,5,5.9,6,6.1,5.6,6.7,5.6,5.8,6.2,5.6,5.9,6.1,6.3,6.1,6.4,6.6,6.8,6.7,6,5.7,5.5,5.5,5.8,6,5.4,6,6.7,6.3,5.6,5.5,5.5,6.1,5.8,5,5.6,5.7,5.7,6.2,5.1,5.7],"text":["versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />","versicolor<br />Sepal.Length<br />"],"type":"histogram","name":"Sepal.Length","marker":{"color":"rgba(141,160,203,1)","line":{"color":"rgba(141,160,203,1)"}},"error_y":{"color":"rgba(141,160,203,1)"},"error_x":{"color":"rgba(141,160,203,1)"},"xaxis":"x2","yaxis":"y2","frame":null,"showlegend":false},{"x":[3.2,3.2,3.1,2.3,2.8,2.8,3.3,2.4,2.9,2.7,2,3,2.2,2.9,2.9,3.1,3,2.7,2.2,2.5,3.2,2.8,2.5,2.8,2.9,3,2.8,3,2.9,2.6,2.4,2.4,2.7,2.7,3,3.4,3.1,2.3,3,2.5,2.6,3,2.6,2.3,2.7,3,2.9,2.9,2.5,2.8],"text":["versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />","versicolor<br />Sepal.Width<br />"],"type":"histogram","name":"Sepal.Width","marker":{"color":"rgba(231,138,195,1)","line":{"color":"rgba(231,138,195,1)"}},"error_y":{"color":"rgba(231,138,195,1)"},"error_x":{"color":"rgba(231,138,195,1)"},"xaxis":"x2","yaxis":"y2","frame":null,"showlegend":false},{"x":[6,5.1,5.9,5.6,5.8,6.6,4.5,6.3,5.8,6.1,5.1,5.3,5.5,5,5.1,5.3,5.5,6.7,6.9,5,5.7,4.9,6.7,4.9,5.7,6,4.8,4.9,5.6,5.8,6.1,6.4,5.6,5.1,5.6,6.1,5.6,5.5,4.8,5.4,5.6,5.1,5.1,5.9,5.7,5.2,5,5.2,5.4,5.1],"text":["virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />","virginica<br />Petal.Length<br />"],"type":"histogram","name":"Petal.Length","marker":{"color":"rgba(102,194,165,1)","line":{"color":"rgba(102,194,165,1)"}},"error_y":{"color":"rgba(102,194,165,1)"},"error_x":{"color":"rgba(102,194,165,1)"},"xaxis":"x3","yaxis":"y3","frame":null,"showlegend":false},{"x":[2.5,1.9,2.1,1.8,2.2,2.1,1.7,1.8,1.8,2.5,2,1.9,2.1,2,2.4,2.3,1.8,2.2,2.3,1.5,2.3,2,2,1.8,2.1,1.8,1.8,1.8,2.1,1.6,1.9,2,2.2,1.5,1.4,2.3,2.4,1.8,1.8,2.1,2.4,2.3,1.9,2.3,2.5,2.3,1.9,2,2.3,1.8],"text":["virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />","virginica<br />Petal.Width<br />"],"type":"histogram","name":"Petal.Width","marker":{"color":"rgba(252,141,98,1)","line":{"color":"rgba(252,141,98,1)"}},"error_y":{"color":"rgba(252,141,98,1)"},"error_x":{"color":"rgba(252,141,98,1)"},"xaxis":"x3","yaxis":"y3","frame":null,"showlegend":false},{"x":[6.3,5.8,7.1,6.3,6.5,7.6,4.9,7.3,6.7,7.2,6.5,6.4,6.8,5.7,5.8,6.4,6.5,7.7,7.7,6,6.9,5.6,7.7,6.3,6.7,7.2,6.2,6.1,6.4,7.2,7.4,7.9,6.4,6.3,6.1,7.7,6.3,6.4,6,6.9,6.7,6.9,5.8,6.8,6.7,6.7,6.3,6.5,6.2,5.9],"text":["virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />","virginica<br />Sepal.Length<br />"],"type":"histogram","name":"Sepal.Length","marker":{"color":"rgba(141,160,203,1)","line":{"color":"rgba(141,160,203,1)"}},"error_y":{"color":"rgba(141,160,203,1)"},"error_x":{"color":"rgba(141,160,203,1)"},"xaxis":"x3","yaxis":"y3","frame":null,"showlegend":false},{"x":[3.3,2.7,3,2.9,3,3,2.5,2.9,2.5,3.6,3.2,2.7,3,2.5,2.8,3.2,3,3.8,2.6,2.2,3.2,2.8,2.8,2.7,3.3,3.2,2.8,3,2.8,3,2.8,3.8,2.8,2.8,2.6,3,3.4,3.1,3,3.1,3.1,3.1,2.7,3.2,3.3,3,2.5,3,3.4,3],"text":["virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />","virginica<br />Sepal.Width<br />"],"type":"histogram","name":"Sepal.Width","marker":{"color":"rgba(231,138,195,1)","line":{"color":"rgba(231,138,195,1)"}},"error_y":{"color":"rgba(231,138,195,1)"},"error_x":{"color":"rgba(231,138,195,1)"},"xaxis":"x3","yaxis":"y3","frame":null,"showlegend":false}],"layout":{"xaxis":{"domain":[0,1],"automargin":true,"anchor":"y"},"xaxis2":{"domain":[0,1],"automargin":true,"anchor":"y2"},"xaxis3":{"domain":[0,1],"automargin":true,"anchor":"y3"},"yaxis3":{"domain":[0,0.313333333333333],"automargin":true,"anchor":"x3"},"yaxis2":{"domain":[0.353333333333333,0.646666666666667],"automargin":true,"anchor":"x2"},"yaxis":{"domain":[0.686666666666667,1],"automargin":true,"anchor":"x"},"margin":{"b":40,"l":60,"t":25,"r":10},"hovermode":"closest","showlegend":true},"attrs":{"327c561966b2":{"x":{},"text":{},"color":{},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"histogram"},"327c62f842e3":{"x":{},"text":{},"color":{},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"histogram"},"327c16b04910":{"x":{},"text":{},"color":{},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"histogram"}},"source":"A","config":{"modeBarButtonsToAdd":[{"name":"Collaborate","icon":{"width":1000,"ascent":500,"descent":-50,"path":"M487 375c7-10 9-23 5-36l-79-259c-3-12-11-23-22-31-11-8-22-12-35-12l-263 0c-15 0-29 5-43 15-13 10-23 23-28 37-5 13-5 25-1 37 0 0 0 3 1 7 1 5 1 8 1 11 0 2 0 4-1 6 0 3-1 5-1 6 1 2 2 4 3 6 1 2 2 4 4 6 2 3 4 5 5 7 5 7 9 16 13 26 4 10 7 19 9 26 0 2 0 5 0 9-1 4-1 6 0 8 0 2 2 5 4 8 3 3 5 5 5 7 4 6 8 15 12 26 4 11 7 19 7 26 1 1 0 4 0 9-1 4-1 7 0 8 1 2 3 5 6 8 4 4 6 6 6 7 4 5 8 13 13 24 4 11 7 20 7 28 1 1 0 4 0 7-1 3-1 6-1 7 0 2 1 4 3 6 1 1 3 4 5 6 2 3 3 5 5 6 1 2 3 5 4 9 2 3 3 7 5 10 1 3 2 6 4 10 2 4 4 7 6 9 2 3 4 5 7 7 3 2 7 3 11 3 3 0 8 0 13-1l0-1c7 2 12 2 14 2l218 0c14 0 25-5 32-16 8-10 10-23 6-37l-79-259c-7-22-13-37-20-43-7-7-19-10-37-10l-248 0c-5 0-9-2-11-5-2-3-2-7 0-12 4-13 18-20 41-20l264 0c5 0 10 2 16 5 5 3 8 6 10 11l85 282c2 5 2 10 2 17 7-3 13-7 17-13z m-304 0c-1-3-1-5 0-7 1-1 3-2 6-2l174 0c2 0 4 1 7 2 2 2 4 4 5 7l6 18c0 3 0 5-1 7-1 1-3 2-6 2l-173 0c-3 0-5-1-8-2-2-2-4-4-4-7z m-24-73c-1-3-1-5 0-7 2-2 3-2 6-2l174 0c2 0 5 0 7 2 3 2 4 4 5 7l6 18c1 2 0 5-1 6-1 2-3 3-5 3l-174 0c-3 0-5-1-7-3-3-1-4-4-5-6z"},"click":"function(gd) { \n        // is this being viewed in RStudio?\n        if (location.search == '?viewer_pane=1') {\n          alert('To learn about plotly for collaboration, visit:\\n https://cpsievert.github.io/plotly_book/plot-ly-for-collaboration.html');\n        } else {\n          window.open('https://cpsievert.github.io/plotly_book/plot-ly-for-collaboration.html', '_blank');\n        }\n      }"}],"cloud":false},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"subplot":true,"base_url":"https://plot.ly"},"evals":["config.modeBarButtonsToAdd.0.click"],"jsHooks":[]}</script>
<!--/html_preserve-->
### Split Features and Response

We will split our data set into two separate data sets, one containing the 4 features and the other containing the response variable Species:

``` r
# Features
x_df <- iris %>% 
  dplyr::select(-Species)

# Response
y_df <- iris %>% 
  dplyr::select(Species)
```

### Standardize the features

The first step is to standardise our data and then to center the data by subtracting the mean from each data point. Centering the data is an important step in the PCA process.

``` r
# Standardize data
x_standard_df <- data.frame(apply(x_df,
                                  2,
                                  FUN = function(x){(x - min(x))/(max(x) - min(x))}))

# Center data
x_centered_df <- data.frame(apply(x_standard_df,
                                2,
                                FUN = function(x){ x - mean(x)}))
```

### Convert from DataFrame to Matrix

We'll convert our data to a matrix to allow for matrix multiplication:

``` r
x_centered_matrix <- as.matrix(x_centered_df)
```

### Covariance Matrix

We now calculate the covariance matrix of our data (We have calculated this the long way but we could alternatively use the cov() function in R):

``` r
cov_matrix <- (t(x_centered_matrix) %*% x_centered_matrix) / (nrow(x_centered_matrix) - 1)
```

### Eigenvectors

As mentioned, matrices can be thought of as linear tranformations of vectors. The covariance matrix happens to apply an important transformaton with respect to the data it is generated from. Given a vector *v*, applying the covariance matrix to *v* it will rotate *v* towards the direction of the most variation in the sample data. As this process is repeated it, the direction of *v* will slowly converge to the direction of the most variation. As we can recall from earlier, that is exactly what we're looking for when trying to calculate the prinipal components for PCA. Now, we could iteratively apply the covariance matrix transformation to some arbitrary vector and we will arrive at a point of convergence, or we could simply find a vector *v* such that applying the covariance matrix to *v* does not change its direction, namely the eigenvectors of the covariance matrix!

``` r
eigenvectors_df <- as.data.frame(eigen(cov_matrix)$vectors)

# take a look:
eigenvectors_df
```

    ##           V1           V2         V3         V4
    ## 1  0.4249421 -0.423202708 -0.7135724  0.3621300
    ## 2 -0.1507482 -0.903967112  0.3363160 -0.2168178
    ## 3  0.6162670  0.060383083 -0.0659003 -0.7824487
    ## 4  0.6456889  0.009839255  0.6110345  0.4578492

### Eigenvalues

Each eigenvector has a corresponding eigenvalue. This value corresponds to the magnitude of the transformation. That is, if we consider our eigenvector *e*, and apply our covariance matrix transformation to it, the eigenvalue tells us how much the eigenvector *e* will grow or shrink (remembering that the direction of the eigenvector does not change).

``` r
eigenvalues_df <- data.frame("Eigenvalue" = eigen(cov_matrix)$values)

# take a look:
eigenvalues_df
```

    ##    Eigenvalue
    ## 1 0.232453251
    ## 2 0.032468204
    ## 3 0.009596846
    ## 4 0.001764319

As for PCA, the eigenvalues tell us how much of the variability in the data is explained by each prinicpal component, the higher the eigenvalue, the more variability it explains. We can make this a little easier to intepret by creating a specific column:

``` r
# add variation and cumulative variation columns:
eigenvalues_df <- eigenvalues_df %>%
  mutate("Variation" = Eigenvalue / sum(Eigenvalue),
         "CumulativeVariation" = cumsum(Variation))

# take a look:
eigenvalues_df
```

    ##    Eigenvalue   Variation CumulativeVariation
    ## 1 0.232453251 0.841360382           0.8413604
    ## 2 0.032468204 0.117518082           0.9588785
    ## 3 0.009596846 0.034735614           0.9936141
    ## 4 0.001764319 0.006385922           1.0000000

We'll also store the number of eigenvalues as a variable for use with plotting, this is equal to the number of features:

``` r
num_eigenvalues <- nrow(eigenvalues_df)
```

### Scree Plot

A Scree Plot is a plot used to visualise how much of the variability in the original data set is being explained by each principal component. Despite being all a little subjective, it is also a useful plot when determining how many principal componenets to keep.

``` r
# Plotly Plot:
screeplot <- plot_ly() %>%
  # Add Variation Bars
  add_trace(x = 1:num_eigenvalues,
            y = eigenvalues_df$Variation,
            name = "Variation",
            type = "bar",
            text = ~paste0("PC", 1:num_eigenvalues, "\n",
                           "Variation Explained: ", round(eigenvalues_df$Variation * 100,2), "%", "\n",
                           "Eigenvalue: ", round(eigenvalues_df$Eigenvalue,2)),
  hoverinfo = 'text') %>%
  # Add Cumulative Line
  add_trace(x = 1:num_eigenvalues,
            y = eigenvalues_df$CumulativeVariation,
            name = "Cumulative Variation",
            type = "scatter",
            mode = "lines+markers",
            text = ~paste0("PC", 1:num_eigenvalues, "\n",
                           "Cumulative Variation Explained: ", round(eigenvalues_df$CumulativeVariation * 100,2), "%", "\n",
                           "Eigenvalue: ", round(eigenvalues_df$Eigenvalue,2)),
            hoverinfo = 'text') %>%
  layout(title = "Scree Plot for PCA on Iris Data",
         xaxis = list(title = "Principal Components"),
         yaxis = list(title = "Variation",
                      tickformat = ',.0%'))

screeplot
```

<!--html_preserve-->

<script type="application/json" data-for="htmlwidget-ac8068c5d42bd2101709">{"x":{"visdat":{"327c13b13be5":["function () ","plotlyVisDat"]},"cur_data":"327c13b13be5","attrs":{"327c13b13be5":{"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"x":[1,2,3,4],"y":[0.841360382131543,0.117518081860298,0.0347356140879326,0.00638592192022576],"name":"Variation","type":"bar","text":{},"hoverinfo":"text","inherit":true},"327c13b13be5.1":{"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"x":[1,2,3,4],"y":[0.841360382131543,0.958878463991842,0.993614078079774,1],"name":"Cumulative Variation","type":"scatter","mode":"lines+markers","text":{},"hoverinfo":"text","inherit":true}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"title":"Scree Plot for PCA on Iris Data","xaxis":{"domain":[0,1],"automargin":true,"title":"Principal Components"},"yaxis":{"domain":[0,1],"automargin":true,"title":"Variation","tickformat":",.0%"},"hovermode":"closest","showlegend":true},"source":"A","config":{"modeBarButtonsToAdd":[{"name":"Collaborate","icon":{"width":1000,"ascent":500,"descent":-50,"path":"M487 375c7-10 9-23 5-36l-79-259c-3-12-11-23-22-31-11-8-22-12-35-12l-263 0c-15 0-29 5-43 15-13 10-23 23-28 37-5 13-5 25-1 37 0 0 0 3 1 7 1 5 1 8 1 11 0 2 0 4-1 6 0 3-1 5-1 6 1 2 2 4 3 6 1 2 2 4 4 6 2 3 4 5 5 7 5 7 9 16 13 26 4 10 7 19 9 26 0 2 0 5 0 9-1 4-1 6 0 8 0 2 2 5 4 8 3 3 5 5 5 7 4 6 8 15 12 26 4 11 7 19 7 26 1 1 0 4 0 9-1 4-1 7 0 8 1 2 3 5 6 8 4 4 6 6 6 7 4 5 8 13 13 24 4 11 7 20 7 28 1 1 0 4 0 7-1 3-1 6-1 7 0 2 1 4 3 6 1 1 3 4 5 6 2 3 3 5 5 6 1 2 3 5 4 9 2 3 3 7 5 10 1 3 2 6 4 10 2 4 4 7 6 9 2 3 4 5 7 7 3 2 7 3 11 3 3 0 8 0 13-1l0-1c7 2 12 2 14 2l218 0c14 0 25-5 32-16 8-10 10-23 6-37l-79-259c-7-22-13-37-20-43-7-7-19-10-37-10l-248 0c-5 0-9-2-11-5-2-3-2-7 0-12 4-13 18-20 41-20l264 0c5 0 10 2 16 5 5 3 8 6 10 11l85 282c2 5 2 10 2 17 7-3 13-7 17-13z m-304 0c-1-3-1-5 0-7 1-1 3-2 6-2l174 0c2 0 4 1 7 2 2 2 4 4 5 7l6 18c0 3 0 5-1 7-1 1-3 2-6 2l-173 0c-3 0-5-1-8-2-2-2-4-4-4-7z m-24-73c-1-3-1-5 0-7 2-2 3-2 6-2l174 0c2 0 5 0 7 2 3 2 4 4 5 7l6 18c1 2 0 5-1 6-1 2-3 3-5 3l-174 0c-3 0-5-1-7-3-3-1-4-4-5-6z"},"click":"function(gd) { \n        // is this being viewed in RStudio?\n        if (location.search == '?viewer_pane=1') {\n          alert('To learn about plotly for collaboration, visit:\\n https://cpsievert.github.io/plotly_book/plot-ly-for-collaboration.html');\n        } else {\n          window.open('https://cpsievert.github.io/plotly_book/plot-ly-for-collaboration.html', '_blank');\n        }\n      }"}],"cloud":false},"data":[{"x":[1,2,3,4],"y":[0.841360382131543,0.117518081860298,0.0347356140879326,0.00638592192022576],"name":"Variation","type":"bar","text":["PC1<br />Variation Explained: 84.14%<br />Eigenvalue: 0.23","PC2<br />Variation Explained: 11.75%<br />Eigenvalue: 0.03","PC3<br />Variation Explained: 3.47%<br />Eigenvalue: 0.01","PC4<br />Variation Explained: 0.64%<br />Eigenvalue: 0"],"hoverinfo":["text","text","text","text"],"marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"error_y":{"color":"rgba(31,119,180,1)"},"error_x":{"color":"rgba(31,119,180,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":[1,2,3,4],"y":[0.841360382131543,0.958878463991842,0.993614078079774,1],"name":"Cumulative Variation","type":"scatter","mode":"lines+markers","text":["PC1<br />Cumulative Variation Explained: 84.14%<br />Eigenvalue: 0.23","PC2<br />Cumulative Variation Explained: 95.89%<br />Eigenvalue: 0.03","PC3<br />Cumulative Variation Explained: 99.36%<br />Eigenvalue: 0.01","PC4<br />Cumulative Variation Explained: 100%<br />Eigenvalue: 0"],"hoverinfo":["text","text","text","text"],"marker":{"color":"rgba(255,127,14,1)","line":{"color":"rgba(255,127,14,1)"}},"error_y":{"color":"rgba(255,127,14,1)"},"error_x":{"color":"rgba(255,127,14,1)"},"line":{"color":"rgba(255,127,14,1)"},"xaxis":"x","yaxis":"y","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"base_url":"https://plot.ly"},"evals":["config.modeBarButtonsToAdd.0.click"],"jsHooks":[]}</script>
<!--/html_preserve-->
### Create Principal Components

Now we can transform our data onto our new linear combinations of our old features.

### Transformation Matrix

First we build our transformation matrix:

``` r
transformation_matrix <- as.matrix(eigenvectors_df[,1:2])
```

### Transform the Data

Take the dot product of our centered data and our transformation matrix:

``` r
transformed_df <- as.data.frame(x_centered_matrix %*% transformation_matrix)

# take a look:
head(transformed_df, n = 5)
```

    ##           V1          V2
    ## 1 -0.6307029 -0.10757791
    ## 2 -0.6229049  0.10425983
    ## 3 -0.6695204  0.05141706
    ## 4 -0.6541528  0.10288487
    ## 5 -0.6487881 -0.13348758

Rename the columns:

``` r
names(transformed_df) <- c("PC1", "PC2")
```

Bolt on our response variable:

``` r
transformed_df <- cbind(transformed_df,
                          y_df)
```

### Scatterplot

Now that we only have two features, we can plot all the information in our data set in a single 2D scatter plot:

``` r
# Plot
scatterplot <- plot_ly(data = transformed_df) %>%
  add_trace(x = ~PC1,
            y = ~PC2,
            color = ~Species,
            type = "scatter",
            mode = "markers") %>%
  layout(title = "Iris Species after PCA")

scatterplot
```

<!--html_preserve-->

<script type="application/json" data-for="htmlwidget-f81e89a666ec85294069">{"x":{"visdat":{"327c210510e0":["function () ","plotlyVisDat"]},"cur_data":"327c210510e0","attrs":{"327c210510e0":{"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"x":{},"y":{},"color":{},"type":"scatter","mode":"markers","inherit":true}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"title":"Iris Species after PCA","xaxis":{"domain":[0,1],"automargin":true,"title":"PC1"},"yaxis":{"domain":[0,1],"automargin":true,"title":"PC2"},"hovermode":"closest","showlegend":true},"source":"A","config":{"modeBarButtonsToAdd":[{"name":"Collaborate","icon":{"width":1000,"ascent":500,"descent":-50,"path":"M487 375c7-10 9-23 5-36l-79-259c-3-12-11-23-22-31-11-8-22-12-35-12l-263 0c-15 0-29 5-43 15-13 10-23 23-28 37-5 13-5 25-1 37 0 0 0 3 1 7 1 5 1 8 1 11 0 2 0 4-1 6 0 3-1 5-1 6 1 2 2 4 3 6 1 2 2 4 4 6 2 3 4 5 5 7 5 7 9 16 13 26 4 10 7 19 9 26 0 2 0 5 0 9-1 4-1 6 0 8 0 2 2 5 4 8 3 3 5 5 5 7 4 6 8 15 12 26 4 11 7 19 7 26 1 1 0 4 0 9-1 4-1 7 0 8 1 2 3 5 6 8 4 4 6 6 6 7 4 5 8 13 13 24 4 11 7 20 7 28 1 1 0 4 0 7-1 3-1 6-1 7 0 2 1 4 3 6 1 1 3 4 5 6 2 3 3 5 5 6 1 2 3 5 4 9 2 3 3 7 5 10 1 3 2 6 4 10 2 4 4 7 6 9 2 3 4 5 7 7 3 2 7 3 11 3 3 0 8 0 13-1l0-1c7 2 12 2 14 2l218 0c14 0 25-5 32-16 8-10 10-23 6-37l-79-259c-7-22-13-37-20-43-7-7-19-10-37-10l-248 0c-5 0-9-2-11-5-2-3-2-7 0-12 4-13 18-20 41-20l264 0c5 0 10 2 16 5 5 3 8 6 10 11l85 282c2 5 2 10 2 17 7-3 13-7 17-13z m-304 0c-1-3-1-5 0-7 1-1 3-2 6-2l174 0c2 0 4 1 7 2 2 2 4 4 5 7l6 18c0 3 0 5-1 7-1 1-3 2-6 2l-173 0c-3 0-5-1-8-2-2-2-4-4-4-7z m-24-73c-1-3-1-5 0-7 2-2 3-2 6-2l174 0c2 0 5 0 7 2 3 2 4 4 5 7l6 18c1 2 0 5-1 6-1 2-3 3-5 3l-174 0c-3 0-5-1-7-3-3-1-4-4-5-6z"},"click":"function(gd) { \n        // is this being viewed in RStudio?\n        if (location.search == '?viewer_pane=1') {\n          alert('To learn about plotly for collaboration, visit:\\n https://cpsievert.github.io/plotly_book/plot-ly-for-collaboration.html');\n        } else {\n          window.open('https://cpsievert.github.io/plotly_book/plot-ly-for-collaboration.html', '_blank');\n        }\n      }"}],"cloud":false},"data":[{"x":[-0.630702931394452,-0.622904942531991,-0.669520395417932,-0.654152758889205,-0.648788055988872,-0.535272778199451,-0.656537789993852,-0.625780498562827,-0.67564350431726,-0.64564461888523,-0.59740823823645,-0.638943190325622,-0.661612593447808,-0.751967943188854,-0.600371589001377,-0.552157226726167,-0.577053592987857,-0.603799228208583,-0.520483461331004,-0.612197555104896,-0.557674300248832,-0.579012675054555,-0.737784661697071,-0.506093857016596,-0.607607579234317,-0.590210587407839,-0.561527888493987,-0.608453779967403,-0.612617806800033,-0.638184784326627,-0.620099659732207,-0.524757301271296,-0.673044544340101,-0.627455378525961,-0.618740915699361,-0.644553755925189,-0.593932344171762,-0.687495706904689,-0.692369884878833,-0.613976550832879,-0.626048379635633,-0.609693995911714,-0.704932238607776,-0.514001658986719,-0.54351303713062,-0.607805187076069,-0.628656054593664,-0.670879139450778,-0.609212185966398,-0.629944525395457],"y":[-0.10757791034986,0.104259832937028,0.0514170597492874,0.102884871049092,-0.133487575901587,-0.289615723926643,-0.0107244911068701,-0.0571335411343441,0.200703283227261,0.0672080097270809,-0.21715195331778,-0.0325988374705539,0.115605494774021,0.171313322469912,-0.38024069175408,-0.515255982171859,-0.293709492263795,-0.107167941397103,-0.287627288907177,-0.219140388337246,-0.102109180124772,-0.181065123043011,-0.0905588210797345,-0.0279470845557685,-0.0295285112176898,0.0945510863158529,-0.0552901611445406,-0.118310099055323,-0.0816682447981343,0.0544873860021515,0.0803970515538778,-0.103336126387833,-0.344711846056945,-0.418257507899206,0.0676179786798386,0.0151267252957462,-0.155623875593153,-0.122141914064593,0.162014544801495,-0.0688891719240951,-0.0964357526916396,0.414325957354843,0.0866839521185406,-0.0921355195805023,-0.214636651047336,0.116425432679537,-0.218526915205716,0.0641961326233266,-0.205396322528029,-0.0204916868771548],"type":"scatter","mode":"markers","name":"setosa","marker":{"color":"rgba(102,194,165,1)","line":{"color":"rgba(102,194,165,1)"}},"textfont":{"color":"rgba(102,194,165,1)"},"error_y":{"color":"rgba(102,194,165,1)"},"error_x":{"color":"rgba(102,194,165,1)"},"line":{"color":"rgba(102,194,165,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":[0.279951766302762,0.21514137571474,0.322223106017358,0.0594030130682039,0.262515234599675,0.10383104269125,0.244850361700393,-0.171529385613276,0.214230599093413,0.0153249619092413,-0.113710323031238,0.137348379702638,0.0439928190248075,0.192559767326644,-0.00826091517708372,0.219485488886084,0.133272147604098,-0.000575757060344864,0.254345248899559,-0.00560800299963166,0.268168357713912,0.0988208151255346,0.289086480824499,0.145033537819376,0.159287092542212,0.213962718020608,0.291913781997853,0.369148997490774,0.186769115388362,-0.0687697501084309,-0.0215759775622097,-0.0589248844451808,0.0323412419171908,0.288906394485784,0.109664252144202,0.182266934251874,0.277724803163259,0.195615409696195,0.0376839264439527,0.0468406593392608,0.0554365940773262,0.17583338676507,0.049067622478764,-0.153444261018856,0.0669726607344689,0.033029374685133,0.066214254735474,0.135679197082316,-0.158634574923286,0.0620502279028439],"y":[-0.179245790116101,-0.110348920593413,-0.127368009863539,0.328502275260686,0.029580076067033,0.121781742395238,-0.133801733023805,0.352976762209426,-0.0206607889697108,0.2124945091325,0.49392920095416,0.0206894997854326,0.306159510795135,0.0395507760160903,0.0866610980849196,-0.109383927658235,0.05902671840755,0.142367732751539,0.289815304400862,0.239572671798177,-0.0472705335335205,0.0696420088147936,0.169157552923831,0.0763961344520521,-0.000219853643072813,-0.0599630005270064,-0.00404990108640184,-0.0643480719527561,0.049669491590023,0.185648007377039,0.287970156845117,0.286536745808072,0.141140786488478,0.131550705731463,0.0825379799870521,-0.138247021164605,-0.105903632452613,0.23855099727983,0.0541130121648824,0.253171682577732,0.219190185620649,0.000862037590324971,0.179829524914243,0.378886427761152,0.168132343273602,0.0429708545066616,0.0810461198008966,0.0232914079364293,0.28913984698834,0.117687974058086],"type":"scatter","mode":"markers","name":"versicolor","marker":{"color":"rgba(252,141,98,1)","line":{"color":"rgba(252,141,98,1)"}},"textfont":{"color":"rgba(252,141,98,1)"},"error_y":{"color":"rgba(252,141,98,1)"},"error_x":{"color":"rgba(252,141,98,1)"},"line":{"color":"rgba(252,141,98,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":[0.622771338435538,0.346009608583496,0.617986434427958,0.417789308803932,0.563621247537038,0.75012259895741,0.135857804188558,0.608945211983124,0.511020214575814,0.720608541108758,0.424135061556644,0.437723702357388,0.540793776449707,0.363226514071259,0.474246947648372,0.513932630778508,0.424670823702255,0.749026038654557,0.872194271608288,0.282963371925171,0.614733184216655,0.322133832050795,0.758030400927533,0.357235236653164,0.531036705520548,0.546962122568456,0.328704908361643,0.314783810599853,0.51658554295596,0.484826662531457,0.63304363236921,0.687490916651409,0.543489246141829,0.291133357625287,0.305410131193973,0.763507934573589,0.547805643596791,0.406585699107835,0.292534659172803,0.535871343618083,0.613864965109998,0.558343138898517,0.346009608583496,0.62381964388091,0.638651518264026,0.551461624000193,0.407146497265078,0.447142618982689,0.48820758528677,0.31206632253416],"y":[-0.116807265353241,0.156291874169239,-0.100519740542137,0.0268903690062114,-0.0305994289351611,-0.152133799900876,0.330462553548709,-0.0835018443012831,0.132575915381692,-0.334580389401145,-0.113914054113647,0.0878049735993083,-0.0693466165100361,0.242764624510414,0.12067642259155,-0.098881632297047,-0.0353096309990561,-0.463778390385399,-0.00933798116633885,0.318443776401804,-0.15356601790865,0.140500924191445,-0.0879453648761425,0.0950568670991496,-0.168539990576141,-0.187812428788828,0.0681237594631354,0.00557223965422001,0.0540299414162108,-0.115348658179965,-0.0592290939653752,-0.491179916123281,0.0544399103689685,0.0582085480679753,0.161757643799114,-0.168186703206552,-0.158976298984628,-0.0612192965507823,0.016304428359683,-0.119790985725552,-0.0930029331192011,-0.122041374072901,0.156291874169239,-0.139763502950323,-0.16690011476511,-0.0598413740676337,0.17182087081915,-0.0375600193464047,-0.149677521316211,0.0311303854022981],"type":"scatter","mode":"markers","name":"virginica","marker":{"color":"rgba(141,160,203,1)","line":{"color":"rgba(141,160,203,1)"}},"textfont":{"color":"rgba(141,160,203,1)"},"error_y":{"color":"rgba(141,160,203,1)"},"error_x":{"color":"rgba(141,160,203,1)"},"line":{"color":"rgba(141,160,203,1)"},"xaxis":"x","yaxis":"y","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"base_url":"https://plot.ly"},"evals":["config.modeBarButtonsToAdd.0.click"],"jsHooks":[]}</script>
<!--/html_preserve-->
