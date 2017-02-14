---
layout: post
title: Introducing Mortgage v1.0.0
categories: blog
date: 2017-02-13 20:30:00 -0600
---

Mortgage is a simple package that aims to make the lifetime cost of a mortage easier to understand.

Version 1.0.0 is out on PyPI and can be installed with

```commandline
pip install mortgage
```

### How To Use

Begin by importing the loan class.

```python
from mortgage import Loan

``` 

Create a simple mortgage.

```python
loan = Loan(principal=200000, interest=.06, term=30, start_date=(2017,3,1))
```

View a summary of pertinent mortgage information by calling the summarize property.

```python
loan.summarize

>>> Original Balance:         $    200,000
>>> Interest Rate:                    0.06 %
>>> APY:                              6.17 %
>>> APR:                              6.00 %
>>> Term:                               30 years
>>> Monthly Payment:          $    1199.10

>>> Total principal payments: $ 200,000.00
>>> Total interest payments:  $ 231,676.38
>>> Total payments:           $ 431,676.38
>>> Interest to principal:           115.8 %
>>> Years to pay:                     30.0
```

Pay particular attention to the Interest to Principal ratio. With the mortgage terms above, you will pay **115%** of the original balance in interest! Compare that to the same loan with a 15 year term below


```python
from mortgage import Loan
loan = Loan(principal=200000, interest=.06, term=15, start_date=(2017,3,1))
loan.summarize

>>> Original Balance:         $    200,000
>>> Interest Rate:                    0.06 %
>>> APY:                              6.17 %
>>> APR:                              6.00 %
>>> Term:                               15 years
>>> Monthly Payment:          $    1687.71

>>> Total principal payments: $ 200,000.00
>>> Total interest payments:  $ 103,788.46
>>> Total payments:           $ 303,788.46
>>> Interest to principal:            51.9 %
>>> Years to pay:                     15.0
```
In this case, you only pay **52%** of the original loan balance in interest. Obviously, the shorter the term with all else equal, the less interest you'll pay. But it helps to know exactly how much less you'll pay.

### Next Steps

I have some ideas for way to improve functionality and add features. My first two targets will be adding support for extra payments and a prettier print of the amortization schedule.
 

I hope you find the package useful! Feel free to open an issue with suggestions, imporovements, ideas, etc over at [Github](https://github.com/austinmcconnell/mortgage). 
