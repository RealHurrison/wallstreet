# wallstreet
Real time Stock and Option tools.

Wallstreet is a Python library for monitoring and analyzing real time Stock and
Option data. Quotes are provided from the Google Finance API. Wallstreet requires
minimal input from the user, it uses available online data to calculate option
greeks and even scrapes the US Treasury website to get the current risk free rate.


Usage
-----

Stocks

.. code-block:: Python

  from wallstreet import Stock, Call, Put

  >>> s = Stock('AAPL')
  >>> s.price
  96.44
  >>> s.price
  96.48
  >>> s.change
  -0.35
  >>> s.last_trade
  '21 Jan 2016 13:32:12'

Options

.. code-block:: Python

  >>> g = Call('GOOG', d=12, m=2, y=2016, strike=700)
  >>> g.price
  38.2
  >>> g.implied_volatility()
  0.49222968442691889
  >>> g.delta()
  0.56522039722040063
  >>> g.vega()
  0.685034827159825
  >>> g.underlying.price
  706.59

Alternative construction

.. code-block:: Python

  >>> g = Call('GOOG', d=12, m=2, y=2016)
  >>> g
  Call(ticker=GOOG, expiration=12-02-2016)
  >>> g.strikes
  (580, 610, 620, 630, 640, 650, 660, 670, 680, 690, 697.5, 700, 702.5, 707.5, 710, 712.5, 715, 720, 725, 730, 732.5, 735, 737.5, 740, 742.5, 745, 747.5, 750, 752.5, 755, 760, 762.5, 765, 767.5, 770, 775, 777.5, 780, 782.5, 785, 787.5, 790, 792.5, 795, 800, 802.5, 805, 807.5, 810, 830, 910)
  >>> g.set_strike(712.5)
  >>> g
  Call(ticker=GOOG, expiration=12-02-2016, strike=712.5)

or

.. code-block:: Python

  >>> g = Put("GOOG")
  No options listed for given date, using 22-01-2016 instead
  >>> g.expirations
  ['22-01-2016', '29-01-2016', '05-02-2016', '12-02-2016', '19-02-2016', '26-02-2016', '04-03-2016', '18-03-2016', '15-04-2016', '17-06-2016', '16-09-2016', '20-01-2017', '19-01-2018']
  >>> g
  Put(ticker=GOOG, expiration=22-01-2016)


Dependencies
------------

Wallstreet requires to have Scipy, requests and bs4 (BeautifulSoup4) installed.


Stock Attributes
----------------

- ticker
- price
- id
- exchange
- last_trade
- change   (change in currency)
- cp   (percentage change)


Option Attributes and Methods
-----------------------------

- strike
- expiration
- underlying  (underlying stock object)
- ticker
- bid
- ask
- price (option price)
- id
- exchange
- change  (in currency)
- cp  (percentage change)
- volume
- open_interest
- code
- expirations (list of possible expiration dates for option chain)
- strikes (list of possible strike prices)

- set_strike()
- implied_volatility()
- delta()
- gamma()
- vega()
- theta()
- rho()