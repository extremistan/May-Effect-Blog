# May Effect Blog 

All of our analysis and results can be found in the blog on our [website](https://extremistanresearch.com). In this README, we will  broadly explain our code, as   well as our though process in our methodology. 
  
We used 2 python programs to gather the  data for our blog. This was neccesaary because we used two different data sets, which both needed slightly different       methods for importing and analyzing.


## may_effect.py

The first python file we used was may_effect.py. This program uses the Yahoo Finance API to import the stock data. To properly judge the May Effect, we first       imported our data. We went as far back as Yahoo Finance would allow with monthly data.
  
`data = yf.download("SPY", start="1900-01-01", end="2021-05-01", interval = "1mo")`
  
We then looped through all the data. Everytime it was the start of May, we would store the data in one list, and when that period ended and Novembner started, we would store the data in another list. After each period, we would caculate the average percent change for the 6 month period. 
```
for i in range(len(data.index)):

    # Begin on the first May of the data set
    if int(data.index[i].month) == 5 and begin == False:
        begin = True

    if begin:

        # If it is May, start the time period
        if int(data.index[i].month) == 5:
            start_price = data["Open"][i]

        # Finish time period at the end of October
        elif int(data.index[i].month) == 10:
            may_september.append(((data["Close"][i] - start_price) / start_price) * 100)

        # Start next time period at the beginning of November
        elif int(data.index[i].month) == 11:
            start_price = data["Open"][i]

        # Finish time period at the end of April
        elif int(data.index[i].month) == 4:
            november_april.append(((data["Close"][i] - start_price) / start_price) * 100)
```
We then removed any empty data that may have appeared in our lists, and then averaged the percent change over all the periods to get a total percent change for each 6 month period. Finally, we graphed the data in a bar chart and saved it.


## may_effect_alternate_data.py

While the Yahoo Finance data allowed us to do almost everything we wanted, it didn't allow us to go as far into the past as we had hoped. In order to do this, we found data that went all the way back to 1877 (linked here).


  



