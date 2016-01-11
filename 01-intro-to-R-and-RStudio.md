# Overview of R

(Highly abbreviated version of R lessons found here: https://github.com/datacarpentry/2015-06-30-FederalReserveBoard/wiki.)


Basic Layout
Workflow

R as calc
Math functions
Comparisons

Variables and Assignment*

Managing Environ (use ls() as lead in/discussion about functions)

Project Management Universals and Whys (reproducible, making your life easier)
Importance of scripting and file org
Treating data as read-only
Output disposable
Separating cleaning from analysis code

Help in R
Google It/Stackoverflow

Data Strucutre
Quick Overview of Types
Focus on Dataframes

Read GapMinder URL into dataframe
Dataframe functions (head, names)
Subsetting dataframes

R/Twitter
http://www.r-bloggers.com/how-to-create-a-twitter-sentiment-analysis-using-r-and-shiny/







Basic layout

When you first open RStudio, you will be greeted by three panels:

    The interactive R console (entire left)
    Workspace/History (tabbed in upper right)
    Files/Plots/Packages/Help (tabbed in lower right)

Once you open files, such as R scripts, a scripting panel will also open in the top left.
Work flow within Rstudio

There are two main ways one can work within Rstudio.

    Test and play within the interactive R console then copy code into a .R file to run later.
    This works well when doing small tests and initially starting off.
    Becomes laboursome.
    Start writing in an .R file and use Rstudio’s command / short cut to push current line, selected lines or modified lines to the interactive R console.
    This is great way to start and work as all workings are saved for latter reference and can be read latter.

Tip: Pushing to the interactive R console

To run the current line click on the Run button just above the file pane. Or use the short cut which can be see by hovering the mouse over the button.

To run a block of code, select it and then Run. If you have modified a line of code within a block of code you have just run. There is no need to reselct the section and Run, you can use the next button along, Re-run the previous region. This will run the previous code block inculding the modifications you have made.
