# FIN-654

This project focused on a fixed portfolio consisting of companies that have been recently hacked or breached.  In general, efforts in this project attempts to put into place a frame of analysis to determine the impact to stock values. However, follow-up studies could determine whether companies had or lacked business acumen to mitigate or minimize the effect of such occurrences.  Further analysis could also indicate whether to avoid volatile stocks that have been hacked or breached, and whether different sectors are more impacted.

## Dependency

This project requires local [R installation](https://cran.r-project.org/bin/).  However, all required [packages](https://github.com/jeff1evesque/fin-654/tree/master/packages) have been automated, using a combination of conditional [`install.packages`](https://github.com/jeff1evesque/fin-654/blob/master/app.R#L20-L37), as well as custom [utility functions](https://github.com/jeff1evesque/fin-654/blob/master/app.R#L38-L67). However, edge cases may exist.  For example, linux systems may require [additional configurations](https://github.com/jeff1evesque/fin-654/blob/master/app.R#L4-L17):

```bash
yum install -y libgcc
yum remove gcc
```

## Data

Three [different datasets](https://github.com/jeff1evesque/fin-654/blob/master/app.R#L345-L373) were ultimately used for the overall project:

- [security](https://github.com/jeff1evesque/fin-654/tree/master/data/security): csv files listing company names that have been breached or hacked
- [stock-exchange](https://github.com/jeff1evesque/fin-654/tree/master/data/stock-exchange): csv files listing ticker symbols and associated company names

The [security](https://github.com/jeff1evesque/fin-654/tree/master/data/security) and [stock-exchange](https://github.com/jeff1evesque/fin-654/tree/master/data/stock-exchange) dataset were [joined](https://github.com/jeff1evesque/fin-654/blob/master/app.R#L361-L366) to produce a list of stock tickers that have been breached or hacked. This list of tickers was passed into the [quandl api](https://github.com/jeff1evesque/fin-654/blob/master/packages/fin654/R/load_symbol.R#L19-L43) to produce the symbol dataset:

- [symbol](https://github.com/jeff1evesque/fin-654/tree/master/data/symbol): csv files of each ticker, containing daily open, close, low, high and overall volume

**Note:** the entire process of [download/loading](https://github.com/jeff1evesque/fin-654/blob/master/packages/fin654/R/load_symbol.R) datasets is completely automated.  If local [symbol](https://github.com/jeff1evesque/fin-654/tree/master/data/symbol) dataset already exists, it will be used. Otherwise, the dataset will be generated on-demand, and will require a valid [`Quandl.api_key`](https://github.com/jeff1evesque/fin-654/blob/master/packages/fin654/R/load_symbol.R#L29).


## Execution

Executing the overall project can be done with a single command:

```bash
Rscript app.R
```

Once the R shiny application is running, it can be accessed via `localhost:8100` (i.e. 127.0.0.1:8100).
