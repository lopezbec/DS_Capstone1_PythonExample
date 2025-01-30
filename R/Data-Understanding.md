Data Understanding: R Introduction
================
CL
9/7/2021

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>. You can also look at Wickham, H., & Grolemund, G. (2016). R for data science: import, tidy, transform, visualize, and model data. ” O’Reilly Media, Inc.” [Chapter 27](https://r4ds.had.co.nz/r-markdown.html) for more info about R Markdown files.

In this document we will go over some of the commands to load and read data, view information about data types, ad how to summarize it.

``` r
#We will use the mpg dataset, which you can find more info HERE https://archive.ics.uci.edu/ml/datasets/auto+mpg OR you can type in the console ?mpg

#This dataset is on the "ggplot2" library

if(!require(ggplot2)){ #This just check if the library is installed already or not
  install.packages('ggplot2',verbose=T,dependencies=TRUE)   # if not, this will install it
}
```

    ## Loading required package: ggplot2

    ## Warning: package 'ggplot2' was built under R version 4.3.3

``` r
if(!require(ggplot2)){ #This just check if the library is installed already or not
  install.packages('ggplot2',verbose=T,dependencies=TRUE)   # if not, this will install it
}

library (ggplot2)    #Load library
```

## Loading dataset from a Library

The dataset is already loaded with the package and it is named ‘mpg’

``` r
?mpg
```

    ## starting httpd help server ... done

``` r
data=mpg    #This is just to create  a new data structure call "data' that you can see in the "Environment" tabs and double click to open it.

head(data)   # The function head print out the first 10 rows of the data
```

    ## # A tibble: 6 × 11
    ##   manufacturer model displ  year   cyl trans      drv     cty   hwy fl    class 
    ##   <chr>        <chr> <dbl> <int> <int> <chr>      <chr> <int> <int> <chr> <chr> 
    ## 1 audi         a4      1.8  1999     4 auto(l5)   f        18    29 p     compa…
    ## 2 audi         a4      1.8  1999     4 manual(m5) f        21    29 p     compa…
    ## 3 audi         a4      2    2008     4 manual(m6) f        20    31 p     compa…
    ## 4 audi         a4      2    2008     4 auto(av)   f        21    30 p     compa…
    ## 5 audi         a4      2.8  1999     6 auto(l5)   f        16    26 p     compa…
    ## 6 audi         a4      2.8  1999     6 manual(m5) f        18    26 p     compa…

``` r
tail(data)   # tail print out the last 10 rows of the dataset
```

    ## # A tibble: 6 × 11
    ##   manufacturer model  displ  year   cyl trans      drv     cty   hwy fl    class
    ##   <chr>        <chr>  <dbl> <int> <int> <chr>      <chr> <int> <int> <chr> <chr>
    ## 1 volkswagen   passat   1.8  1999     4 auto(l5)   f        18    29 p     mids…
    ## 2 volkswagen   passat   2    2008     4 auto(s6)   f        19    28 p     mids…
    ## 3 volkswagen   passat   2    2008     4 manual(m6) f        21    29 p     mids…
    ## 4 volkswagen   passat   2.8  1999     6 auto(l5)   f        16    26 p     mids…
    ## 5 volkswagen   passat   2.8  1999     6 manual(m5) f        18    26 p     mids…
    ## 6 volkswagen   passat   3.6  2008     6 auto(s6)   f        17    26 p     mids…

### Data dimensions

Once you see the data, you need to check how many features (columns) it has, and how many entities (rows)

``` r
dim(data)  #Prints #rows and # columns
```

    ## [1] 234  11

``` r
ncol(data)   #print # columns
```

    ## [1] 11

``` r
nrow(data)   #print # rows
```

    ## [1] 234

### Data Structure and type

We also need to understand the data type of our features. R has their unique data object type and structure that we can explore using the functions “str”. For more info about R Data Object and Structures visit [HERE](https://mgimond.github.io/ES218/Week02a.html)

``` r
str(data)
```

    ## tibble [234 × 11] (S3: tbl_df/tbl/data.frame)
    ##  $ manufacturer: chr [1:234] "audi" "audi" "audi" "audi" ...
    ##  $ model       : chr [1:234] "a4" "a4" "a4" "a4" ...
    ##  $ displ       : num [1:234] 1.8 1.8 2 2 2.8 2.8 3.1 1.8 1.8 2 ...
    ##  $ year        : int [1:234] 1999 1999 2008 2008 1999 1999 2008 1999 1999 2008 ...
    ##  $ cyl         : int [1:234] 4 4 4 4 6 6 6 4 4 4 ...
    ##  $ trans       : chr [1:234] "auto(l5)" "manual(m5)" "manual(m6)" "auto(av)" ...
    ##  $ drv         : chr [1:234] "f" "f" "f" "f" ...
    ##  $ cty         : int [1:234] 18 21 20 21 16 18 18 18 16 20 ...
    ##  $ hwy         : int [1:234] 29 29 31 30 26 26 27 26 25 28 ...
    ##  $ fl          : chr [1:234] "p" "p" "p" "p" ...
    ##  $ class       : chr [1:234] "compact" "compact" "compact" "compact" ...

From this we can see that we have a mix of nominal data types (i.e., “chr”= characters) and numeric data types. Very important to remember is that when performing some statistical analysis, you will need to transform some datatypes in “factors” using the “as.factor” functions. However, character with number might not directly translate to factor with the right order or level. Hence, you need to always check the order of your factor.

### Data Summary

We can use the function “summary” to extract some summary statistics about our data

``` r
summary(data)
```

    ##  manufacturer          model               displ            year     
    ##  Length:234         Length:234         Min.   :1.600   Min.   :1999  
    ##  Class :character   Class :character   1st Qu.:2.400   1st Qu.:1999  
    ##  Mode  :character   Mode  :character   Median :3.300   Median :2004  
    ##                                        Mean   :3.472   Mean   :2004  
    ##                                        3rd Qu.:4.600   3rd Qu.:2008  
    ##                                        Max.   :7.000   Max.   :2008  
    ##       cyl           trans               drv                 cty       
    ##  Min.   :4.000   Length:234         Length:234         Min.   : 9.00  
    ##  1st Qu.:4.000   Class :character   Class :character   1st Qu.:14.00  
    ##  Median :6.000   Mode  :character   Mode  :character   Median :17.00  
    ##  Mean   :5.889                                         Mean   :16.86  
    ##  3rd Qu.:8.000                                         3rd Qu.:19.00  
    ##  Max.   :8.000                                         Max.   :35.00  
    ##       hwy             fl               class          
    ##  Min.   :12.00   Length:234         Length:234        
    ##  1st Qu.:18.00   Class :character   Class :character  
    ##  Median :24.00   Mode  :character   Mode  :character  
    ##  Mean   :23.44                                        
    ##  3rd Qu.:27.00                                        
    ##  Max.   :44.00

To get counts or frequency distribution of a feature that is of “character” type, we need to transform it to factor.

``` r
data$manufacturer<-as.factor(data$manufacturer)
data$model<-as.factor(data$model)
data$trans<-as.factor(data$trans)
data$drv<-as.factor(data$drv)
data$fl<-as.factor(data$fl)
data$class<-as.factor(data$class)

summary(data)
```

    ##      manufacturer                 model         displ            year     
    ##  dodge     :37    caravan 2wd        : 11   Min.   :1.600   Min.   :1999  
    ##  toyota    :34    ram 1500 pickup 4wd: 10   1st Qu.:2.400   1st Qu.:1999  
    ##  volkswagen:27    civic              :  9   Median :3.300   Median :2004  
    ##  ford      :25    dakota pickup 4wd  :  9   Mean   :3.472   Mean   :2004  
    ##  chevrolet :19    jetta              :  9   3rd Qu.:4.600   3rd Qu.:2008  
    ##  audi      :18    mustang            :  9   Max.   :7.000   Max.   :2008  
    ##  (Other)   :74    (Other)            :177                                 
    ##       cyl               trans    drv          cty             hwy       
    ##  Min.   :4.000   auto(l4)  :83   4:103   Min.   : 9.00   Min.   :12.00  
    ##  1st Qu.:4.000   manual(m5):58   f:106   1st Qu.:14.00   1st Qu.:18.00  
    ##  Median :6.000   auto(l5)  :39   r: 25   Median :17.00   Median :24.00  
    ##  Mean   :5.889   manual(m6):19           Mean   :16.86   Mean   :23.44  
    ##  3rd Qu.:8.000   auto(s6)  :16           3rd Qu.:19.00   3rd Qu.:27.00  
    ##  Max.   :8.000   auto(l6)  : 6           Max.   :35.00   Max.   :44.00  
    ##                  (Other)   :13                                          
    ##  fl             class   
    ##  c:  1   2seater   : 5  
    ##  d:  5   compact   :47  
    ##  e:  8   midsize   :41  
    ##  p: 52   minivan   :11  
    ##  r:168   pickup    :33  
    ##          subcompact:35  
    ##          suv       :62

To create a frequency table you can use the “table” function

``` r
table(data$manufacturer)
```

    ## 
    ##       audi  chevrolet      dodge       ford      honda    hyundai       jeep 
    ##         18         19         37         25          9         14          8 
    ## land rover    lincoln    mercury     nissan    pontiac     subaru     toyota 
    ##          4          3          4         13          5         14         34 
    ## volkswagen 
    ##         27

To calculate the range of a numeric data type, you can use the function “range”

``` r
range(data$displ)
```

    ## [1] 1.6 7.0

Unfortunately, base R does not provide a function for finding the mode, but you can create your own use the one from the “modeest” package

``` r
if(!require(modeest)){ 
  install.packages('modeest',verbose=T,dependencies=TRUE)   
}
```

    ## Loading required package: modeest

    ## Warning: package 'modeest' was built under R version 4.2.3

``` r
library (modeest)
mfv(data$displ)
```

    ## [1] 2

OR

``` r
head(sort(table(data$displ),decreasing =T),n=5)  # This will show the top 5 most frequent values
```

    ## 
    ##   2 2.5 4.7   4 1.8 
    ##  21  20  17  15  14

## Loading Data from your computer

This is just to download a csv from GitHub for consistency

``` r
ABS_FILE_PATH='./SUMMARY_moth.csv'   #name are different from Apple OS and Window, make sure to use the appropriate one. 

print("FILE AT:")
```

    ## [1] "FILE AT:"

``` r
print( getwd())
```

    ## [1] "C:/Users/gtcel/OneDrive/Desktop/test_Lab1/R"

``` r
download.file ("https://raw.githubusercontent.com/lopezbec/COVID19_Tweets_Dataset/main/Summary_Details/SUMMARY_moth.csv", destfile=ABS_FILE_PATH)
```

To read a csv file from your computer, just need to provide the File Path and use the functions “read.csv”

``` r
data<-read.csv(ABS_FILE_PATH)

head(data)
```

    ##   X Year Month Avg..OR  Avg..RT Avg.Tweets    X..OR    X..RT   X.Total
    ## 1 1 2020     1  5947.0  30576.5    35501.5  1958346  7852504   9810850
    ## 2 2 2020     2 10978.0  29918.0    40604.5  7624648 21944443  29568948
    ## 3 3 2020     3 13095.5  44714.5    56283.0 12610824 46659589  59270412
    ## 4 4 2020     4 30091.0  89513.0   119859.5 20594379 60311559  80905936
    ## 5 5 2020     5 35163.0 100022.5   135709.0 26307406 73792461 100099863
    ## 6 6 2020     6 51033.0 142569.0   193096.0 34786076 95171388 129957461
    ##   Total.Geo  Max.Rt MD.RT Max.Like MD.Like
    ## 1      1773  674151 166.5   334802       0
    ## 2      8103  469739  50.0   637589       0
    ## 3     19952 1064693 159.0  1255858       0
    ## 4     38220  649823  36.0   662005       0
    ## 5     47777 1007616  27.0   929811       0
    ## 6     58138  790652  38.0   882693       0
