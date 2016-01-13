# Introduction to R-Shiny

R Shiny is an R packge which allows you to quickly develop interactive web sites.

* R Shiny http://shiny.rstudio.com/
* R Shiny Gallery - http://shiny.rstudio.com/gallery/
* Self-hosted Shiny Apps - https://www.shinyapps.io/

# Getting Started

Everything you need to get started with Shiny is in the shiny library included in R Studio.

You should have a copy of the gap-minder data already downloaded and be familiar with read.csv to load the data.

<pre>
> install.packages("shiny")
> install.packages("RCurl")
</pre>

After you're started, load and run the demo application to make sure that everything has installed correctly.

<pre>
> library(shiny)
> runExample("01_hello")
</pre>

This will start up a simple R shiny library which does one simple thing, create a simple app which has a histogram manipulated by a slider.

# Create your own app.

While you have the 01_hello example, you're going to copy and paste the two files which make up the app into a new directory and make sure these run.

*Type Along 1* 

* Have all students run the example
* Have them create a new project directory and switch to it
* Have them create two new files, ui.R and server.R which contain the contents of the example copied.
* Click 'Stop' to terminate the example and click the 'Run App' 

Now that they have the application running, explain the two pieces which comprise an R Shiny application.

*server.R* - This file runs the server side of your code. Any modelling, computation, and data loading will occur here.

*ui.R* - This file contains the instructions for building a shiny application. The pieces to build a the front-end of the application are here. They are automaticaly updated based on the actions that happen in the backend server. Any changes made to controls here are also passed back to the server for processing.

# Step One, load the gampinder data

We're going to load the gapminder data a little differently this time. Rather than using the downloaded copy, we're going to load it directly from the web. 

First, we need to include the RCurl library by doing the following:
<pre>
library(RCurl)
</pre>

Now, lets test to make sure you can load the data:
getURL("https://goo.gl/NpMmTZ")

What did that show? something not right? 

What happened was the web server decided to redirect you to a new location, however RCurl wasn't told to follow to the new location, we can fix this by passing some options to it.

getURL("https://goo.gl/NpMmTZ", opts=curlOptions(followlocation=TRUE))
read.csv(text=webdata)

## Update server UI

On the server side, modify the server.R script file in the following ways:

At the top add:

<pre>
library(RCurl)
webdata <- getURL("https://goo.gl/NpMmTZ", opts=curlOptions(followlocation=TRUE))
gapminder <- read.csv(text=webdata)
</pre>

Select these lines and hit ctrl-enter to make sure they run correctly.

Next we want to graph the data as is, using a static graph, there are two parts to this. First, add a space in ui.R to receive the plot and second, modify the server to fill that space.

Make the following changes to server.R

* At the top of server.R add in a library(ggplot2)
* Remove the contents of the renderPlot function and replace them with 
<pre>
plot <- ggplot(data=gapminder, aes(x=year,y=lifeExp,by=country,color=continent)) + geom_line()
print(plot)
</pre>

# Step Two, wire in some controls.

Now, lets wire in some basic controls to limit the year. To do this, we're going to first repurpose the existing slider.

In the ui.R, do the following:

* Rename the application from Hello Shiny to something more meaningful
* On SliderInput, change "bins" to years and change the second value to the new title "Years"
* Copy the three data loading lines from server.R to the top
<pre>
<pre>
library(RCurl)
webdata <- getURL("https://goo.gl/NpMmTZ", opts=curlOptions(followlocation=TRUE))
gapminder <- read.csv(text=webdata)
</pre>
* Now since you have the data available, work with your neighbor to replace the min and max with the min and max from the 'gapminder' variable
* Answer: 
<pre>
 min = min(gapminder$year),
 max = max(gapminder$year),
</pre>
* After you have that, replace value with the min

Save your application and run it and you should notice a few things, mainly the dates and ugly formatting.
* Fix the formatting and re-run your application
* sep = ""
* step = 1

Now, your slider works, but doesn't do anything, so we have to update the server.R file. Remember how we could subset data w/in a dataframe before? We can use that same subsetting to create take values from the slider and filter the dataframe.

data=gapminder[gapminder$year > input$year[1],]

For the next, lets add the top slider:
* modify the sliderInput to include multiple values as a vector, this will add additional sliders
<pre>value = c(min(gapminder$year),max(gapminder$year))</pre>
* Challenge: modify the gapminder data in server.R to test for the second slider, hint it will need to use index on years

# Step three, filtering by country

This will involve creating a completely new UI element and modifying the server data link to include a new widget

After the sliderInput, create a new widget called checkboxGroupInput("continents", "Continents", levels(gapminder$continent)

Challenge: You now have a list of results in input$continents, modify teh data expression to include these items
A: add & gapminder$continent %in% input$continents
