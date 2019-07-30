# Project-2

# Stock market and New York Times project

The S & P 500 or "Standard and Poor's 500" is an index of 500 major stocks traded on the NYSE and NASDAQ stock exchanges.  For instance, the list includes Walmart, Apple, and Netflix.  This project is about analyzing the values of the stocks in the S & P 500 over the time period 1998-2013.  This time period has been selected because I was able to obtain free historical stock information for this periodfrom the QuantQuote website (quantquote.com).  

It is useful to know the "market cap" (or "market capitalization") of each stock, which equals the price per share times the number of shares.  This is the total value of the company: the amount you would have to pay if you were to write a check and buy that whole company.  It can reach almost a trillion dollars in the case of Apple or Amazon.  QuantQuote does not provide the market cap, so instead I obtained this information from the Fidelity website (fidelity.com). Fidelity only gives the market cap in 2018, so I made the approximation that the market cap in 2013 equals the market cap in 2018.

I was also interested in the relationship between the market cap, the growth of the stocks, and the references to these stocks on the New York Times online newspaper.  I was able to explore the New York Times online using an API provided by the newspaper.  I thought perhaps that bigger companies would be referenced more frequently in the newspaper, or that fast-growing companies would be referenced more.  Therefore, I have obtained the number of references to each stock on the New York Times, using the New York Times API.  My code permits comparisons between the 2018 market cap of the stock, the growth ratio of the stock (by what factor it grew between 1998 and 2013), and the number of New York Times hits.  Only New York Times references during the time period 1998-2013 are considered.

Sector information (such as classifying stocks as "Information Technology") is also obtained from the Fidelity website.  This is interesting if you want to see the tech bubble around 2001 for example.

Stock histories and sector histories can be plotted over the 15 year period.

The main analysis is stored in the file "Stock prices.ipynb".

The code allows you to perform various tests using several functions.  You can choose the stocks and sectors that you test.  You might enjoy deciding which tests to perform yourself.  If you want to do this, it is easy to load the data, which are stored in two pickle files:

1) Obtain a copy of the git repo
2) From the main directory of the project, cd quantquote_daily_sp500_83986/daily
3) unzip data.pickle.zip (this produces a 100 MB file)
4) unzip hits.pickle.zip (this produces a small file)
5) Go back to the root directory of the local repo
6) Run jupyter notebook and open “Stock prices.ipynb”
7) Run the two “unpickle” commands at the beginning of the file (for hitdict and StockData).  
NOTE: Do not run the _first_ two commands which are commented out and say "Do not run this command."  If you run them, they will attempt to generate the data files from scratch.
8) The data are now loaded.  You should be able to run the functions described in the jupyter notebook file to analyze any stocks or sectors of your choosing.

Future work: To expand on this project, I could explore other sources of financial articles, such as the Wall Street Journal.  I noticed that with the New York Times, a company's growth did not correlate with the amount of news coverage.  Perhaps this happens because the New York Times is intended for general audiences.  General audiences care about corporations that affect their daily lives.  They might want to know if Apple makes a new iphone.  They do not particularly care about Apple's market capitalization.  If AT&T is or is not growing, that is irrelevant to a general audience.  If AT&T is their phone company, they want to know about it, whether it is growing or not.  General audiences do not care about Texas Instruments' semiconductor business; they think of it as a company that produces calculators.  Therefore, they do not care if semiconductors happen to be booming.  In contrast, it seems possible that a more financially-oriented news source could write about companies' growth, trying to analyze how and why they are growing.

Technical note 1: The QuantQuote website provides the price of an individual share of stock, corrected for dividends and splits.  In other words, if a stock pays dividends to the investor, then that money is not going toward increasing the investor's wealth; it is just income.  But if the investor were to re-invest the dividends, they could buy more stock and increase their wealth.  QuantQuote assumes the investor will do this: the dividends will be used to increase the investor's stock holdings.  Another correction is needed when a split occurs.  Each share of the stock may turn into two shares, each with half the value of the original.  QuantQuote ignores this change (which is really just a matter of bookkeeping) and pretends that the investor owns the original, unsplit stocks with the original value.

Technical note 2: the process for actually re-creating the pickle files from scratch is somewhat tricky.  You first need to get a New York Times API key from the New York Times API website.  Replace the string "You need to obtain your API key" in the code with your API key.  Then you need to create a new StockData object and run the create() function, with use_NYT = True.  If the program crashes, use begin_stock (and end_stock = None) to start again where you left off.  This requires counting how many you have already done (the total number of the most recent run is printed by the create() function.).  Your work is saved in the StockData object's dictionaries.  You can also set use_NYT = False, which does not require an API key but requires you to have a "hits" dictionary already complete.  (The "hits" dictionary can be found by unpickling "hits.pickle".)

Information about QuantQuote data:

***QuantQuote Free Historical Stock Data***

This collection of daily resolution data goes back to 1998 for all symbols currently active in the S&P500. It is updated quarterly, the last update was 07/31/2013 (for more frequent updates, contact us). While this data is available for free from multiple online sources, the QuantQuote Free Daily Data has several advantages not found elsewhere:

***Full split/dividend adjustments for OHLCV***

Single zip file makes downloading ~500 symbols a one step process

QuantQuote data quality means errors in many free sources (such as Yahoo) are not present.

For format information, please consult our minute resolution data documentation.

Our active S&P500 daily resolution collection is provided completely free of charge and because of that, it is not covered under our lifetime support gauranty. Data is provided as is, with no warranty. However, if you do have questions about the data or find errors, please feel free to reach out to our support team at support@quantquote.com.

Happy trading,

The QuantQuote Team

***Splits***

When a stock split occurs, the data is adjusted to reflect this so that the data is more or less continuous. If the stock price is 20 and then a 2:1 split occurs, bringing the price to 10, all data ***before the split date*** is divided by 2. The split factor data column is then multiplied by 2. The data thus reflects how much money an investor would expect to make by investing at the beginning of a period and selling at the end of the period without having to take split discontinuities into account. The true price of the stock on any day can be recovered by multiplying the listed price by the split factor. The open, high, low, close, volume, and dividend columns are all split-adjusted.   ***[In other words, the price shown is the price as if all splits had already occurred]***
