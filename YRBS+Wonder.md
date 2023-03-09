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
tsdisplay(YRBS_sad_tot_ts, main = "Total YRBS feelings of sadness", lag.max=10)
```

![](YRBS+Wonder_files/figure-gfm/plot%20first-2.png)<!-- -->

``` r
tsdisplay(YRBS_con_tot_ts, main = "Total YRBS contemplation of suicide", lag.max=10)
```

![](YRBS+Wonder_files/figure-gfm/plot%20first-3.png)<!-- -->

What about the girls?

``` r
tsdisplay(wonder_grl, main = "Girls suicide")
```

![](YRBS+Wonder_files/figure-gfm/plot%20girls-1.png)<!-- -->

``` r
tsdisplay(YRBS_sad_grl_ts, main = "Girls YRBS feelings of sadness", lag.max=10)
```

![](YRBS+Wonder_files/figure-gfm/plot%20girls-2.png)<!-- -->

``` r
tsdisplay(YRBS_con_grl_ts, main = "Girls YRBS contemplation of suicide", lag.max=10)
```

![](YRBS+Wonder_files/figure-gfm/plot%20girls-3.png)<!-- -->

What about the boys?

``` r
tsdisplay(wonder_boy, main = "Boys suicide")
```

![](YRBS+Wonder_files/figure-gfm/plot%20boys-1.png)<!-- -->

``` r
tsdisplay(YRBS_sad_boy_ts, main = "Boys YRBS feelings of sadness", lag.max=10)
```

![](YRBS+Wonder_files/figure-gfm/plot%20boys-2.png)<!-- -->

``` r
tsdisplay(YRBS_con_boy_ts, main = "Boys YRBS contemplation of suicide", lag.max=10)
```

![](YRBS+Wonder_files/figure-gfm/plot%20boys-3.png)<!-- -->

``` r
adfResults <- adf.test(YRBS_sad_boy_ts) 
```

    ## Warning in adf.test(YRBS_sad_boy_ts): p-value greater than printed p-value

``` r
adfResults
```

    ## 
    ##  Augmented Dickey-Fuller Test
    ## 
    ## data:  YRBS_sad_boy_ts
    ## Dickey-Fuller = 0.57873, Lag order = 2, p-value = 0.99
    ## alternative hypothesis: stationary

``` r
kpssResults <- kpss.test(YRBS_sad_boy_ts)
```

    ## Warning in kpss.test(YRBS_sad_boy_ts): p-value greater than printed p-value

``` r
kpssResults
```

    ## 
    ##  KPSS Test for Level Stationarity
    ## 
    ## data:  YRBS_sad_boy_ts
    ## KPSS Level = 0.31417, Truncation lag parameter = 2, p-value = 0.1

``` r
out1 <- beast(wonder_boy, season='none')
```

    ## FALSETRUEFALSEFALSE
    ## INFO: To supress printing the parameers in beast123(),   set extra$printOptions = 0  
    ## INFO: To supress printing the parameers in beast(),      set print.options = 0 
    ## INFO: To supress printing the parameers in beast.irreg(),set print.options = 0 
    ## INFO: To supress warning messages in beast123(),         set extra$quiet = 1  
    ## INFO: To supress warning messages in beast(),            set quiet = 1 
    ## INFO: To supress warning messages in beast.irreg(),      set quiet = 1 
    ## 
    ## #--------------------------------------------------#
    ## #       Brief summary of Input Data                #
    ## #--------------------------------------------------#
    ## Data Dimension: One signal of length 54
    ## IsOrdered     : Yes, ordered in time
    ## IsRegular     : Yes, evenly spaced at interval of  1 (unknown unit)
    ## hasSeasonCmpnt: FALSE | no periodic or seasonal component. The model Y=Trend+Error is fitted.
    ## hasOutlierCmpt: FALSE | If true, Y=Trend+Outlier+Error (experimental) is fitted instead of Y=Trend+Error 
    ## Detrend       : FALSE | If true, remove a global trend component before running BEAST & add it back after BEAST
    ## missingValue  : NaN  flagged as missing values 
    ## MissingRate   : if more than 75% of data is missing, BEAST will skip it.
    ## 
    ## 
    ## #--------------------------------------------------#
    ## #      OPTIONS used in the MCMC inference          #
    ## #--------------------------------------------------#
    ## 
    ## #......Start of displaying 'MetaData' ......
    ## metadata                = list()     # metadata used to interpret the input data
    ## metadata$season         = 'none'     # trend-only data with no periodic variation
    ## metadata$startTime      = 1968       # unknown unit
    ## metadata$deltaTime      = 1          # unknown unit
    ## metadata$MissingRate    = 0.75       # if more than 75% of data is missing, BEAST will skip it.
    ## metadata$detrend        = FALSE      # If true,remove a global trend  cmpnt before running BEAST & add it back later
    ## #........End of displaying MetaData ........
    ## 
    ## #......Start of displaying 'prior' ......
    ## prior                  = list()     # prior is the key model parameters of BEAST
    ## prior$trendMinOrder    = 0          # torder.minmax[1]: min trend polynomial order alllowed
    ## prior$trendMaxOrder    = 1          # torder.minmax[2]: max trend polynomial order alllowed
    ## prior$trendMinKnotNum  = 0          # tcp.minmax[1]   : min num of chngpts in trend
    ## prior$trendMaxKnotNum  = 10         # tcp.minmax[2]   : min num of chngpts in trend
    ## prior$trendMinSepDist  = 3          # tseg.min        : min trend segment length in terms of datapoints
    ## prior$K_MAX            = 22         # max number of terms in general linear model (useful only at small values)
    ## prior$precValue        = 1.5        # useful mainly when precPriorType='constant'
    ## prior$modelPriorType   = 1         
    ## prior$precPriorType    = 'uniform'
    ## #......End of displaying pripr ......
    ## 
    ## #......Start of displaying 'mcmc' ......
    ## mcmc                           = list()     # mcmc used to specify the inference algorithm
    ## mcmc$seed                      = 0
    ## mcmc$samples                   = 8000
    ## mcmc$thinningFactor            = 5
    ## mcmc$burnin                    = 200
    ## mcmc$chainNumber               = 3
    ## mcmc$maxMoveStepSize           = 4
    ## mcmc$trendResamplingOrderProb  = 0.1
    ## mcmc$credIntervalAlphaLevel    = 0.95
    ## #......End of displaying mcmc ......
    ## 
    ## #......Start of displaying 'extra' ......
    ## extra                      = list()     # extra used to configure output/computing options
    ## extra$dumpInputData        = TRUE
    ## extra$whichOutputDimIsTime = 1
    ## extra$computeCredible      = FALSE
    ## extra$fastCIComputation    = TRUE
    ## extra$computeTrendOrder    = TRUE
    ## extra$computeTrendChngpt   = TRUE
    ## extra$computeTrendSlope    = TRUE
    ## extra$tallyPosNegTrendJump = TRUE
    ## extra$tallyIncDecTrendJump = TRUE
    ## extra$printProgressBar     = TRUE
    ## extra$printOptions         = TRUE
    ## extra$consoleWidth         = 80
    ## extra$numThreadsPerCPU     = 2
    ## extra$numParThreads        = 0
    ## #......End of displaying extra ......
    ## 
    ## -Progress:  0.0% done[>********************************************************]\Progress:  4.2% done[==>******************************************************]|Progress:  8.3% done[=====>***************************************************]/Progress: 12.5% done[=======>*************************************************]-Progress: 16.7% done[==========>**********************************************]\Progress: 20.8% done[============>********************************************]|Progress: 25.0% done[==============>******************************************]/Progress: 29.2% done[=================>***************************************]-Progress: 33.3% done[===================>*************************************]\Progress: 37.5% done[=====================>***********************************]|Progress: 41.7% done[========================>********************************]/Progress: 45.8% done[==========================>******************************]-Progress: 50.0% done[=============================>***************************]\Progress: 54.2% done[===============================>*************************]|Progress: 58.3% done[=================================>***********************]/Progress: 62.5% done[====================================>********************]-Progress: 66.7% done[======================================>******************]\Progress: 70.8% done[========================================>****************]|Progress: 75.0% done[===========================================>*************]/Progress: 79.2% done[=============================================>***********]-Progress: 83.3% done[================================================>********]\Progress: 87.5% done[==================================================>******]|Progress: 91.7% done[====================================================>****]/Progress: 95.8% done[=======================================================>*]-Progress:100.0% done[=========================================================]

``` r
out2 <- beast(YRBS_sad_boy_ts, season='none')
```

    ## FALSETRUEFALSEFALSE
    ## INFO: To supress printing the parameers in beast123(),   set extra$printOptions = 0  
    ## INFO: To supress printing the parameers in beast(),      set print.options = 0 
    ## INFO: To supress printing the parameers in beast.irreg(),set print.options = 0 
    ## INFO: To supress warning messages in beast123(),         set extra$quiet = 1  
    ## INFO: To supress warning messages in beast(),            set quiet = 1 
    ## INFO: To supress warning messages in beast.irreg(),      set quiet = 1 
    ## 
    ## #--------------------------------------------------#
    ## #       Brief summary of Input Data                #
    ## #--------------------------------------------------#
    ## Data Dimension: One signal of length 12
    ## IsOrdered     : Yes, ordered in time
    ## IsRegular     : Yes, evenly spaced at interval of  2 (unknown unit)
    ## hasSeasonCmpnt: FALSE | no periodic or seasonal component. The model Y=Trend+Error is fitted.
    ## hasOutlierCmpt: FALSE | If true, Y=Trend+Outlier+Error (experimental) is fitted instead of Y=Trend+Error 
    ## Detrend       : FALSE | If true, remove a global trend component before running BEAST & add it back after BEAST
    ## missingValue  : NaN  flagged as missing values 
    ## MissingRate   : if more than 75% of data is missing, BEAST will skip it.
    ## 
    ## 
    ## #--------------------------------------------------#
    ## #      OPTIONS used in the MCMC inference          #
    ## #--------------------------------------------------#
    ## 
    ## #......Start of displaying 'MetaData' ......
    ## metadata                = list()     # metadata used to interpret the input data
    ## metadata$season         = 'none'     # trend-only data with no periodic variation
    ## metadata$startTime      = 1999       # unknown unit
    ## metadata$deltaTime      = 2          # unknown unit
    ## metadata$MissingRate    = 0.75       # if more than 75% of data is missing, BEAST will skip it.
    ## metadata$detrend        = FALSE      # If true,remove a global trend  cmpnt before running BEAST & add it back later
    ## #........End of displaying MetaData ........
    ## 
    ## #......Start of displaying 'prior' ......
    ## prior                  = list()     # prior is the key model parameters of BEAST
    ## prior$trendMinOrder    = 0          # torder.minmax[1]: min trend polynomial order alllowed
    ## prior$trendMaxOrder    = 1          # torder.minmax[2]: max trend polynomial order alllowed
    ## prior$trendMinKnotNum  = 0          # tcp.minmax[1]   : min num of chngpts in trend
    ## prior$trendMaxKnotNum  = 2          # tcp.minmax[2]   : min num of chngpts in trend
    ## prior$trendMinSepDist  = 3          # tseg.min        : min trend segment length in terms of datapoints
    ## prior$K_MAX            = 6          # max number of terms in general linear model (useful only at small values)
    ## prior$precValue        = 1.5        # useful mainly when precPriorType='constant'
    ## prior$modelPriorType   = 1         
    ## prior$precPriorType    = 'uniform'
    ## #......End of displaying pripr ......
    ## 
    ## #......Start of displaying 'mcmc' ......
    ## mcmc                           = list()     # mcmc used to specify the inference algorithm
    ## mcmc$seed                      = 0
    ## mcmc$samples                   = 8000
    ## mcmc$thinningFactor            = 5
    ## mcmc$burnin                    = 200
    ## mcmc$chainNumber               = 3
    ## mcmc$maxMoveStepSize           = 4
    ## mcmc$trendResamplingOrderProb  = 0.1
    ## mcmc$credIntervalAlphaLevel    = 0.95
    ## #......End of displaying mcmc ......
    ## 
    ## #......Start of displaying 'extra' ......
    ## extra                      = list()     # extra used to configure output/computing options
    ## extra$dumpInputData        = TRUE
    ## extra$whichOutputDimIsTime = 1
    ## extra$computeCredible      = FALSE
    ## extra$fastCIComputation    = TRUE
    ## extra$computeTrendOrder    = TRUE
    ## extra$computeTrendChngpt   = TRUE
    ## extra$computeTrendSlope    = TRUE
    ## extra$tallyPosNegTrendJump = TRUE
    ## extra$tallyIncDecTrendJump = TRUE
    ## extra$printProgressBar     = TRUE
    ## extra$printOptions         = TRUE
    ## extra$consoleWidth         = 80
    ## extra$numThreadsPerCPU     = 2
    ## extra$numParThreads        = 0
    ## #......End of displaying extra ......
    ## 
    ## \Progress:  0.0% done[>********************************************************]|Progress:  4.2% done[==>******************************************************]/Progress:  8.3% done[=====>***************************************************]-Progress: 12.5% done[=======>*************************************************]\Progress: 16.7% done[==========>**********************************************]|Progress: 20.8% done[============>********************************************]/Progress: 25.0% done[==============>******************************************]-Progress: 29.2% done[=================>***************************************]\Progress: 33.3% done[===================>*************************************]|Progress: 37.5% done[=====================>***********************************]/Progress: 41.7% done[========================>********************************]-Progress: 45.8% done[==========================>******************************]\Progress: 50.0% done[=============================>***************************]|Progress: 54.2% done[===============================>*************************]/Progress: 58.3% done[=================================>***********************]-Progress: 62.5% done[====================================>********************]\Progress: 66.7% done[======================================>******************]|Progress: 70.8% done[========================================>****************]/Progress: 75.0% done[===========================================>*************]-Progress: 79.2% done[=============================================>***********]\Progress: 83.3% done[================================================>********]|Progress: 87.5% done[==================================================>******]/Progress: 91.7% done[====================================================>****]-Progress: 95.8% done[=======================================================>*]\Progress:100.0% done[=========================================================]

``` r
out3 <- beast(YRBS_con_boy_ts, season='none')
```

    ## FALSETRUEFALSEFALSE
    ## INFO: To supress printing the parameers in beast123(),   set extra$printOptions = 0  
    ## INFO: To supress printing the parameers in beast(),      set print.options = 0 
    ## INFO: To supress printing the parameers in beast.irreg(),set print.options = 0 
    ## INFO: To supress warning messages in beast123(),         set extra$quiet = 1  
    ## INFO: To supress warning messages in beast(),            set quiet = 1 
    ## INFO: To supress warning messages in beast.irreg(),      set quiet = 1 
    ## 
    ## #--------------------------------------------------#
    ## #       Brief summary of Input Data                #
    ## #--------------------------------------------------#
    ## Data Dimension: One signal of length 16
    ## IsOrdered     : Yes, ordered in time
    ## IsRegular     : Yes, evenly spaced at interval of  2 (unknown unit)
    ## hasSeasonCmpnt: FALSE | no periodic or seasonal component. The model Y=Trend+Error is fitted.
    ## hasOutlierCmpt: FALSE | If true, Y=Trend+Outlier+Error (experimental) is fitted instead of Y=Trend+Error 
    ## Detrend       : FALSE | If true, remove a global trend component before running BEAST & add it back after BEAST
    ## missingValue  : NaN  flagged as missing values 
    ## MissingRate   : if more than 75% of data is missing, BEAST will skip it.
    ## 
    ## 
    ## #--------------------------------------------------#
    ## #      OPTIONS used in the MCMC inference          #
    ## #--------------------------------------------------#
    ## 
    ## #......Start of displaying 'MetaData' ......
    ## metadata                = list()     # metadata used to interpret the input data
    ## metadata$season         = 'none'     # trend-only data with no periodic variation
    ## metadata$startTime      = 1991       # unknown unit
    ## metadata$deltaTime      = 2          # unknown unit
    ## metadata$MissingRate    = 0.75       # if more than 75% of data is missing, BEAST will skip it.
    ## metadata$detrend        = FALSE      # If true,remove a global trend  cmpnt before running BEAST & add it back later
    ## #........End of displaying MetaData ........
    ## 
    ## #......Start of displaying 'prior' ......
    ## prior                  = list()     # prior is the key model parameters of BEAST
    ## prior$trendMinOrder    = 0          # torder.minmax[1]: min trend polynomial order alllowed
    ## prior$trendMaxOrder    = 1          # torder.minmax[2]: max trend polynomial order alllowed
    ## prior$trendMinKnotNum  = 0          # tcp.minmax[1]   : min num of chngpts in trend
    ## prior$trendMaxKnotNum  = 3          # tcp.minmax[2]   : min num of chngpts in trend
    ## prior$trendMinSepDist  = 3          # tseg.min        : min trend segment length in terms of datapoints
    ## prior$K_MAX            = 8          # max number of terms in general linear model (useful only at small values)
    ## prior$precValue        = 1.5        # useful mainly when precPriorType='constant'
    ## prior$modelPriorType   = 1         
    ## prior$precPriorType    = 'uniform'
    ## #......End of displaying pripr ......
    ## 
    ## #......Start of displaying 'mcmc' ......
    ## mcmc                           = list()     # mcmc used to specify the inference algorithm
    ## mcmc$seed                      = 0
    ## mcmc$samples                   = 8000
    ## mcmc$thinningFactor            = 5
    ## mcmc$burnin                    = 200
    ## mcmc$chainNumber               = 3
    ## mcmc$maxMoveStepSize           = 4
    ## mcmc$trendResamplingOrderProb  = 0.1
    ## mcmc$credIntervalAlphaLevel    = 0.95
    ## #......End of displaying mcmc ......
    ## 
    ## #......Start of displaying 'extra' ......
    ## extra                      = list()     # extra used to configure output/computing options
    ## extra$dumpInputData        = TRUE
    ## extra$whichOutputDimIsTime = 1
    ## extra$computeCredible      = FALSE
    ## extra$fastCIComputation    = TRUE
    ## extra$computeTrendOrder    = TRUE
    ## extra$computeTrendChngpt   = TRUE
    ## extra$computeTrendSlope    = TRUE
    ## extra$tallyPosNegTrendJump = TRUE
    ## extra$tallyIncDecTrendJump = TRUE
    ## extra$printProgressBar     = TRUE
    ## extra$printOptions         = TRUE
    ## extra$consoleWidth         = 80
    ## extra$numThreadsPerCPU     = 2
    ## extra$numParThreads        = 0
    ## #......End of displaying extra ......
    ## 
    ## |Progress:  0.0% done[>********************************************************]/Progress:  4.2% done[==>******************************************************]-Progress:  8.3% done[=====>***************************************************]\Progress: 12.5% done[=======>*************************************************]|Progress: 16.7% done[==========>**********************************************]/Progress: 20.8% done[============>********************************************]-Progress: 25.0% done[==============>******************************************]\Progress: 29.2% done[=================>***************************************]|Progress: 33.3% done[===================>*************************************]/Progress: 37.5% done[=====================>***********************************]-Progress: 41.7% done[========================>********************************]\Progress: 45.8% done[==========================>******************************]|Progress: 50.0% done[=============================>***************************]/Progress: 54.2% done[===============================>*************************]-Progress: 58.3% done[=================================>***********************]\Progress: 62.5% done[====================================>********************]|Progress: 66.7% done[======================================>******************]/Progress: 70.8% done[========================================>****************]-Progress: 75.0% done[===========================================>*************]\Progress: 79.2% done[=============================================>***********]|Progress: 83.3% done[================================================>********]/Progress: 87.5% done[==================================================>******]-Progress: 91.7% done[====================================================>****]\Progress: 95.8% done[=======================================================>*]|Progress:100.0% done[=========================================================]

``` r
plot(out1, main = "Boys suicide")
```

![](YRBS+Wonder_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
plot(out2, main = "Boys YRBS feelings of sadness")
```

![](YRBS+Wonder_files/figure-gfm/unnamed-chunk-3-2.png)<!-- -->

``` r
plot(out3, main = "Boys YRBS contemplation of suicide")
```

![](YRBS+Wonder_files/figure-gfm/unnamed-chunk-3-3.png)<!-- -->

``` r
out1 <- beast(wonder_grl, season='none')
```

    ## FALSETRUEFALSEFALSE
    ## INFO: To supress printing the parameers in beast123(),   set extra$printOptions = 0  
    ## INFO: To supress printing the parameers in beast(),      set print.options = 0 
    ## INFO: To supress printing the parameers in beast.irreg(),set print.options = 0 
    ## INFO: To supress warning messages in beast123(),         set extra$quiet = 1  
    ## INFO: To supress warning messages in beast(),            set quiet = 1 
    ## INFO: To supress warning messages in beast.irreg(),      set quiet = 1 
    ## 
    ## #--------------------------------------------------#
    ## #       Brief summary of Input Data                #
    ## #--------------------------------------------------#
    ## Data Dimension: One signal of length 54
    ## IsOrdered     : Yes, ordered in time
    ## IsRegular     : Yes, evenly spaced at interval of  1 (unknown unit)
    ## hasSeasonCmpnt: FALSE | no periodic or seasonal component. The model Y=Trend+Error is fitted.
    ## hasOutlierCmpt: FALSE | If true, Y=Trend+Outlier+Error (experimental) is fitted instead of Y=Trend+Error 
    ## Detrend       : FALSE | If true, remove a global trend component before running BEAST & add it back after BEAST
    ## missingValue  : NaN  flagged as missing values 
    ## MissingRate   : if more than 75% of data is missing, BEAST will skip it.
    ## 
    ## 
    ## #--------------------------------------------------#
    ## #      OPTIONS used in the MCMC inference          #
    ## #--------------------------------------------------#
    ## 
    ## #......Start of displaying 'MetaData' ......
    ## metadata                = list()     # metadata used to interpret the input data
    ## metadata$season         = 'none'     # trend-only data with no periodic variation
    ## metadata$startTime      = 1968       # unknown unit
    ## metadata$deltaTime      = 1          # unknown unit
    ## metadata$MissingRate    = 0.75       # if more than 75% of data is missing, BEAST will skip it.
    ## metadata$detrend        = FALSE      # If true,remove a global trend  cmpnt before running BEAST & add it back later
    ## #........End of displaying MetaData ........
    ## 
    ## #......Start of displaying 'prior' ......
    ## prior                  = list()     # prior is the key model parameters of BEAST
    ## prior$trendMinOrder    = 0          # torder.minmax[1]: min trend polynomial order alllowed
    ## prior$trendMaxOrder    = 1          # torder.minmax[2]: max trend polynomial order alllowed
    ## prior$trendMinKnotNum  = 0          # tcp.minmax[1]   : min num of chngpts in trend
    ## prior$trendMaxKnotNum  = 10         # tcp.minmax[2]   : min num of chngpts in trend
    ## prior$trendMinSepDist  = 3          # tseg.min        : min trend segment length in terms of datapoints
    ## prior$K_MAX            = 22         # max number of terms in general linear model (useful only at small values)
    ## prior$precValue        = 1.5        # useful mainly when precPriorType='constant'
    ## prior$modelPriorType   = 1         
    ## prior$precPriorType    = 'uniform'
    ## #......End of displaying pripr ......
    ## 
    ## #......Start of displaying 'mcmc' ......
    ## mcmc                           = list()     # mcmc used to specify the inference algorithm
    ## mcmc$seed                      = 0
    ## mcmc$samples                   = 8000
    ## mcmc$thinningFactor            = 5
    ## mcmc$burnin                    = 200
    ## mcmc$chainNumber               = 3
    ## mcmc$maxMoveStepSize           = 4
    ## mcmc$trendResamplingOrderProb  = 0.1
    ## mcmc$credIntervalAlphaLevel    = 0.95
    ## #......End of displaying mcmc ......
    ## 
    ## #......Start of displaying 'extra' ......
    ## extra                      = list()     # extra used to configure output/computing options
    ## extra$dumpInputData        = TRUE
    ## extra$whichOutputDimIsTime = 1
    ## extra$computeCredible      = FALSE
    ## extra$fastCIComputation    = TRUE
    ## extra$computeTrendOrder    = TRUE
    ## extra$computeTrendChngpt   = TRUE
    ## extra$computeTrendSlope    = TRUE
    ## extra$tallyPosNegTrendJump = TRUE
    ## extra$tallyIncDecTrendJump = TRUE
    ## extra$printProgressBar     = TRUE
    ## extra$printOptions         = TRUE
    ## extra$consoleWidth         = 80
    ## extra$numThreadsPerCPU     = 2
    ## extra$numParThreads        = 0
    ## #......End of displaying extra ......
    ## 
    ## /Progress:  0.0% done[>********************************************************]-Progress:  4.2% done[==>******************************************************]\Progress:  8.3% done[=====>***************************************************]|Progress: 12.5% done[=======>*************************************************]/Progress: 16.7% done[==========>**********************************************]-Progress: 20.8% done[============>********************************************]\Progress: 25.0% done[==============>******************************************]|Progress: 29.2% done[=================>***************************************]/Progress: 33.3% done[===================>*************************************]-Progress: 37.5% done[=====================>***********************************]\Progress: 41.7% done[========================>********************************]|Progress: 45.8% done[==========================>******************************]/Progress: 50.0% done[=============================>***************************]-Progress: 54.2% done[===============================>*************************]\Progress: 58.3% done[=================================>***********************]|Progress: 62.5% done[====================================>********************]/Progress: 66.7% done[======================================>******************]-Progress: 70.8% done[========================================>****************]\Progress: 75.0% done[===========================================>*************]|Progress: 79.2% done[=============================================>***********]/Progress: 83.3% done[================================================>********]-Progress: 87.5% done[==================================================>******]\Progress: 91.7% done[====================================================>****]|Progress: 95.8% done[=======================================================>*]/Progress:100.0% done[=========================================================]

``` r
out2 <- beast(YRBS_sad_grl_ts, season='none')
```

    ## FALSETRUEFALSEFALSE
    ## INFO: To supress printing the parameers in beast123(),   set extra$printOptions = 0  
    ## INFO: To supress printing the parameers in beast(),      set print.options = 0 
    ## INFO: To supress printing the parameers in beast.irreg(),set print.options = 0 
    ## INFO: To supress warning messages in beast123(),         set extra$quiet = 1  
    ## INFO: To supress warning messages in beast(),            set quiet = 1 
    ## INFO: To supress warning messages in beast.irreg(),      set quiet = 1 
    ## 
    ## #--------------------------------------------------#
    ## #       Brief summary of Input Data                #
    ## #--------------------------------------------------#
    ## Data Dimension: One signal of length 12
    ## IsOrdered     : Yes, ordered in time
    ## IsRegular     : Yes, evenly spaced at interval of  2 (unknown unit)
    ## hasSeasonCmpnt: FALSE | no periodic or seasonal component. The model Y=Trend+Error is fitted.
    ## hasOutlierCmpt: FALSE | If true, Y=Trend+Outlier+Error (experimental) is fitted instead of Y=Trend+Error 
    ## Detrend       : FALSE | If true, remove a global trend component before running BEAST & add it back after BEAST
    ## missingValue  : NaN  flagged as missing values 
    ## MissingRate   : if more than 75% of data is missing, BEAST will skip it.
    ## 
    ## 
    ## #--------------------------------------------------#
    ## #      OPTIONS used in the MCMC inference          #
    ## #--------------------------------------------------#
    ## 
    ## #......Start of displaying 'MetaData' ......
    ## metadata                = list()     # metadata used to interpret the input data
    ## metadata$season         = 'none'     # trend-only data with no periodic variation
    ## metadata$startTime      = 1999       # unknown unit
    ## metadata$deltaTime      = 2          # unknown unit
    ## metadata$MissingRate    = 0.75       # if more than 75% of data is missing, BEAST will skip it.
    ## metadata$detrend        = FALSE      # If true,remove a global trend  cmpnt before running BEAST & add it back later
    ## #........End of displaying MetaData ........
    ## 
    ## #......Start of displaying 'prior' ......
    ## prior                  = list()     # prior is the key model parameters of BEAST
    ## prior$trendMinOrder    = 0          # torder.minmax[1]: min trend polynomial order alllowed
    ## prior$trendMaxOrder    = 1          # torder.minmax[2]: max trend polynomial order alllowed
    ## prior$trendMinKnotNum  = 0          # tcp.minmax[1]   : min num of chngpts in trend
    ## prior$trendMaxKnotNum  = 2          # tcp.minmax[2]   : min num of chngpts in trend
    ## prior$trendMinSepDist  = 3          # tseg.min        : min trend segment length in terms of datapoints
    ## prior$K_MAX            = 6          # max number of terms in general linear model (useful only at small values)
    ## prior$precValue        = 1.5        # useful mainly when precPriorType='constant'
    ## prior$modelPriorType   = 1         
    ## prior$precPriorType    = 'uniform'
    ## #......End of displaying pripr ......
    ## 
    ## #......Start of displaying 'mcmc' ......
    ## mcmc                           = list()     # mcmc used to specify the inference algorithm
    ## mcmc$seed                      = 0
    ## mcmc$samples                   = 8000
    ## mcmc$thinningFactor            = 5
    ## mcmc$burnin                    = 200
    ## mcmc$chainNumber               = 3
    ## mcmc$maxMoveStepSize           = 4
    ## mcmc$trendResamplingOrderProb  = 0.1
    ## mcmc$credIntervalAlphaLevel    = 0.95
    ## #......End of displaying mcmc ......
    ## 
    ## #......Start of displaying 'extra' ......
    ## extra                      = list()     # extra used to configure output/computing options
    ## extra$dumpInputData        = TRUE
    ## extra$whichOutputDimIsTime = 1
    ## extra$computeCredible      = FALSE
    ## extra$fastCIComputation    = TRUE
    ## extra$computeTrendOrder    = TRUE
    ## extra$computeTrendChngpt   = TRUE
    ## extra$computeTrendSlope    = TRUE
    ## extra$tallyPosNegTrendJump = TRUE
    ## extra$tallyIncDecTrendJump = TRUE
    ## extra$printProgressBar     = TRUE
    ## extra$printOptions         = TRUE
    ## extra$consoleWidth         = 80
    ## extra$numThreadsPerCPU     = 2
    ## extra$numParThreads        = 0
    ## #......End of displaying extra ......
    ## 
    ## -Progress:  0.0% done[>********************************************************]\Progress:  4.2% done[==>******************************************************]|Progress:  8.3% done[=====>***************************************************]/Progress: 12.5% done[=======>*************************************************]-Progress: 16.7% done[==========>**********************************************]\Progress: 20.8% done[============>********************************************]|Progress: 25.0% done[==============>******************************************]/Progress: 29.2% done[=================>***************************************]-Progress: 33.3% done[===================>*************************************]\Progress: 37.5% done[=====================>***********************************]|Progress: 41.7% done[========================>********************************]/Progress: 45.8% done[==========================>******************************]-Progress: 50.0% done[=============================>***************************]\Progress: 54.2% done[===============================>*************************]|Progress: 58.3% done[=================================>***********************]/Progress: 62.5% done[====================================>********************]-Progress: 66.7% done[======================================>******************]\Progress: 70.8% done[========================================>****************]|Progress: 75.0% done[===========================================>*************]/Progress: 79.2% done[=============================================>***********]-Progress: 83.3% done[================================================>********]\Progress: 87.5% done[==================================================>******]|Progress: 91.7% done[====================================================>****]/Progress: 95.8% done[=======================================================>*]-Progress:100.0% done[=========================================================]

``` r
out3 <- beast(YRBS_con_grl_ts, season='none')
```

    ## FALSETRUEFALSEFALSE
    ## INFO: To supress printing the parameers in beast123(),   set extra$printOptions = 0  
    ## INFO: To supress printing the parameers in beast(),      set print.options = 0 
    ## INFO: To supress printing the parameers in beast.irreg(),set print.options = 0 
    ## INFO: To supress warning messages in beast123(),         set extra$quiet = 1  
    ## INFO: To supress warning messages in beast(),            set quiet = 1 
    ## INFO: To supress warning messages in beast.irreg(),      set quiet = 1 
    ## 
    ## #--------------------------------------------------#
    ## #       Brief summary of Input Data                #
    ## #--------------------------------------------------#
    ## Data Dimension: One signal of length 16
    ## IsOrdered     : Yes, ordered in time
    ## IsRegular     : Yes, evenly spaced at interval of  2 (unknown unit)
    ## hasSeasonCmpnt: FALSE | no periodic or seasonal component. The model Y=Trend+Error is fitted.
    ## hasOutlierCmpt: FALSE | If true, Y=Trend+Outlier+Error (experimental) is fitted instead of Y=Trend+Error 
    ## Detrend       : FALSE | If true, remove a global trend component before running BEAST & add it back after BEAST
    ## missingValue  : NaN  flagged as missing values 
    ## MissingRate   : if more than 75% of data is missing, BEAST will skip it.
    ## 
    ## 
    ## #--------------------------------------------------#
    ## #      OPTIONS used in the MCMC inference          #
    ## #--------------------------------------------------#
    ## 
    ## #......Start of displaying 'MetaData' ......
    ## metadata                = list()     # metadata used to interpret the input data
    ## metadata$season         = 'none'     # trend-only data with no periodic variation
    ## metadata$startTime      = 1991       # unknown unit
    ## metadata$deltaTime      = 2          # unknown unit
    ## metadata$MissingRate    = 0.75       # if more than 75% of data is missing, BEAST will skip it.
    ## metadata$detrend        = FALSE      # If true,remove a global trend  cmpnt before running BEAST & add it back later
    ## #........End of displaying MetaData ........
    ## 
    ## #......Start of displaying 'prior' ......
    ## prior                  = list()     # prior is the key model parameters of BEAST
    ## prior$trendMinOrder    = 0          # torder.minmax[1]: min trend polynomial order alllowed
    ## prior$trendMaxOrder    = 1          # torder.minmax[2]: max trend polynomial order alllowed
    ## prior$trendMinKnotNum  = 0          # tcp.minmax[1]   : min num of chngpts in trend
    ## prior$trendMaxKnotNum  = 3          # tcp.minmax[2]   : min num of chngpts in trend
    ## prior$trendMinSepDist  = 3          # tseg.min        : min trend segment length in terms of datapoints
    ## prior$K_MAX            = 8          # max number of terms in general linear model (useful only at small values)
    ## prior$precValue        = 1.5        # useful mainly when precPriorType='constant'
    ## prior$modelPriorType   = 1         
    ## prior$precPriorType    = 'uniform'
    ## #......End of displaying pripr ......
    ## 
    ## #......Start of displaying 'mcmc' ......
    ## mcmc                           = list()     # mcmc used to specify the inference algorithm
    ## mcmc$seed                      = 0
    ## mcmc$samples                   = 8000
    ## mcmc$thinningFactor            = 5
    ## mcmc$burnin                    = 200
    ## mcmc$chainNumber               = 3
    ## mcmc$maxMoveStepSize           = 4
    ## mcmc$trendResamplingOrderProb  = 0.1
    ## mcmc$credIntervalAlphaLevel    = 0.95
    ## #......End of displaying mcmc ......
    ## 
    ## #......Start of displaying 'extra' ......
    ## extra                      = list()     # extra used to configure output/computing options
    ## extra$dumpInputData        = TRUE
    ## extra$whichOutputDimIsTime = 1
    ## extra$computeCredible      = FALSE
    ## extra$fastCIComputation    = TRUE
    ## extra$computeTrendOrder    = TRUE
    ## extra$computeTrendChngpt   = TRUE
    ## extra$computeTrendSlope    = TRUE
    ## extra$tallyPosNegTrendJump = TRUE
    ## extra$tallyIncDecTrendJump = TRUE
    ## extra$printProgressBar     = TRUE
    ## extra$printOptions         = TRUE
    ## extra$consoleWidth         = 80
    ## extra$numThreadsPerCPU     = 2
    ## extra$numParThreads        = 0
    ## #......End of displaying extra ......
    ## 
    ## \Progress:  0.0% done[>********************************************************]|Progress:  4.2% done[==>******************************************************]/Progress:  8.3% done[=====>***************************************************]-Progress: 12.5% done[=======>*************************************************]\Progress: 16.7% done[==========>**********************************************]|Progress: 20.8% done[============>********************************************]/Progress: 25.0% done[==============>******************************************]-Progress: 29.2% done[=================>***************************************]\Progress: 33.3% done[===================>*************************************]|Progress: 37.5% done[=====================>***********************************]/Progress: 41.7% done[========================>********************************]-Progress: 45.8% done[==========================>******************************]\Progress: 50.0% done[=============================>***************************]|Progress: 54.2% done[===============================>*************************]/Progress: 58.3% done[=================================>***********************]-Progress: 62.5% done[====================================>********************]\Progress: 66.7% done[======================================>******************]|Progress: 70.8% done[========================================>****************]/Progress: 75.0% done[===========================================>*************]-Progress: 79.2% done[=============================================>***********]\Progress: 83.3% done[================================================>********]|Progress: 87.5% done[==================================================>******]/Progress: 91.7% done[====================================================>****]-Progress: 95.8% done[=======================================================>*]\Progress:100.0% done[=========================================================]

``` r
plot(out1, main = "Girls suicide")
```

![](YRBS+Wonder_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
plot(out2, main = "Girls YRBS feelings of sadness")
```

![](YRBS+Wonder_files/figure-gfm/unnamed-chunk-4-2.png)<!-- -->

``` r
plot(out3, main = "Girlss YRBS contemplation of suicide")
```

![](YRBS+Wonder_files/figure-gfm/unnamed-chunk-4-3.png)<!-- -->
