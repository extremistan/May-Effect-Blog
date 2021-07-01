# May Effect Blog 

  All of our analysis and results can be found in the blog on our [website](https://extremistanresearch.com). In this README, we will  broadly explain our code, as   well as our though process in our methodology. 
  
  We used 2 python programs to gather the  data for our blog. This was neccesaary because we used two different data sets, which both needed slightly different       methods for importing and analyzing.

## may_effect.py

  The first python file we used was may_effect.py. This program uses the Yahoo Finance API to import the stock data. To properly judge the May Effect, we first       imported our data. We went as far back as Yahoo Finance would allow with monthly data.
  
  `data = yf.download("SPY", start="1900-01-01", end="2021-05-01", interval = "1mo")`
  
  
  



