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

*server.R* 
 This file runs the server side of your code. Any modelling, computation, and data loading will occur here.

*ui.R* 
 This file contains the instructions for building a shiny application. The pieces to build a the front-end of the application are here. They are automaticaly updated based on the actions that happen in the backend server. Any changes made to controls here are also passed back to the server for processing.



