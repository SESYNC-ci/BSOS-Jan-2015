# Using R and twitter

For more information: 
* http://davetang.org/muse/2013/04/06/using-the-r_twitter-package/
* https://cran.r-project.org/web/packages/tm/vignettes/tm.pdf
* https://deltadna.com/blog/text-mining-in-r-for-term-frequency/ 
* https://cran.r-project.org/web/packages/wordcloud/wordcloud.pdf
* http://shiny.rstudio.com/gallery/word-cloud.html

This demonstration will construct a shiny interface which will generate a workcloud from twitter data. It relies on three packages, the twitteR package which wraps tweets, tm a natural language package, and wordcloud for visualization.


# Step 1 Setup keys for searching. 

Most web api's require some type of authentication. In the case of twitter, applications need to use oauth to connect. THis involves a series of keys that identify individual appliations. If you've ever granted an application such as facebook, tweetdeck or others access this is the type of exchange which occurs under the hood.

* Log into twitter. Go to your profile and settings, apps
* https://apps.twitter.com
** Name, desc, website need to be filled out, leave callback blank.
** Go to Keys and access tokens, update permissions for read-only. Generate an access token
** Keep this page open as we're going to copy these values in later.

# Step 2 - Setup and twitter connection

Install the packages you will need for this:

<pre>
install.packages("twitteR")
install.packages("wordcloud")
install.packages("tm")
</pre>

Create a new directory which will contain your webapp. In there, create a new R file and start putting in the following.

<pre>
#install the necessary packages
 
library("twitteR")
library("wordcloud")
library("tm")

#necessary file for Windows
#download.file(url="http://curl.haxx.se/ca/cacert.pem", destfile="cacert.pem")
 
#to get your consumerKey and consumerSecret see the twitteR documentation for instructions
consumer_key <- 'your key'
consumer_secret <- 'your secret'
access_token <- 'your access token'
access_secret <- 'your access secret'
</pre>

Now we setup our connection to twitter.

<pre>
options(httr_oauth_cache = TRUE)
setup_twitter_oauth(consumer_key,
                    consumer_secret,
                    access_token,
                    access_secret)
</pre>

# Step 3, perform a twitter query

<pre> 
#the cainfo parameter is necessary only on Windows, this didn't appear to need to be done at this time.
r_stats <- searchTwitter("#Rstats", n=1500) #, cainfo="cacert.pem")
</pre>

Take a look at the str, structure of this list that comes back, there's a whole lot of stuff going on in there.

You can pull in individual tweet by running

<pre>
print(r_stats[[1]]$text)
</pre>


# Step 4, clean results via TM

TM can apply filters to text that arrives from a directory, vector, or data frame. So this means we have to take our ugly list and 
clean it up by extracting the tweet part only then removing extra punctuation using tm_map.

tm_map in this pachge applies a function to all elements in the Corpus. Examples of these transformations are:
* tm_map(corpus,stripWhitespace)
* tm_map(corpus,content_transformer(tolower) - toupper, etc
* tm_map(corpus,removeWords, stopwords())
* tm_map(corpus,remotePunctuation)

<pre>
#save text
r_stats_text <- sapply(r_stats, function(x) x$getText())
r_stats_text <- iconv(r_stats_text,"latin1","ASCII",sub="")
 
#create corpus
corpus <- Corpus(VectorSource(r_stats_text))
 
#clean up
corpus <- tm_map(corpus, content_transformer(tolower)) 
corpus <- tm_map(corpus, removePunctuation)
corpus <- tm_map(corpus, function(x)removeWords(x,stopwords()))
wordcloud(corpus)
</pre>

This will take a few minutes to apply, now to make it more interesting and filter out different items we can filter based on word frequency

<pre>
dtm <- as.matrixDocumentTermMatrix(corpus) 
wordcounts <- sort(colSums(dtm),descreasing=TRUE)
popularWords <- wordCounts[wordCounts>5]
wordcloud(names(popularWords),popularWords) 
<pre>

# Step 5 - turn this into a shiny app

* Create a server.R and ui.R with the following:

*server.R*

* When creating this, hardcode the wordcloud generation and have the students sub out the sliders

<pre>
library(shiny)
#
# packages to install prior
#install the necessary packages
#install.packages("twitteR")
#install.packages("wordcloud")
#install.packages("tm")

library("twitteR")
library("wordcloud")
library(tm)

#necessary file for Windows
#download.file(url="http://curl.haxx.se/ca/cacert.pem", destfile="cacert.pem")

#to get your consumerKey and consumerSecret see the twitteR documentation for instructions
consumer_key <- ''
consumer_secret <- ''
access_token <- ''
access_secret <- ''
options(httr_oauth_cache = TRUE)
setup_twitter_oauth(consumer_key,
                    consumer_secret,
                    access_token,
                    access_secret)

#the cainfo parameter is necessary only on Windows
searchresults <- searchTwitter("#sotu", n=1500)
#searchresults<- searchTwitter("#Rstats", n=1500, cainfo="cacert.pem")


#save text
tweet_text <- sapply(searchresults, function(x) x$getText())
tweet_text <- iconv(tweet_text, "latin1","ASCII",sub="")

#create corpus
tweet_corpus <- Corpus(VectorSource(tweet_text))

#clean up
tweet_corpus <- tm_map(tweet_corpus, content_transformer(tolower)) 
tweet_corpus <- tm_map(tweet_corpus, removePunctuation)
tweet_corpus <- tm_map(tweet_corpus, function(x)removeWords(x,stopwords()))
#wordcloud(tweet_corpus)
print("done")

# Define server logic required to draw a histogram
shinyServer(function(input, output) {
  
  # Expression that generates a histogram. The expression is
  # wrapped in a call to renderPlot to indicate that:
  #
  #  1) It is "reactive" and therefore should be automatically
  #     re-executed when inputs change
  #  2) Its output type is a plot
  
  output$wordcloud <- renderPlot({
    wordcloud(tweet_corpus, 
              colors = brewer.pal(8,"Dark2"), 
              min.freq = input$frequency, 
              max.words = input$maxwords)
  })
  
})
</pre>

*ui.R*

* When demo'ing, setup teh structure, but leave out the two sliders and hve them added as an exercise

<pre>

# Define UI for application that draws a histogram
shinyUI(fluidPage(
  
  # Application title
  titlePanel("Twitter Wordcloud"),
  
  # Sidebar with a slider input for the number of bins
  sidebarLayout(
    sidebarPanel(
      sliderInput("frequency",
                  "Minimum Frequency",
                  min = 5,
                  max = 1500,
                  value = 100,
                  step = 1),
      sliderInput("maxwords",
                  "Maximum Words",
                  min = 1,
                  max = 300,
                  value = 50,
                  step = 1)
    ),
    
    # Show a plot of the generated distribution
    mainPanel(
      plotOutput("wordcloud")
    )
  )
))
</pre>

Some notes from the original blog in case there were issues loading

<pre> 
#alternative steps if you're running into problems 
r_stats<- searchTwitter("#Rstats", n=1500, cainfo="cacert.pem")
#save text
r_stats_text <- sapply(r_stats, function(x) x$getText())
#create corpus
r_stats_text_corpus <- Corpus(VectorSource(r_stats_text))
 
#if you get the below error
#In mclapply(content(x), FUN, ...) :
#  all scheduled cores encountered errors in user code
#add mc.cores=1 into each function
 
#run this step if you get the error:
#(please break it!)' in 'utf8towcs'
r_stats_text_corpus <- tm_map(r_stats_text_corpus,
                              content_transformer(function(x) iconv(x, to='UTF-8-MAC', sub='byte')),
                              mc.cores=1
                              )
r_stats_text_corpus <- tm_map(r_stats_text_corpus, content_transformer(tolower), mc.cores=1)
r_stats_text_corpus <- tm_map(r_stats_text_corpus, removePunctuation, mc.cores=1)
r_stats_text_corpus <- tm_map(r_stats_text_corpus, function(x)removeWords(x,stopwords()), mc.cores=1)
</pre>
