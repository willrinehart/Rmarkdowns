Analysis of YRBS and Wonder data
================

Read in the data.

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
