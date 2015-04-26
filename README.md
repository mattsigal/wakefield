# wakefield





[![Project Status: Wip - Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](http://www.repostatus.org/badges/0.1.0/wip.svg)](http://www.repostatus.org/#wip)
[![Build Status](https://travis-ci.org/trinker/wakefield.svg?branch=master)](https://travis-ci.org/trinker/wakefield)
[![Coverage Status](https://coveralls.io/repos/trinker/wakefield/badge.svg?branch=master)](https://coveralls.io/r/trinker/wakefield?branch=master)
<a href="https://img.shields.io/badge/Version-0.1.0-orange.svg"><img src="https://img.shields.io/badge/Version-0.1.0-orange.svg" alt="Version"/></a></p>

**wakefield** is designed to quickly generate random data sets.  The user passes `n` (number of rows) and predefined vectors to the `r_data_frame` function to produce a `dplyr::tbl_df` object.

<img src="inst/wakefield_logo/r_wakefield.png" width="60%", alt="">  

## Installation

To download the development version of **wakefield**:

Download the [zip ball](https://github.com/trinker/wakefield/zipball/master) or [tar ball](https://github.com/trinker/wakefield/tarball/master), decompress and run `R CMD INSTALL` on it, or use the **pacman** package to install the development version:

```r
if (!require("pacman")) install.packages("pacman")
pacman::p_load_gh("trinker/wakefield")
```

## Help
    
- [Package PDF Help Manual](https://dl.dropboxusercontent.com/u/61803503/wakefield.pdf)   


## Contact

You are welcome to:
* submit suggestions and bug-reports at: <https://github.com/trinker/wakefield/issues>
* send a pull request on: <https://github.com/trinker/wakefield/>
* compose a friendly e-mail to: <tyler.rinker@gmail.com>

## Demonstration

The `r_data_frame` function (random data frame) takes `n` (the number of rows) and any number of variables (columns).  These columns are typically produced from a **wakefield** variable function.  Each of these variable functions has a pre-set behavior that produces a named vector of n length, allowing the user to lazily pass unnamed functions (optionally, without call parenthesis).  The column name is hidden as a `varname` attribute.  For example here we see the `race` variable function:


```r
race(n=10)
```

```
##  [1] White    White    White    White    White    White    White   
##  [8] Hispanic Hispanic Asian   
## Levels: White Hispanic Black Asian Bi-Racial Native Other Hawaiian
```

```r
attributes(race(n=10))
```

```
## $levels
## [1] "White"     "Hispanic"  "Black"     "Asian"     "Bi-Racial" "Native"   
## [7] "Other"     "Hawaiian" 
## 
## $class
## [1] "variable" "factor"  
## 
## $varname
## [1] "Race"
```

When this variable is used inside of `r_data_frame` the `varname` is used as a column name.  Additionally, the `n` argument is not set within variable functions but is set once in `r_data_frame`:


```r
r_data_frame(
    n = 500,
    race
)
```

```
## Source: local data frame [500 x 1]
## 
##     Race
## 1  White
## 2  White
## 3  White
## 4  White
## 5  White
## 6  White
## 7  White
## 8  White
## 9  Black
## 10 White
## ..   ...
```

The power of `r_data_frame` is apparent when we use many modular variable functions:


```r
r_data_frame(
    n = 500,
    id,
    race,
    age,
    sex,
    hour,
    iq,
    height,
    died
)
```

```
## Source: local data frame [500 x 8]
## 
##     ID      Race Age    Sex     Hour  IQ Height  Died
## 1  001     White  26 Female 00:00:00  99     67 FALSE
## 2  002     White  30 Female 00:00:00  98     71 FALSE
## 3  003     Black  23   Male 00:00:00  86     71 FALSE
## 4  004     White  34   Male 00:00:00 105     69  TRUE
## 5  005     White  33   Male 00:00:00 107     72  TRUE
## 6  006 Bi-Racial  30 Female 00:00:00  95     66  TRUE
## 7  007     White  23   Male 00:00:00 101     71 FALSE
## 8  008     Asian  29   Male 00:00:00 106     66 FALSE
## 9  009     White  29 Female 00:00:00  88     63 FALSE
## 10 010     White  26   Male 00:00:00 117     65 FALSE
## .. ...       ... ...    ...      ... ...    ...   ...
```


There are a plethora of **wakefield** based variable functions to chose from, spanning **R**'s various data types.

<!-- html table generated in R 3.2.0 by xtable 1.7-4 package -->
<!-- Sun Apr 26 00:28:11 2015 -->
<table >
  <tr> <td> age </td> <td> education </td> <td> level </td> <td> race </td> </tr>
  <tr> <td> animal </td> <td> employment </td> <td> likert </td> <td> sat </td> </tr>
  <tr> <td> answer </td> <td> eye </td> <td> likert_5 </td> <td> sentence </td> </tr>
  <tr> <td> area </td> <td> gpa </td> <td> likert_7 </td> <td> sex </td> </tr>
  <tr> <td> birth </td> <td> grade </td> <td> lorem_ipsum </td> <td> smokes </td> </tr>
  <tr> <td> car </td> <td> grade_letter </td> <td> lower </td> <td> speed </td> </tr>
  <tr> <td> children </td> <td> grade_level </td> <td> lower_factor </td> <td> speed_kph </td> </tr>
  <tr> <td> coin </td> <td> group </td> <td> marital </td> <td> speed_mph </td> </tr>
  <tr> <td> date_stamp </td> <td> hair </td> <td> month </td> <td> state </td> </tr>
  <tr> <td> death </td> <td> height </td> <td> name </td> <td> string </td> </tr>
  <tr> <td> dice </td> <td> height_cm </td> <td> normal </td> <td> upper </td> </tr>
  <tr> <td> died </td> <td> height_in </td> <td> normal_round </td> <td> upper_factor </td> </tr>
  <tr> <td> dna </td> <td> income </td> <td> paragraph </td> <td> valid </td> </tr>
  <tr> <td> dob </td> <td> iq </td> <td> pet </td> <td> year </td> </tr>
  <tr> <td> dummy </td> <td> language </td> <td> political </td> <td> zip_code </td> </tr>
   </table>
<p class="caption"><em>Available Variable Functions</em></p>

However, the user may also pass their own vector producing functions or vectors to `r_data_frame`.  Those with an `n` argument can be set by `r_data_table`:


```r
r_data_frame(
    n = 500,
    id,
    Scoring = rnorm,
    Smoker = valid,
    race,
    age,
    sex,
    hour,
    iq,
    height,
    died
)
```

```
## Source: local data frame [500 x 10]
## 
##     ID     Scoring Smoker  Race Age    Sex     Hour  IQ Height  Died
## 1  001  0.08009426  FALSE Black  28 Female 00:00:00 107     67  TRUE
## 2  002  1.42640983  FALSE White  27   Male 00:00:00 110     69  TRUE
## 3  003  1.40808831  FALSE White  30   Male 00:00:00  80     73  TRUE
## 4  004 -0.29469577  FALSE Black  34 Female 00:00:00  85     64  TRUE
## 5  005 -0.03411889   TRUE White  27 Female 00:00:00  94     68  TRUE
## 6  006 -0.53237077  FALSE White  34   Male 00:00:00 122     68 FALSE
## 7  007  0.50363998  FALSE White  32 Female 00:30:00  94     70 FALSE
## 8  008 -0.08671203   TRUE White  22   Male 00:30:00  94     60 FALSE
## 9  009 -0.01147565   TRUE White  35 Female 00:30:00  96     70  TRUE
## 10 010  0.04213622  FALSE White  31   Male 00:30:00 102     75  TRUE
## .. ...         ...    ...   ... ...    ...      ... ...    ...   ...
```



```r
r_data_frame(
    n = 500,
    id,
    age, age, age,
    grade, grade, grade
)
```

```
## Source: local data frame [500 x 7]
## 
##     ID Age_1 Age_2 Age_3 Grade_1 Grade_2 Grade_3
## 1  001    23    33    33    80.2    86.7    86.5
## 2  002    23    24    23    87.4    84.8    87.3
## 3  003    28    28    29    90.9    92.6    80.8
## 4  004    21    30    30    92.2    91.1    89.5
## 5  005    25    26    34    89.0    89.8    82.2
## 6  006    32    23    28    85.1    94.5    87.5
## 7  007    34    32    34    92.0    89.6    87.4
## 8  008    22    35    20    88.0    90.8    89.2
## 9  009    25    26    21    93.2    83.2    81.7
## 10 010    28    29    24    88.4    96.8    82.1
## .. ...   ...   ...   ...     ...     ...     ...
```


While, passing variable functions to `r_data_frame` without call parenthesis is handy the user may wish to set arguments.  This can be done through call parenthesis as we do with `data.frame` or `dplyr::data_frame`:


```r
r_data_frame(
    n = 500,
    id,
    Scoring = rnorm,
    Smoker = valid,
    `Reading(mins)` = rpois(lambda=20),  
    race,
    age(x = 8:14),
    sex,
    hour,
    iq,
    height(mean=50, sd = 10),
    died
)
```

```
## Source: local data frame [500 x 11]
## 
##     ID    Scoring Smoker Reading(mins)     Race Age    Sex     Hour  IQ
## 1  001 -1.3843663  FALSE            17    White  10   Male 00:00:00 129
## 2  002 -1.6933132   TRUE            27 Hispanic   8   Male 00:00:00  98
## 3  003  0.6091624  FALSE            21    White  12 Female 00:00:00 102
## 4  004  2.5396455  FALSE            23    White  11 Female 00:00:00 109
## 5  005  0.4119612  FALSE            14    White  14 Female 00:00:00  90
## 6  006 -1.8946591   TRUE            14    White  11 Female 00:00:00 110
## 7  007  0.1030845   TRUE            21    Black  10 Female 00:00:00 103
## 8  008  0.5199644  FALSE            17 Hispanic  10 Female 00:00:00 109
## 9  009 -1.4332710  FALSE            25    White   8 Female 00:00:00 105
## 10 010  0.7818851   TRUE            25    White  12   Male 00:00:00  88
## .. ...        ...    ...           ...      ... ...    ...      ... ...
## Variables not shown: Height (dbl), Died (lgl)
```

## Random Missing Observations

Often data contains missing values.  **wakefield** allows the user to add a proportion of missing values per column/vector via the `r_na` (random `NA`).  This works nicely within a **dplyr**/**magrittr** `%>%` *then* pipeline:


```r
r_data_frame(
    n = 30,
    id,
    race,
    age,
    sex,
    hour,
    iq,
    height,
    died,
    Scoring = rnorm,
    Smoker = valid
) %>%
    r_na(prob=.4)
```

```
## Source: local data frame [30 x 10]
## 
##    ID     Race Age    Sex     Hour  IQ Height  Died    Scoring Smoker
## 1  01    Black  NA   Male 01:00:00  NA     71 FALSE  1.3617039  FALSE
## 2  02    White  28     NA 01:00:00  NA     NA    NA -0.0361482     NA
## 3  03       NA  NA   Male 01:00:00  NA     77    NA  0.7327269  FALSE
## 4  04 Hispanic  20     NA 02:30:00 101     65 FALSE         NA     NA
## 5  05       NA  22     NA     <NA>  91     79    NA         NA   TRUE
## 6  06    White  NA     NA 05:00:00 104     NA FALSE  0.7531669   TRUE
## 7  07    White  29 Female 05:00:00  NA     67  TRUE  0.3215741  FALSE
## 8  08       NA  NA   Male 08:00:00 116     NA    NA         NA   TRUE
## 9  09    White  24   Male     <NA> 109     66    NA -0.9869757  FALSE
## 10 10       NA  NA   Male 09:00:00  NA     65 FALSE         NA   TRUE
## .. ..      ... ...    ...      ... ...    ...   ...        ...    ...
```

## Repeated Measures & Time Series

The `r_series` function allows the user to pass a single **wakefield** function and dictate how many columns (`j`) to produce.  


```r
set.seed(10)

r_series(likert, j = 3, n=10)
```

```
## Source: local data frame [10 x 3]
## 
##           Likert_1          Likert_2          Likert_3
## 1          Neutral          Disagree Strongly Disagree
## 2            Agree           Neutral          Disagree
## 3          Neutral   Strongly Agree           Disagree
## 4         Disagree           Neutral             Agree
## 5  Strongly Agree              Agree           Neutral
## 6            Agree           Neutral          Disagree
## 7            Agree   Strongly Agree  Strongly Disagree
## 8            Agree             Agree             Agree
## 9         Disagree             Agree          Disagree
## 10         Neutral Strongly Disagree             Agree
```

Often the user wants a numeric score for Likert type columns and similar variables.  For series with multiple factors the `as_integer` converts all columns to integer values.  Additionally, we may want to specify column name prefixes. This can be accomplished via the variable function's `name` argument.  Both of these features are demonstrated here.


```r
set.seed(10)

as_integer(r_series(likert, j = 5, n=10, name = "Item"))
```

```
## Source: local data frame [10 x 5]
## 
##    Item_1 Item_2 Item_3 Item_4 Item_5
## 1       3      2      1      3      4
## 2       4      3      2      5      4
## 3       3      5      2      5      5
## 4       2      3      4      1      2
## 5       5      4      3      3      4
## 6       4      3      2      2      5
## 7       4      5      1      1      5
## 8       4      4      4      1      3
## 9       2      4      2      2      5
## 10      3      1      4      3      1
```

`r_series` can be used within a `r_data_frame` as well.  


```r
set.seed(10)

r_data_frame(n=100,
    id,
    age,
    sex,
    r_series(likert, 3, name = "Question")
)
```

```
## Source: local data frame [100 x 6]
## 
##     ID Age    Sex        Question_1        Question_2        Question_3
## 1  001  28   Male             Agree             Agree Strongly Disagree
## 2  002  24   Male           Neutral   Strongly Agree           Disagree
## 3  003  26   Male          Disagree           Neutral          Disagree
## 4  004  31   Male Strongly Disagree           Neutral          Disagree
## 5  005  21 Female   Strongly Agree  Strongly Disagree Strongly Disagree
## 6  006  23 Female          Disagree          Disagree             Agree
## 7  007  24 Female          Disagree   Strongly Agree  Strongly Disagree
## 8  008  24   Male Strongly Disagree             Agree             Agree
## 9  009  29 Female             Agree   Strongly Agree    Strongly Agree 
## 10 010  26   Male Strongly Disagree Strongly Disagree             Agree
## .. ... ...    ...               ...               ...               ...
```



```r
set.seed(10)

r_data_frame(n=100,
    id,
    age,
    sex,
    r_series(likert, 5, name = "Item", integer = TRUE)
)
```

```
## Source: local data frame [100 x 8]
## 
##     ID Age    Sex Item_1 Item_2 Item_3 Item_4 Item_5
## 1  001  28   Male      4      4      1      1      1
## 2  002  24   Male      3      5      2      1      2
## 3  003  26   Male      2      3      2      1      2
## 4  004  31   Male      1      3      2      4      3
## 5  005  21 Female      5      1      1      5      4
## 6  006  23 Female      2      2      4      3      4
## 7  007  24 Female      2      5      1      5      2
## 8  008  24   Male      1      4      4      5      5
## 9  009  29 Female      4      5      5      4      3
## 10 010  26   Male      1      1      4      1      2
## .. ... ...    ...    ...    ...    ...    ...    ...
```

## Expanded Dummy Coding

The user may wish to expand a `factor` into `j` dummy coded columns.  The `r_dummy` function expands a factor into `j` columns and works similar to the `r_series` function.  The user may wish to use the original factor name as the prefix to the `j` columns.  Setting `prefix = TRUE` within `r_dummy` accomplishes this.



```r
set.seed(10)
r_data_frame(n=100,
    id,
    age,
    r_dummy(sex, prefix = TRUE),
    r_dummy(political)
)
```

```
## Source: local data frame [100 x 9]
## 
##     ID Age Sex_Male Sex_Female Constitution Democrat Green Libertarian
## 1  001  28        1          0            1        0     0           0
## 2  002  24        1          0            1        0     0           0
## 3  003  26        1          0            0        1     0           0
## 4  004  31        1          0            0        1     0           0
## 5  005  21        0          1            1        0     0           0
## 6  006  23        0          1            0        1     0           0
## 7  007  24        0          1            0        1     0           0
## 8  008  24        1          0            0        0     0           0
## 9  009  29        0          1            1        0     0           0
## 10 010  26        1          0            0        1     0           0
## .. ... ...      ...        ...          ...      ...   ...         ...
## Variables not shown: Republican (int)
```










