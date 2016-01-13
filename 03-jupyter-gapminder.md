# Using Gapminder data in Jupyter


You're looking at a new Jupyter notebook. THis project was originally spawned from the iPython project to create a more general purpose lab-notebook for code. Its a good teaching tool for combining code, visualizations and data in one convenient form. Notebooks are generally portable and can be run on a shared notbook server, or your own desktop.

Today we're going to use a demo service that's freely available. 

Go to http://tmpnb.org/ to get your own notebook. Please note, this is a disposable, test instance of a jupyter notebook so your code will be deleted when you log out.

The first thing we need to do is upload the 5-year gapminder data. Find the gapminder data on your desktop/downloads folder and upload it to the kernel by selecting and uploading it.

Second, create a new R notebook.

In the first block, enter your library and data loading statements. 

<pre>
require(ggplot2)
gapminder <- read.csv("gapminder-FiveYearData.csv)
<pre>

Press the run button and you'll see some output regarding data being loaded. 

Lets add a header to this. Select the cell, go to insert, insert cell above.

Change the type of cell from code to markdown and enter

<pre>
# Load gapminder data

we will not load the gm data
</pre>

Now, in the empty cell below, run 

<pre>
ggplot(data=gapminder, aes(x=year,y=lifeExp,by=country, color=continent)) + geom_line()
</pre>

