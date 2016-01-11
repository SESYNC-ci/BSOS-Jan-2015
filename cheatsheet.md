
# Lesson 1 

## Shortcuts
* str() - details abt data variable
* typeof() - list data type in data structure
* ?fn - getting help
*  <tab> - complete stuff
* <- assignment (x <- 3)

## Data Types

* logical (TRUE, FALSE, etc)
* integer ( 2L, as.integer)
* numeric ( real or decimal)
* complex (i + 0i, 1 + 4i)
* character ( "a", "ABC")

* as.numeric, as.logical, as.character, as.complex to convert - works on basic types and structures

## Data Structures

* head, tail, length
* str - details on structure

* Vector - one data type
** vector(), vector(length=10)
** 1:10 - sequence
** c(4,5,6), c(x,45)
** seq(10) - same as 1:10
* Factor - vectors taht contain a constrained vocabulary
* factor(c(...), levels=c())
* List - garbage bucket of anything
** list(x,'a',1)
** list(d=5,c=6)
* Matrix - like a vector, just multi-dimensional
** matrix( 1:50, ncol=5,nrow=10 )
* data.frame - like Matrix, but columns are different typesa (ie, list where columns must be same length)
** data.frame (id=c('a','b'),x=2:3)
** nrow, ncol
** rbind, cbind
** class(frame$col)
** frame$col <- c(1:3) - replace a column
** colnames()

## GGPlot

ggplot(data = data, aes(x=col,y=col2)) + geom_point|line 
