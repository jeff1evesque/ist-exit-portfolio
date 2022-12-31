# IST-736

This is a final project for a short 10 week course in text mining. Coding, visualizations, and overall report were improved after completion of the course, then submitted within a portfolio requirement for graduation. In general, the project attempts to address several items, including the larger question -- Can Market Sentiment Predict the Stock Market?

## Codebase

The entire [project codebase](https://github.com/jeff1evesque/ist-736) can be downloaded:

```bash
git clone https://github.com/jeff1evesque/ist-736.git
```

## Dependency

This project requires the following packages:

```bash
$ sudo pip install nltk \
    matplotlib \
    twython \
    quandl \
    sklearn \
    scikit-plot \
    statsmodels \
    seaborn \
    wordcloud \
    keras \
    numpy \
    h5py
```

## Data

Two different datasets were acquired via the [Twython](https://twython.readthedocs.io/en/latest/) and [Quandl](https://docs.quandl.com/) API:

- [financial analyst](https://github.com/jeff1evesque/ist-736/tree/master/data/twitter) tweets
- [stock market](https://github.com/jeff1evesque/ist-736/tree/master/data/quandl) index/volume measures

Due to limitations of the twitter API, roughly 3200 tweets could be collected for a given [user timeline](https://developer.twitter.com/en/docs/tweets/timelines/api-reference/get-statuses-user_timeline). However, the quandl data has a much larger limit. This imposed a [limitation](https://github.com/jeff1evesque/ist-736/blob/master/app/join_data.py) upon [joining data](https://github.com/jeff1evesque/ist-736/blob/master/app.py#L103-L116). Specifically, only a subset of the quandl dataset was utilized during the analysis.

## Execution

A provided [`config-TEMPLATE.py`](https://github.com/jeff1evesque/ist-736/blob/master/config-TEMPLATE.py) is required to be copied as `config.py` in the same directory. If additional twitter user timelines, or quandl stock index are required, the contents of the copied `config.py` need to match, respectively.

Further, the overall data collection is [idempotent](https://en.wikipedia.org/wiki/Idempotence). Since [`TwitterQuery`](https://github.com/jeff1evesque/ist-736/blob/58e1169a0c3d96da724db496d3adeb4f241b7752/consumer/twitter.py#L36-L67) and [`QuandlQuery`](https://github.com/jeff1evesque/ist-736/blob/58e1169a0c3d96da724db496d3adeb4f241b7752/consumer/quandl.py#L27-L46) has already been executed for the overall project, corresponding twitter and quandl csv files have already been produced. This means running the codebase again, will not rewrite or delete existing datasets. In order to generate new files for the same ticker or analyst, existing files need to be moved, deleted, or renamed.

Additionally, only one analysis can be performed at a given time, which involves commenting out segments of [`analysis.py`](https://github.com/jeff1evesque/ist-736/blob/master/app/analysis.py) prior to execution. Moreover, timeseries sentiment models (consisting of both ARIMA and LSTM) has an added constraint. Only one stock code can be implemented at a given time:

```python
screen_name = [
    'jimcramer',
    'ReformedBroker',
    'TheStalwart',
    'LizAnnSonders',
    'SJosephBurns'
]
codes = [
    ('BATS', 'BATS_AAPL'),
##    ('BATS', 'BATS_AMZN'),
##    ('BATS', 'BATS_GOOGL'),
##    ('BATS', 'BATS_MMT'),
##    ('BATS', 'BATS_NFLX'),
##    ('CHRIS', 'CBOE_VX1'),
##    ('NASDAQOMX', 'COMP-NASDAQ'),
##    ('FINRA', 'FNYX_MMM'),
##    ('FINRA', 'FNSQ_SPY'),
##    ('FINRA', 'FNYX_QQQ'),
##    ('EIA', 'PET_RWTC_D'),
##    ('WFC', 'PR_CON_15YFIXED_IR'),
##    ('WFC', 'PR_CON_30YFIXED_APR')
]
```

The above limitation is largely due to exceeding memory availability for a local machine. Should this codebase be extended as a [restful application](https://aws.amazon.com/what-is/restful-api/), the problem could resolve itself.  Therefore, the overall analysis can be executed in a stepwise fashion, by (un)commenting portions of [`analysis.py`](https://github.com/jeff1evesque/ist-736/blob/master/app/analysis.py), as well as modifying `codes` from `config.py`:

```bash
$ pwd
/path/to/web-projects/ist-736
$ python app.py
```
