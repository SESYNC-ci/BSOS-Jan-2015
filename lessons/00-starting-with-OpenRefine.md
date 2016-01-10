---
layout: lesson
title: Open Refine
---
# Open Refine
(Adapted from: https://github.com/tracykteal/openrefine-gapminder/blob/gh-pages/00-starting-with-OpenRefine.md)

--------------------------------------------------

# Objectives

* Motivate participants to clean, organize, enhance data before insert into a database or merging data with other data files.
* Introduce participants to Open Refine as a powerful data-cleaning tool.

* Introduce concept of facets
* Show power of include / exclude, sort by name / count
* Show the power of clustering algorithms to reveal data patterns, data snafus
* Show the power of undo / redo.
* Can be used to introduce
 - scripting
 - regular expressions
 - APIs

If there's time: 
* Encourage dataset exploration; look at the data with the visualization tools in Open Refine.
* If time, show call to an API, a web service (JSON example here from a locality georeferencing service)
* If time, show how to parse the JSON returned from the service.

----------------------------------------------------

# Motivations for the Open Refine Lesson

* It's really important that you know what you did. More journals/grants/etc. are also making it important for them to know what you did. You can capture all steps done to your data in Open Refine to the raw file and share with your publication as supplemental material.
* All steps are easily reversed in Refine.
* You _must_ save your work to a new file; Refine _does not_ modify your original dataset.
* Data is often very messy - and this tool saves a lot of cleaning headaches.
* Data cleaning steps often need repeating with multiple files. Refine is perfect for speeding up repetitive tasks.

# Before we get started

* Check that you have Firefox browser installed. Open Refine runs in this browser. It will not run in IE.
* Download software from http://openrefine.org if you have not done this yet.
* Unzip the downloaded file into a directory. Name that directory something like Open-Refine
* Note that "double-clicking" a zipped file on a windows machine sometimes results in a correctly unzipped set of files, other times, this is not successful. Try installing 7-Zip and use 7-Zip to extract all files from the zipped file to the desired directory.
* Go to your newly created Open-Refine directory.
* Click the google-refine.exe file to launch Open Refine.
* Note, this is a Java program that runs on your machine (not in the cloud). It runs inside the Firefox browser, but no web connection is needed.

# Basics of Open Refine

You can find out a lot more about Open Refine at http://openrefine.org and check out some great introductory videos. As with other programs of this type, Open Refine libraries are available too, where you can find a script you need and copy it into your Refine instance to run it on your dataset.

* Open source.
* A large growing community, from novice to expert, ready to help.
* Works with large-ish datasets (100,000 rows). Does not scale to many millions. (yet).

# Demo of Open Refine

Start the program. (Double-click on the google-refine.exe file. Java services will start on your machine, and Refine will open in your Firefox browser).

Note the file types Open Refine handles: TSV, CSF, *SV, Excel (.xls .xlsx), JSON, XML, RDF as XML, Google Data documents. Support for other formats can be added with Google Refine extensions.

Rather than having you download the file and open it in OpenRefine like you would in Excel, we are going to get the data straight from a webpage. https://goo.gl/38QDoy is a URL for  Gapminder data that has been adapted for the lesson to include adding known errors to demonstrate use case for OpenRefine.

_Once Refine is open, you'll be asked if you want to Create, Open, or Import a Project._

* Click "Web Addresses" and paste in the link above. Then click "Next."
* Refine gives you a preview - a chance to show you it understood the file. If, for example, your file was really tab-delimited, the preview might look strange, you would choose the correct separator in the box shown and click "update preview."
* If all looks well, give the project a better name and click _Create Project._
* By default you see the first 10 rows of your data, but you can show up to 50.

## Faceting

* Scroll over to the 'country' column
* Click the down arrow and choose > Facet > Text facet
* In the left margin, you'll see a box containing every unique, distinct value in the Country column and Refine shows you how many times that value occurs in the column (a count), and allows you to sort (order) your facets by name or count.
* Filter. Note that by clicking on a country name you limit the data displayed to that country only.
* Edit. Note that at any time, in any cell of the Facet box, or data cell in the Refine window, you have access to "edit" and can fix an error immediately. Refine will even ask you if you'd like to make that same correction to every value it finds like that one (or not).

## Cluster

* One of the most magical bits of Refine, the moment you realize what you've been missing. Refine has several clustering algorithms built in. Experiment with them, and follow the link inside Refine, to learn more about these algorithms and how they work. https://github.com/OpenRefine/OpenRefine/wiki/Clustering-In-Depth
* In this example, in the country Text Facet we created in the step above, click the _Cluster_ button.
* In the resulting pop-up window, you can change the algorithm method, and keying function. Try different combinations to see the difference.
* For example, with this dataset, the _nearest neighbor_ method with the _PPM_ keying function shows the power of clustering the best.
* Countries have had different names over time or people inputting the data have mis-spelled the country name. In order to look at the same country over time though, it needs to have a consistent name. Intentional errors have been introduced to show how errors (typos) in any position can be found with this method, and there are instances of legitimate changes in country names over time. All errors or differences can then be fixed by entering the correct value in the box on the right. Often, the algorithm has guessed correctly.
* After corrections are made in this window, Merge and Re-cluster.
* Note that after you merge and re-cluster, if you sort by count, the highest and lowest count is 12, indicating that the data are now correct since the rows represent a country-year, and there are 12 years per country.

## Numeric Faceting and Filtering

* Select the drop-down arrow next to lifeExp and click "Numeric Facet." Notice how in the left-hand column you get a graphical representation of the distribution along with a two-ended slider. You can use the slider to limit the rows shown to part of the distribution.
* Now, select the drop-down arrow by gdpPerCap and click "Numeric Facet." Both filters are now applied and you can see the outliers, for example, which country/years have a low life expectancy but a high GDP per capita? 


## Scripts

* Refine saves every change, every edit you make to the dataset in a file you can save on your machine.
* If you had 20 files to clean, and they all had the same type of errors, and all files had the same columns, you could save the script, open a new file to clean, paste in the script and run it. Voila, clean data.
* In the Undo / Redo section, click Extract, save the bits desired using the check boxes. Save the code in a .txt file. To run these steps on a new dataset, import the new dataset into Refine, open the Extract / Apply section, paste in the .txt file, click Apply.

## Export

* Save your work when you are done by exporting it in the desire format. Save your files with meaningful names, no spaces. Refine does not change your original dataset.

#### Time estimate for this demo.
* Takes about 20 - 30 minutes to do a good demo.
* If students are going to install and then try this tool out on the provided dataset or their own dataset, it will take longer.
* Mac users with the newest operating system will have to allow this to run by "allowing everything" to run. They can change the setting back after the exercise.
* Some students will run into issues with
  - unzipping
  - finding the .exe file once the software has been unzipped

