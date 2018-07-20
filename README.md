# Project-2
Stock market and New York TImes project

This project is about analyzing the values of the stocks in the S & P 500 over the time period 1998-2013.  This time period has been selected because I was able to obtain free historical stock information from Quant Quote.

I have also obtain the number of references to each stock on the New York Times, using the New York Times API.  My code permits comparisons between the final value of the stock (actually in 2018, taken from the Fidelity website), the growth ratio of the stock (how much it grew between 1998 and 2013), and the number of New York Times hits.  Only references during the appropriate time period are considered.

Sector information (such as classifying stocks as "Information Technology") is also obtained from the Fidelity website.

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
NOTE: Do not run the _first_ two commands which are commented out and say "Do not run this command."  If you run them, they will attempt to generated the data files from scratch.
8) The data are now loaded.  You should be able to run the functions described in the jupyter notebook file to analyze any stocks or sectors of your choosing.

Note: the process for actually re-creating the pickle files from scratch is somewhat tricky.  You first need to get a New York Times API key from the New York Times API website.  Replace the string "You need to obtain your API key" in the code with your API key.  Then you need to create a new StockData object and run the create() function, with use_NYT = True.  If the program crashes, use begin_stock (and end_stock = None) to start again where you left off.  Your work is saved in the StockData object's dictionaries.  You can also set use_NYT = False, which does not require an API key but requires you to have a "hits" dictionary already complete.  (The "hits" dictionary can be found by unpickling "hits.pickle".)

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
