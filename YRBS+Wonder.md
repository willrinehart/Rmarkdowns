R Notebook
================

Read in the data.

    ## ! Using an auto-discovered, cached token.

    ##   To suppress this message, modify your code or options to clearly consent to
    ##   the use of a cached token.

    ##   See gargle's "Non-interactive auth" vignette for more details:

    ##   <https://gargle.r-lib.org/articles/non-interactive-auth.html>

    ## ℹ The googlesheets4 package is using a cached token for 'will@thecgo.org'.

    ## ✔ Reading from "Teens mental health data and tech use".

    ## ✔ Range ''teen suicides''.

    ## New names:
    ## ✔ Reading from "Teens mental health data and tech use".
    ## ✔ Range ''Stack-YRBS-Wonder-R''.
    ## New names:
    ## • `` -> `...6`
    ## • `` -> `...7`

Clean the data and make some filetypes.

``` r
wonder_tot_ts <- ts(wonder$`Total suicide rate`, start = 1968, frequency = 1)
wonder_grl <- ts(wonder$`Girls suicide rate`, start = 1968, frequency = 1)
wonder_boy <- ts(wonder$`Boys suicide rate`, start = 1968, frequency = 1)
YRBS_sad_tot_ts <- ts(na.omit(stack$`Felt sad or hopeless (YRBS)`),
                      start = 1999, frequency = .5)
YRBS_sad_grl_ts <- ts(na.omit(stack$`Female felt sad or hopeless`),
                      start = 1999, frequency = .5)
YRBS_sad_boy_ts <- ts(na.omit(stack$`Male felt sad or hopeless`),
                      start = 1999, frequency = .5)
YRBS_con_tot_ts <- ts(na.omit(stack$`Seriously considered attempting suicide (YRBS)`),
                      start = 1991, frequency = .5)
YRBS_con_grl_ts <- ts(na.omit(stack$`Female seriously considered attempting suicide (YRBS)`),
                      start = 1991, frequency = .5)
YRBS_con_boy_ts <- ts(na.omit(stack$`Male seriously considered attempting suicide`),
                      start = 1991, frequency = .5)
```

Let’s plot what we have so far.

``` r
tsdisplay(wonder_tot_ts, main = "Total suicides")
```

![](YRBS+Wonder_files/figure-gfm/plot%20first-1.png)<!-- -->

``` r
tsdisplay(YRBS_sad_tot_ts, main = "Total YRBS feelings of sadness")
```

![](YRBS+Wonder_files/figure-gfm/plot%20first-2.png)<!-- -->

``` r
tsdisplay(YRBS_con_tot_ts, main = "Total YRBS contemplation of suicide")
```

![](YRBS+Wonder_files/figure-gfm/plot%20first-3.png)<!-- -->

What about the girls?

``` r
tsdisplay(wonder_grl, main = "Girls suicide")
```

![](YRBS+Wonder_files/figure-gfm/plot%20girls-1.png)<!-- -->

``` r
tsdisplay(YRBS_sad_grl_ts, main = "Girls YRBS feelings of sadness")
```

![](YRBS+Wonder_files/figure-gfm/plot%20girls-2.png)<!-- -->

``` r
tsdisplay(YRBS_con_grl_ts, main = "Girls YRBS contemplation of suicide")
```

![](YRBS+Wonder_files/figure-gfm/plot%20girls-3.png)<!-- -->

What about the boys?

``` r
tsdisplay(wonder_boy, main = "Boys suicide")
```

![](YRBS+Wonder_files/figure-gfm/plot%20boys-1.png)<!-- -->

``` r
tsdisplay(YRBS_sad_boy_ts, main = "Boys YRBS feelings of sadness")
```

![](YRBS+Wonder_files/figure-gfm/plot%20boys-2.png)<!-- -->

``` r
tsdisplay(YRBS_con_boy_ts, main = "Boys YRBS contemplation of suicide")
```

![](YRBS+Wonder_files/figure-gfm/plot%20boys-3.png)<!-- -->
