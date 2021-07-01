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

While the Yahoo Finance data allowed us to do almost everything we wanted, we couldn't go as far into the past as we had hoped. In order to do this, we found data that went all the way back to 1877 (linked [here](http://www.econ.yale.edu/~shiller/data.htm)). 

After importing this data from a xcel spreadsheet, we used a very similar process as before. The only difference is that we grouped the data into multi year periods based on the secular bull and bear markets to see if there is a difference in the May Effect between those periods. Here is the code block that loops through the data, groups the prices, and calculates the percent change. Note that while the syntax looks different than other programs logic, these two code blocks do the exact same thing.
```
# For each row in the data sheet, get the necessary data and calculate the percent change
for i in range(len(data["Unnamed: 0"])):
    if str(data["Unnamed: 0"][i])[1].isnumeric():

        # Note, the years in the line below will be changed for each run through to keep the proper time frame
        if float(str(data["Unnamed: 0"][i])) > 2009 and float(str(data["Unnamed: 0"][i])) < 2022:

            # Store the current date
            if len(str(data["Unnamed: 0"][i])) == 7 and str(data["Unnamed: 0"][i])[1].isnumeric():
                cur_date = str(data["Unnamed: 0"][i])[5] + str(data["Unnamed: 0"][i])[6]

            # The number 10 was corrupted on the date sheet, so here is our accounting for that
            elif len(str(data["Unnamed: 0"][i])) == 6 and str(data["Unnamed: 0"][i])[1].isnumeric():
                cur_date = "10"
            else:
                cur_date = 0

            # Start on the first May of the data sheet so we have all complete time periods
            if cur_date == "05" and begin == False:
                begin = True

            # If it is May, begin time period
            if cur_date == "05" and data["Unnamed: 1"][1] is not None:
                start_price = data["Unnamed: 1"][i]

            # If it is October, finish time period at the end of the month
            if cur_date == "10" and data["Unnamed: 1"][1] is not None:
                may_october.append(((float(data["Unnamed: 1"][i]) - float(start_price)) / float(start_price)) * 100)

            # If it is the start of November, start next period
            if cur_date == "11" and data["Unnamed: 1"][1] is not None:
                start_price = data["Unnamed: 1"][i]

            # If it is the end of April, finish the time period
            if cur_date == "04" and data["Unnamed: 1"][1] is not None and begin == True:
                november_april.append(((float(data["Unnamed: 1"][i]) - float(start_price)) / float(start_price)) * 100)
```

After gathering all the percent changes for each period, the rest of the program is the same as the previous one. We removed any incomplete data, averaged the whole data set, and plotted it.

  



